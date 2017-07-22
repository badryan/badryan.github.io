---
layout: post
title: Node-RED and Minecraft
date: '2015-09-03 09:14:34'
tags:
- node-red
- education
---

My work with [Node-RED](http://www.nodered.org) exposed me to plenty of concepts like [RESTful APIs](https://en.wikipedia.org/wiki/Representational_state_transfer), various [communication layers and protocols](https://en.wikipedia.org/wiki/OSI_model) such as IP, TCP, UDP, HTTP and MQTT, as well as the general notion that today's software mostly deals with the exchange of messages. In other words, these are the acronyms that hold your computer and the Internet together.

The [Minecraft Pi Edition](https://www.raspberrypi.org/learning/getting-started-with-minecraft-pi/worksheet/) is a great motivation for kids to learn programming in Python. A very popular book about controlling the Minecraft world with this scripting language is called [Adventures in Minecraft](http://www.amazon.co.uk/Adventures-Minecraft-David-Whale/dp/111894691X) and introduces the basic concepts of programming in a playful way. But where from here?

For [CamJam](http://camjam.me) I've developed a workshop that uses Node-RED as a platform to explore what's going on behind the scenes of Minecraft Pi. In brief, it talks the user through the OSI layers and how TCP can be used to send messages to the Minecraft binary: controlling Minecraft is as simple as sending ``chat.post(Hello)`` to a local interface.

![](/content/images/2015/09/Mincraft_API_in_Node-RED.jpg)

There are examples for one-way communication like sending a chat message, but the final exercises go into bi-directional TCP requests, flow-control and how JavaScript can be used to tabulate a histogram of block types to systematically mine the world for wood, sand, etc.

Download the [complete tutorial](http://www.slideshare.net/BorisAdryan/nodered-and-minecraft-camjam-september-2015) from SlideShare.