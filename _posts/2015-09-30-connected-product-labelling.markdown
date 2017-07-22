---
layout: post
title: Connected product labelling
date: '2015-09-30 10:45:09'
tags:
- iot
---

A few months ago [Alex Deschamps-Sonsino](https://twitter.com/iotwatch) from the Internet of Things design and strategy consultancy [designswarm](http://designswarm.com) reflected on **our right to know** if and how a device shares our data with the outside world. I seem to distinctly remember a slide that showed different degrees of compliance with data exchange standards, much in the style of the [European energy efficiency label](https://en.wikipedia.org/wiki/European_Union_energy_label).
<br>
Recently [Martin Charlier](https://twitter.com/marcharlier), one of the co-authors of [Designing Connected Products](http://www.amazon.co.uk/Designing-Connected-Products-Consumer-Internet/dp/1449372562/ref=sr_1_1?s=books&ie=UTF8&qid=1443611017&sr=1-1&keywords=designing+connected+products) asked:

<center>
<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Thoughts after <a href="https://twitter.com/hashtag/responsibleobjects?src=hash">#responsibleobjects</a> <a href="https://twitter.com/method_inc">@method_inc</a>: What&#39;s the food pyramid or labelling for consumer electronics? <a href="http://t.co/UTTznP7utx">pic.twitter.com/UTTznP7utx</a></p>&mdash; Martin Charlier (@marcharlier) <a href="https://twitter.com/marcharlier/status/647003184142098432">September 24, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>
<br>
I spent a bit of time sieving through Alex D-S' [repository of SlideShares](http://www.slideshare.net/designswarm/presentations) but couldn't find the "energy label" representation. However, in the meantime, Alex posted:

<center>
<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">What does it do? A proposal for connected product labelling. WIP. <a href="https://twitter.com/hashtag/iot?src=hash">#iot</a> <a href="http://t.co/TF6vWDzcyi">http://t.co/TF6vWDzcyi</a></p>&mdash; designswarm (@designswarm) <a href="https://twitter.com/designswarm/status/648529000403456000">September 28, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</center>
<br>
While certainly a great entry point into the discussion, there a various challenges with connected products. I'm coming from a more technical perspective than Alex, so I thought about what I would consider an ideal label for (potentially connected) products in the future.

![](/content/images/2015/09/Data_label.jpg)
<br>
This is obviously just a first draft, but probably serves well to highlight the three pain points of connected consumer products: **Data Demand**, **Security** and **Privacy**.

* **Demand.** Is your device connected at all? Is it a data hog? Is it rendered totally useless without a functioning Internet connection or is it happy to occasionally talk to a local hub? In other words, does your web-connected thermostat still work when your communication line is down, or does with the Internet also your heating system fail?

* **Security.** This covers how save your device is and how resilient to outside attacks. We don't need to have this discussion if your device is not connected, but different communication technologies come with different risks. And while I'm probably (still somewhat) comfortable that my connected kitchen sink sends an unencrypted "Clean me!" via Xbee, there are certain domains in which I would hope for a physical range limit, proper authentication and encryption. The latter two become especially relevant with new technologies such as low-power wide-range networks, where the receiver of a radio message may be many kilometres away, with plenty of opportunities for an attacker to skim your information. (Needless to say that also your more locally restricted WiFi should be appropriately protected).

* **Privacy.** Assume your data has safely landed in the hands of your device manufacturer. Are you giving your rights away? In an ideal world, you'd be in complete control over which data is shared with whom and what for. Some data I'd share, but only if it's aggregated with other people's data so the individual data point cannot be traced back to me. On the opposite end of the spectrum, many of us don't even know (or care, or feel helpless) with what major player data companies are doing with our information. Do you want to live in a world where you rather not use a device for fear that the manufacturer sells it and your insurance premium might go up?

![](/content/images/2015/09/Data_label_definition.png)

I'd love to keep this discussion going.