---
layout: post
title: Hacking dinosaurs at Blackgang Chine
date: '2015-10-12 11:54:25'
tags:
- tinkering
- hardware
- software
- node-red
---

Those of you who follow Twitter for hacking, making and crafting will know "celebrities" [Dr Lucy Rogers](https://twitter.com/drlucyrogers) and [Andy Stanford-Clark](https://twitter.com/andysc). For the past year or so, both have been showing pictures and videos of dinosaurs, and those lucky to see a cheerful Andy SC talk about what sort of fun nonsense one can do with a [Raspberry Pi](https://www.raspberrypi.org) and [Node-RED](http://nodered.org) may have seen the little **computers control animatronic dinosaurs**.
<center>
![](http://www.element14.com/community/servlet/JiveServlet/showImage/38-17488-207603/IMG_4194.jpg)
(Image from Element14 blog)
</center>
<br>
## Natural history (not of dinosaurs)
Part of the story goes that the potential of the animatronic dinosaurs is a lot bigger than what their control boxes allow one to do, and with the help of [James Macfarlane](https://twitter.com/RocketEngines), whose company [Airborne Engineering](http://www.ael.co.uk) builds all sorts of clever electronics, and who happens to be Lucy's partner, together they stringed them up to Raspberry Pis... ...add Andy SC and Node-RED, and you get the picture.

The complete story behind this is probably best told over a pint or two, but Lucy has organised three events that have brought together members of the hacking-making-crafting community at [**Blackgang Chine**](http://www.blackgangchine.com) on the Isle of Wight to play and experiment with cool technology... ...and very large dinosaurs. Element14 had blog posts on [#BlackgangPi 1](http://www.element14.com/community/people/drlucyrogers/blog/2015/04/27/blackgangpi-1), [#BlackgangPi 2](http://www.element14.com/community/people/drlucyrogers/blog/2015/04/27/blackgangpi-2) and a little video:

<iframe src="https://player.vimeo.com/video/109237787" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
<br>
## So what is #BlackgangPi ?
It's hard to describe. Although the hashtag for the event is typically #BlackgangPi and most hacks have a Raspberry Pi component, it's **not a Raspberry Jam**. It's an "invite only" event; that's primarily due to the nature of the work (which can involve high voltage, pneumatic control systems and heavy weights) and the venue of the hack (a small cafe at Blackang Chine), but if you're interested, drop Lucy an email at BlackgangPi@lucyrogers.com.

Just having returned from #BlackgangPi 3, I define #BlackgangPi as a win-win: Vectis Ventures, the company behind Blackgang Chine and a few other attractions on the Isle of Wight, host the event, feed the geeks and allow them to play with probably the coolest actuators on pre-historic Earth (with the help of their engineers), and in return the Blackgang Chine crew are exposed to some **new tech**, get **new ideas** and **hands-on** help with these projects. In fact some hack suggestions for last event included new IBM technology (a dinosaur Q&A with [Watson](http://www.ibm.com/madewithibm/uk/en/watson/), a [MQTT](http://mqtt.org)-based messaging system for inter-dino communications, etc.). So no matter if you come to the event as Blackgang Chine employee or external maker, there's something new to be learned.

<br>
## Begging for moooaarrrr....
I had previously tweeted about my **radio-based remote presence sensors with passive-infrared detection**
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">2,700 solder joints today. <a href="http://t.co/y20edVrnS2">pic.twitter.com/y20edVrnS2</a></p>&mdash; Boris Adryan (@BorisAdryan) <a href="https://twitter.com/BorisAdryan/status/647846114675269632">September 26, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
and Andy SC spotted the opportunity to use them in a dinosaur-context.

PCB production is a time-intense business and although Lucy, Andy and I are long-time customers of PCB manufacturer [Ragworm](http://www.ragworm.eu), we couldn't accelerate a process that -as a rule of thumb- takes about two weeks. The problem was timing, as #BlackgangPi 3 was scheduled for less than 14 days later. We approached Ragworm and, thankfully, they had only recently started their *LifeSaver Service*: When PCBs are produced, there's a certain amount of unused space left on the base matrix (imagine this like cutting out differently sized rectangles from a sheet of paper -- although you can try to optimise that process, there's always a bit of paper left over). What now happens is that Ragworm have developed a feel for which PCBs might be needed in the future, and produce more than what is actually being ordered, to fill the gaps. And we were lucky! After a few emails, **we received 10 of our Ragworm LifeSaver boards totally free of charge!**

Unfortunately, not all companies we approached were that generous, and we settled for four motion sensors that I built for Blackgang Chine.
<br>
## What I did...
Well, I built motion sensors that can send a message via a radio band to a Raspberry Pi. But that's going to be a different post... ...once they were built, this happened:
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">Now <a href="https://twitter.com/jpwsutton">@jpwsutton</a> of <a href="https://twitter.com/hashtag/mqtt?src=hash">#mqtt</a> fame takes my wireless sensors for some <a href="https://twitter.com/NodeRED">@NodeRED</a> magic to drive the dino boxes behind him. <a href="http://t.co/oh6woOOuyR">pic.twitter.com/oh6woOOuyR</a></p>&mdash; Boris Adryan (@BorisAdryan) <a href="https://twitter.com/BorisAdryan/status/652845081611890689">October 10, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/blackgangpi?src=hash">#blackgangpi</a> dinosaurs now sensing pray near the coffee machine and the fruit bowl. They interpret <a href="https://twitter.com/hashtag/mqtt?src=hash">#mqtt</a>. <a href="http://t.co/mTzLLIaSxE">pic.twitter.com/mTzLLIaSxE</a></p>&mdash; Boris Adryan (@BorisAdryan) <a href="https://twitter.com/BorisAdryan/status/652857771214413825">October 10, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
 <blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/blackgang?src=hash">#blackgang</a> joint venture between <a href="https://twitter.com/RocketEngines">@RocketEngines</a>, <a href="https://twitter.com/andysc">@andysc</a>, <a href="https://twitter.com/jpwsutton">@jpwsutton</a> and myself: table top dino roars upon movement. <a href="http://t.co/hhb2WuOCOW">pic.twitter.com/hhb2WuOCOW</a></p>&mdash; Boris Adryan (@BorisAdryan) <a href="https://twitter.com/BorisAdryan/status/652873209033957376">October 10, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
(The sensor is actually the small white blob near the basket on the right).
<br>
## Geek cost-benefit calculation
Travelling to the south coast of the Isle of Wight is neither fast nor cheap. It's a tourist metropolis and that has an influence on the price of accommodation. Also, while there is very small budget for components, any 'bigger' hacks require a certain amount of fundraising and preparation upfront... ...**"Why do it then?", you may ask.**

I learned soooo much during my trip!
<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">In 36 hours I travelled 500 kilometres, soldered and installed 4 sensors, wrote 2 Node-RED flows and met 20+ lovely people. <a href="https://twitter.com/hashtag/blackgangpi?src=hash">#blackgangpi</a></p>&mdash; Boris Adryan (@BorisAdryan) <a href="https://twitter.com/BorisAdryan/status/652930542606880768">October 10, 2015</a></blockquote>

Lucy had arranged for friendly people to lend me a bed for a night, [Matt](https://twitter.com/mattdawhit) and [Hannah](https://twitter.com/SudniHeritage). Not only that. While Matt was still on a business trip, Hannah picked me up from the ferry to get me to Blackgang Chine. Now she isn't just someone, she's well versed in essentially everything of cultural interest on the **Isle of Wight**, so much that people actually pay her for talking about it. But I got that for free! Later that evening, they picked me up from Blackgang, and Matt explained to me to the exact level of detail what I wanted to know about how wind **turbine blades** are being built on an industrial scale (amazing stuff!!!). The folk at the hack were all super friendly and helpful, and a learned a bit or two there as well -- including all the technical details I cannot go into here, as that would be a bit like a movie spoiler. But you can get wet at Blackgang Chine! :-) Another treat was a chat with [Laura Cowen](https://twitter.com/lauracowen) about the psychology of abstract quantities and what it has to do with the **Internet of Things** and the way more and more people will have to deal with 'big data'.

**Those conversations cannot be predicted, but they seem to happen more frequently when going to things like a dinosaur hack. So that's why. :-)**