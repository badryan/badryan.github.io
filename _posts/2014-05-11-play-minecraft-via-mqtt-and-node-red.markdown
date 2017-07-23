---
layout: post
title: Play Minecraft via MQTT and Node-RED
date: '2014-05-11 16:33:17'
tags:
- node-red
- education
---


[![photo](http://logic.sysbiol.cam.ac.uk/wp-content/uploads/2014/05/photo-300x224.jpg)](http://logic.sysbiol.cam.ac.uk/?attachment_id=1500)As man flu stopped me from doing any “meaningful work” this weekend, I took the opportunity to have a play with the Minecraft Python API for the [Raspberry Pi](http://raspberrypi.org), especially since on Saturday I’ve had a refresher course at the [Cambridge Raspberry Jam](http://camjam.me)Â (CamJam) with the very [Craig Richardson](https://twitter.com/CraigArgh), who maintains a great [Python/Minecraft blog](http://arghbox.wordpress.com) and is going to publish a book on the topic soon.

If you haven’t heard of [Minecraft](https://minecraft.net) and don’t have children, you can stop reading now. For people with children up to the teenage years, it’s likely that you’re actually facing a certain degree of Minecraft craze in your house already. Whatever it is that turns our children into hole digging, coal mining and house building computer addicts, it’s very powerful. To quote loosely from a presentation by Craig at a recent CamJam, in his experience as a teacher, if you simply add the word “Minecraft” to any exercise, the children double their effort and focus.

Mojang, the company who makes Minecraft, provides a free-to-download version of Minecraft for the Raspberry Pi as well as a set of libraries representing a Python API. This is meant as incentive for children to learn Python, and programmatically interact with the Minecraft world. There is a lot of information out there and on Craig’s blog there are plenty of links to projects that people have created with the API.

**Background**

My two older children are six and eight, and the older one has just managed to get to grips with basic programming logic using [Scratch](http://scratch.mit.edu). While he has expressed the wish to learn Python, I don’t think he’s quite ready yet to do more than using Python as interactive calculator. At the same time, they hear me going on about [MQTT](http://mqtt.org) and [Node-RED](http://nodered.org). In brief, MQTT is a messaging protocol that runs over TCP/IP and allows for very lean data communication, frequently in a machine-to-machine (“Internet of Things”, IoT) context. MQTT messages can be read like an email, where the so-called *topic* is the subject, and the *payload* is the body of the message. Node-RED is a rapid development tool for the IoT, which allows the quick design of workflows in a graphical editor using a [node.js](http://nodejs.org) backbone. Some people say Node-RED is “Scratch for adults”, and I don’t see anything wrong about that.

This is where my plan came in: Rather than exposing my children to Python and the frustration of having to use the Minecraft API with less than a rudimentary understanding of the language, I wanted them to be able to use the API via Node-RED. As Node-RED can’t talk to Minecraft directly (although I’m tempted to sniff around TCP port 4711 that is used by the API), I’m using Node-RED to dispatch MQTT messages that are taken up by a Python script in the background, which then translates this into the movement of the player in the Minecraft world. The message passing between Node-RED and Python happens through a so-called MQTT broker, and I’ve used [mosquitto](http://mosquitto.org). So it’s **Node-RED –MQTT-> mosquitto –MQTT-> Python –TCP-> Minecraft**.

**How-to**

1. Install Minecraft and the Python API on the Raspberry Pi as [described on Craig’s blog](http://arghbox.wordpress.com/2013/06/16/minecraft-pi-api-setting-up/).
2. Install Node-RED as described on the [Hardware Hacks blog](http://c-mobberley.com/wordpress/2013/10/03/raspberry-pi-hosting-node-red-take-the-crap-out-of-developing-automation-the-internet-of-things-iot/).
3. Install mosquitto and mosquitto clients (i.e. mosquitto_pub) via *sudo apt-get install mosquitto mosquitto-clients*
4. Install [Eclipse Paho MQTT](http://www.eclipse.org/paho/) libraries for Python via *sudo pip install paho-mqtt*
5. Test if Minecraft, Node-RED, mosquitto et al. work.
6. Assuming you have Node-RED running as a service (here’s a [hint on how to have this at startup](http://c-mobberley.com/wordpress/2014/01/12/raspberry-pi-node-red-startstoprestart-script/)), you also want to start up the mosquitto broker by issuing *mosquitto -p 1884* (a port of your choosing).

I took my inspiration for dealing with MQTT messages in Python from the “*simple subscribe example*” on the [mosquitto Python page](http://mosquitto.org/documentation/python/), making the relevant adjustments that are necessary through mosquitto’s handover to Paho. I’m too lazy to upload my .py code now (remember, I’m ill), but the code is short enough to get the idea from the screen shot.

![](/content/images/2015/09/code-1.png)

(actually, I find the Minecraft and MQTT APIs pretty amazing — just 36 lines of commented code!)

If you’re in a Minecraft world (you’re on your own here, or ask your children) and the Python script is running, you can test it using *mosquitto_pub -p 1884 -t /fwd -m “5″* (as in: go five steps forwards) or open the Node-RED GUI.

![](/content/images/2015/09/noderedmine.jpg)

Here, I simply use a inject nodes with topics “/fwd”, “/bck” etc. and payload “5″ to get the equivalent output through my MQTT out node on localhost port 1884.

Enjoy your own explorations!


