---
layout: post
title: Triggering Node-RED events with drawings
date: '2014-06-14 14:50:19'
tags:
- node-red
- education
---

![](/content/images/2015/09/photo.jpg)

Yesterday I visited [PrimeConf](http://www.primeconf.com) and, while entertaining my daughter with free biscuits, had a chance to talk to people from [Bareconductive](http://www.bareconductive.com) and [Aestheticodes](http://aestheticodes.com). At first I didn’t even look at Astheticodes, not quite knowing what watercolour images of carps have to do with… …anything, really. However, when Tony explained the principle behind their codes to nobody less than [Mini Geek Girl](http://about.me/minigirlgeek), I listened in and soon was captured by the possibilities of their product. Well, not product, but idea, range of apps, and services their company can provide. They, too, come from an academic background, and so I was very keen to have a go doing an “**Aestheticode**” today.

In brief, Aestheticodes are something like a [QR code](http://en.wikipedia.org/wiki/QR_code), but one that doesn’t suffer the constraint of being a boring square. One can do a drawing and any field that is within a continuous line counts towards the [code](http://aestheticodes.com/teach-me/). In my above example, the three rectangles and two triangles are all coding. Within each field, the number of objects is coding. Again, in my example, we have a triangle in triangle (1), a circle in a triangle (1), two triangles and a circle in a rectangle (3), and two other fields with (3) and (4) objects. In Aestheticode speak, that encodes “1:1:3:3:4″ (note that the counts are simply ordered by value). My drawing is rubbish, but it’s probably conceivable that somebody with a little bit of talent can draw and paint something aesthetic and encode a message.

![](/content/images/2015/09/triggered-300x57.png)

Aestheticodes require an [iPhone](https://itunes.apple.com/us/app/aestheticodes/id703429621?mt=8) or Android app that translate the code and call up a website. While I don’t see them replacing traditional QR codes anytime soon, at this stage I can see their approach being useful for home developers. In fact, as so often I couldn’t help but see a use case with [Node-RED](http://nodered.org). So configuring the Aestheticodes app to connect to *192.x.x.x:1880/aestheticode* upon seeing my funky cheese sandwich, and running a very simple Node-RED flow featuring a *http in* node, you can control your entire Internet-of-Things armada, or at least send a “cheese sandwich detected” tweet.


