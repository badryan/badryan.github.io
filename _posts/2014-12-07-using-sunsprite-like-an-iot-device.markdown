---
layout: post
title: Using SunSprite like an IoT device
date: '2014-12-07 15:21:54'
tags:
- iot
- software
- node-red
---

![](/content/images/2015/09/SunSprite-150x150.jpg)

The [SunSprite](https://www.sunsprite.com) is a small wearable device that monitors light exposure over the day. Why would you want to do that? Light is generally healthy, but many people with office jobs see most of it in the form of gloomy computer displays. While some people get away with that, others experience a drop in productivity or mood especially during the darker times of the year, frequently referred to as winter blues or seasonal affective disorder. With a SunSprite, you get a wearable companion that raises your awareness of the amount of light that you’re actually getting over the day…

The SunSprite has a LED indicator bar for quick checks throughout the day (the one in the picture tells you that we’re at 70% of the recommended light exposure today), and it speaks Bluetooth for syncing with recent iOS devices. These data are used for a more fancy display of today’s light exposure, and in combination with a cloud server allows for viewing more recent historic data. For what it says on the box, the SunSprite and the app do their job well enough.

In November the SunSprite team rolled out a [data portal](http://my.sunsprite.com/#/login) that allows to retrieve all data from their cloud: given a start and end date, it provides lux levels and UV levels with one-minute-resolution over the period. While the portal is convenient enough to get a dump of a week’s worth of device data, it’s not the sort of tool you want to use on a regular basis to explore your data.

I’ve been in contact with the SunSprite team for a while for a variety of curious questions, bug reports and general comments. I like my SunSprite. They’re a very responsive company. When I contacted them a few days before the [Thingmonk](http://thingmonk.com) hack day and pointed out I’d like to use my SunSprite in an Internet-of-things context, it didn’t take long for them to come back to me with a programmer’s dream: API access to their cloud service, hosted by [Kinvey](http://www.kinvey.com).

Disclaimer: What follows is an experimental exploration of the SunSprite platform. They have warned me. This kind of access is not officially supported. They may withdraw or change access to this API at any time. Given API credentials for Kinvey, app name *kid_Ve5xRCs7Mm* and app passphrase *a7f19fa982f4448e84b9ab29bd105a8b*, I knew I was interested in the collection *luxRecords* and field names* date*, *lux* and *uv*… I’m sharing app name and app passphrase with you for your own experiments. If you anger the gods of light, they will take this privilege away from us. Behave!

One of the most successful rapid IoT development frameworks is [Node-RED](http://nodered.org). For my experiments with the SunSprite API, I decided to use Node-RED as it provides the best of both worlds: simple URL calls like with *wget*, *curl* or other command line tools, yet powerful data handling capabilities using the JavaScript derivative *node.js*. Access to Kinvey works over a [REST API](http://en.wikipedia.org/wiki/Representational_state_transfer) (they detail it in their [developer guides](http://devcenter.kinvey.com/rest/guides/getting-started)).

First, we need to establish that our application is allowed to interact with Kinvey and that it’s a legit request from someone who is authorised by SunSprite to access their database. That’s where app name and app passphrase come into play. Their iOS app will have a different app name and app passphrase, which is why our experiment can be cleanly killed if we push to far. The API endpoint is *https://baas.kinvey.com*, followed by paths that each implement different functionality. This is where I spent a few hours cursing myself, SunSprite and ultimately Kinvey. In their [documentation of the login](http://devcenter.kinvey.com/rest/guides/users#login)Â process they say to connect to “*/user/:appKey/login*“. Now in the information I got from SunSprite, what I call app name is called ‘appkey’ and what I called app passphrase is called ‘appsecret’. In the end, a POST to the URLÂ *http://baas.kinvey.com/user/kid_Ve5xRCs7Mm/login* was what was needed.

![](/content/images/2015/09/SunSprite_login_flow.png)

Here’s the Node-RED login flow (click to zoom). Basic building blocks on top, the flow, and configuration details. The login process returns a JSON entry:

{“_id”:”5408a38ff374dfb81300811e”, “wakeUpTimeMin”:420, “sleepTimeMin”:1320, “sunSpriteUUID”:”B9ACE665-D4E2-E0DC-C6B8-8AF2A38EDCBA”, “_push”:{}, “syncRefDate”:”ISODate(\\”2014-12-06T17:23:47.177Z\\”)”, “possibleAchievementsCount”:12, “lastBatteryPercent”:1, “username”:”xxxxx@gxxxx.com”, “timezoneOffsetSec”:0, “luxGoal”:300000, “email”:”xxxxx@gxxxx.com”, “_kmd”:{“lmt”:”2014-12-06T17:45:20.259Z”,”ect”:”2014-09-04T17:38:23.221Z”,”emailVerification”: {“status”:”confirmed”, “lastStateChangeAt”:”2014-09-04T18:19:19.756Z”, “lastConfirmedAt”:”2014-09-04T18:19:19.756Z”, “emailAddress”:”xxxx@gxxx.com”}, “authtoken”:”xxxx”}, “_acl”:{“creator”:”5408a38ff374dfb81300811e”}}

So with a little gazing, it become obvious what device ID your SunSprite has, where you live (timezone offset), when you last synced with the platform, battery status, and, most importantly, an authtoken (here abbreviated with xxxx) to be used with all future queries. Our Node-RED flow defines a few of those as global variables *context.global.xxx*.

Unconstrained queries can easily yield more data than Kinvey is happy to provide in one go: 10k records is the most they will pass back to you per query. However, using the API endpoint at /appdata/*kid_Ve5xRCs7Mm*/*luxRecords*/?query=[filters]&[modifiers] as [detailed in their documentation](http://devcenter.kinvey.com/rest/guides/datastore#Querying) allows one to slice and dice their, what I assume, is a [MongoDB](http://www.mongodb.com) instance. A typical one minute data point looks like this:

{“_id”:”5481da9af84b57755b3fc938″, “lux”:0, “isGoodLux”:false, “goodLux”:0, “normalizedLux”:0, “uv”:-0.155, “date”:”2014-12-05T16:15:23.797Z”, “_acl”:{“creator”:”5408a38ff374dfb81300811e”}, “_kmd”:{“ect”:”2014-12-05T16:17:30.600Z”,”lmt”:”2014-12-05T16:17:30.600Z”}}

I couldn’t spot a difference between “lux” and “normalizedLux”, but that’s effectively the raw reads of brightness. “uv” is the UV index, which for some reason is negative in darkness. The “date” is when the measurement was taken (relative to your timezone offset, I live in Zulu time). I empirically determined that “isGoodLux” is true for lux values > 2500, which is the famous “bright enough” threshold in the iOS app. If data points are bright enough, “goodLux” is a positive integer. I assume that all lux values are added to a sum and expressed relative to luxGoal, as the summation of just the isGoodLux data points was below my daily percentage indicated in the iOS app.

![](/content/images/2015/09/SunSprite_addlux_flow.png)
My Node-RED flow (click to zoom) does the following: Between 7am and 10pm it polls data from Kinvey every 15min. It’s directing a get request to

*http://baas.kinvey.com/appdata/+appname+*  
*/luxRecords/?query={“date”:{“$lt”:”+tomorrow+”,”$gte”:”+today+”},”isGoodLux”:true}&fields=goodLux,date*

which yields relatively little data at a time. tomorrow and today are calculated on the basis of the date stamp coming from the inject node. I’m then looping over all goodLux values and, once I have more goodLux than LUXGOAL, I record the time of day and set a flag. Node-RED messages typically have a payload (which we have seen a few times before) and a topic, which in this case we set to “enough light”. The switch node simply asserts whether we’ve had “enough light” as a topic, and if so, sends a tweet with the payload set in accumulateGoodLux. A typical tweet may then look like: “294% of minimal, 100% at: 11:12:41″.

![](/content/images/2015/09/tweetLux.jpg)

This flow is available at flows.nodered.org: [http://flows.nodered.org/flow/fee5a61f0a4207f6bb46](http://flows.nodered.org/flow/fee5a61f0a4207f6bb46)


