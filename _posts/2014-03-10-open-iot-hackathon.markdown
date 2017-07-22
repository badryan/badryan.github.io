---
layout: post
title: Open IoT hackathon
date: '2014-03-10 10:02:17'
tags:
- iot
- node-red
---

![](/content/images/2015/09/lamp-139x300-1.jpg)

On Friday 7th March technology company [ARM](http://www.arm.com) hosted a hackathon, sponsored by the Technology Strategy Board (TSB) [IoT Ecosystem Demonstrator](https://connect.innovateuk.org/web/internet-of-things-ecosystem-demonstrator) competition. The IoT research branch of ARM along with [1248.io](http://www.1248.io) and others collaborate in the [@OpenIoTProject](http://www.openiot.org) in the exploration of connected IoT systems. Part of this exploration was the hackathon, where various data feeds from a diverse set of sensors on the ARM premises have been made available to the public along with a [call for any project](http://http://www.eventbrite.co.uk/e/open-iot-hackathon-and-demos-tsb-iot-ecosystem-demonstrator-tickets-10805705155?utm_source=eb_email&utm_medium=email&utm_campaign=event_reminder&utm_term=eventname&ref=eemaileventremind) (artwork, visualisation, analysis, web integration etc.) that people would come up with.

I’ve had a look at the [starter pack](https://groups.google.com/forum/#!topic/openiot-datasphere/KBfsMk0tFaI) (highly recommended read). I didn’t think I would stand a chance in the competition against ARM employees whose day job it is to come up with great IoT data analysis strategies, but I was keen to acquire some more technical IoT skills, namely:

- browsing of [HyperCat catalogues](http://wiki.1248.io/doku.php?id=hypercat) (these are hierarchical directories of ‘things’ Â whose feeds are made available by organisations)
- improve my JavaScript and do some real-time analysis in [NodeRED](http://nodered.org)
- use the [GoogleMap API](https://developers.google.com/maps/documentation/javascript/) to create an IoT mash-up.

To make a long story short, my attempts to use [MQTT](http://www.mqtt.org) in NodeRED to retrieve data from 1248.io’s [Geras database](http://1248.io/geras.html) (a data store for IoT data) where fruitless – nobody managed to receive data from that feed. Instead, I resorted to some manual HyperCat exploration and created a NodeRED flow to save data from one particular type of sensor (street lamps!!!) into my own Geras instance. The result of my experiment is summarised in a 20min movie/screen cast to be seen in [1248.io’s Google page](https://plus.google.com/115675618444978609621/posts/LJeFS9yEQ8N)


