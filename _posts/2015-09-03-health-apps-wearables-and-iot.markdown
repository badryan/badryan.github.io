---
layout: post
title: Health Apps, Wearables and IoT
date: '2015-09-03 14:26:23'
tags:
- iot
- tinkering
---

Ever since the arrival of my iPod Touch in 2008 I've occasionally tried apps and the built-in sensors to learn a little bit about myself. While I'm a data geek and keen to have accurate measurements, I soon discovered that simple monitoring my behaviour wasn't going to lead anywhere. Take the **drinking apps**, for example. Tallying up all the booze you've had over a period of time sounds like a good idea health-wise, but what's meant to help you control your alcohol habits turns you into judge and executioner in one. "*You've had five beers last night*". What does that mean? Is that a lot or a little? Five pint of Guinness probably contribute more to your deteriorating liver than five small bottles of a watery ale. While my apps allowed me to specify "standard drinks" with volume and alcohol content, I was back start after a night out to a pub I had not been before (and their excellent choice of beverages). Soon I realised that I was cheating myself by generously rounding my booze intake, and stopped.

Wearable devices and real sensors are the way to go, at least if you want accurate measurements and *actionable insight*. Over the years I've tried various **running trackers**, mostly to see how far my tours had taken me. In the beginning, I used a Nike+ sensor tied to my shoe laces, and after I've had established that the 6th Generation iPod Nano was within a few percent of the chip, I carried that around. However, at some stage I stopped. Sometimes I was fast. Sometimes I was slow. Sometimes I went home early. So what? Without any ambition to run a competition, it seemed pointless to check my speed, and after a while I've had a pretty good idea how far each of my runs were.

Let's talk about my current pet hate, **sleep trackers**. It's been clear since since their first arrival that sleeping [apps that utilise the gyroscope in your phone are rubbish](http://www.huffingtonpost.com/dr-christopher-winter/sleep-tips_b_4792760.html). My hopes were high when Kickstarter featured the very Apple-ish looking *Sense* sleep tracking device. It comes with a base unit that doubles up as communications hub for small gyroscopes (called *Sleep Pills*) that you can tag to your pillow, while also sensing environmental data (temperature, humidity, air quality, noise) to... ...to... ...I don't actually know. The thing is, the style of the video and the apparent attention to detail really *lulled* me into believing that this device could tell me a lot about my sleep. Maybe it even does. However, sleep is a complex beast, especially when you consider good sleep as a combination between a reasonable life-style and a good environment - without the raw data and with just a crude bar graph and an arbitrary score to look at, my *Sense* doesn't make any to me. There are a few tear-downs of *Sense*, for example from biomedical engineer [Lindsay Williams](http://lyndsaywilliams.blogspot.co.uk/2015/07/hello-sense-sleep-computer-under.html) and from [Robert Setiadi](http://www.robertsetiadi.com/one-week-experience-using-sense-sleep-tracker/). While the hardware seems in principle capable of delivering the promise of great insight, the software is a great letdown. Without access to the raw data or algorithmic details, the "Score" is at best subjective.

![](/content/images/2015/09/wearable_health.png)
<br>
My absolute darling and favourite wearable is the **day light tracker** *SunSprite*, a device that continuously tracks your exposure to day light in terms of brightness and UV levels. It scores best in terms of objectiveness and informativeness for me. Too little light is bad, as it screws with vitamin D production and melatonin metabolism. Too much UV is bad, you know, because sunburn. However, it takes a lot of practice to accurately judge whether one has had enough light for a day, or how much UV exposure there is (both especially in cloudy conditions). The SunSprite provides that sense we lack. While their app is very basic (but sufficient), upon my request they opened their data store and users can now [programmatically download their data](https://iot.ghost.io/using-sunsprite-like-an-iot-device/) for further analysis.

I [wrote a web app](https://iot.ghost.io/hosted-node-red-without-budget/) to visually represent data in a calendar view, a function not part of their iOS app. So if you visit the

* **[SunSprite Calendar View](https://fred.sensetecnic.com/public/adryan/index)**

you can see your data just like I have to celebrate on year of usage:
![](/content/images/2015/09/1-year-of-sunsprite.png)

<br>
**A word on opening up your platform:** It's not that I don't appreciate my *Sense*. I just don't find it particularly useful at the moment. Without the actual data, the *Score* is just somebody's arbitrary decision, and thus subjective. My recommendation: Give your users access to their data, and I'm sure there's going to be a lot of innovation coming from there.