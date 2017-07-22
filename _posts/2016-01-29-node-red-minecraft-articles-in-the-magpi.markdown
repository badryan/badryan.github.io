---
layout: post
title: Node-RED + Minecraft articles in the MagPi
date: '2016-01-29 09:52:36'
tags:
- software
- node-red
- education
- media
---

How can we get young people interested in computational thinking? One of my passions is the provision of tutorials that hopefully make them a little bit exited about technology. **Computational thinking is not just programming**: Sure, knowing the syntax of a particular language can be useful, but it's more important to understand how one can go about a problem using a computer generally.
<br>
Are data and code the same? Do code objects manipulate data? Or does information flow from one manipulation to the other? This may sound outright trivial and abstract at the same time, but there are exemplary programming languages for all of these paradigms: functional languages like Lisp and Clojure make no difference between code and data, in Java very much everything is an object, and then there is flow-based programming.
<br>
[Node-RED](http://www.nodered.org) is one example of the latter group, and with the latest distribution ("Jessie") of the operating system Raspian, it's come to [Raspberry Pi](http://www.raspberrypi.org) as a default programming tool. While it's easy to [convince seasoned programmers](https://iot.ghost.io/a-bunch-of-node-red-videos/) to give Node-RED a try, how can we attract that next generation of makers and coders to use it? The answer is simple: Add Minecraft.
The last two issues (41+42) of the official [Raspberry Pi magazine MagPi](https://www.raspberrypi.org/magpi/) featured my articles on Node-RED and Minecraft. The first part introduced the general look-and-feel of flow-based programming and how to find your way around Node-RED.
![](/content/images/2016/01/Node-RED_MagPi_Pt1.jpg)
I believe I managed to hide a lot of technical detail in a simple "Hello World" application. And the good thing is that, unless people want to engage with complex protocols, they don't need to. The Raspberry Pi version of Minecraft provides a TCP server that listens to port 4711. Any scripting or programming language that can connect via TCP is able to send API commands to the Minecraft server and receive back any return values. Now, those last two sentences can be an ideal opener to learn about the OSI communication model, the background of TCP/IP communication, what API actually stands for, and why sometimes you can't get things to work for the lack of a simple invisible character "\n", etc. In the article, I just casually referred to my somewhat longer [tutorial on Minecraft and Node-RED on SlideShare](http://www.slideshare.net/BorisAdryan/nodered-and-minecraft-camjam-september-2015). Within the article, I focus on guiding the reader step-by-step through what needs to be dragged-and-dropped together.
<br>
The second part of the small article series addresses a different level of complexity: If flow-based programming just means the linear passing on of information from one manipulation to the other, how can one implement state and loops? That's where a bit of Node-RED trickery comes in handy. Though global and local variables are covered in the [Node-RED documentation](http://nodered.org/docs/writing-functions.html#storing-data) (and so is the concept of spawning a new message "for each" in an array), a beginner might not appreciate the importance of these concepts and think that Node-RED is just useful when state and/or loops are required.
![](/content/images/2016/01/Node-RED_MagPi_Pt2.jpg)
In the context of Minecraft, I introduce loops with the following challenge: Once you know your player's position, iterate over a cube of blocks around you, and determine the material of each block. The latter means one TCP request per block, so the user has to compile a list of coordinates and, for each coordinate, send a message into the TCP node. That differs from the anatomy of a standard function node by just three lines, but unless you know exactly what you're looking for, that can be a frustrating experience. The article introduces that operation even before our young scholars realise that it can be an issue. Every one of the TCP request returns a value (here, of a block type). In order to tabulate which blocks are present in our cube, the flow needs to store that information in between iterations. Again, that's solved by just a few lines of code, and by playing Minecraft the article introduces the concept of state before people embark on other projects.
<br>
If you like the articles, my blog or the tutorials, please consider buying me a coffee or new HAT for my Raspberry Pi on [Patreon](https://www.patreon.com/adryan). Cheers!