---
layout: post
title: Deploying Raspberry Pi images at scale
date: '2015-09-14 12:30:27'
tags:
- iot
- tinkering
- software
- media
---

This is really just a very quick note about what to do when you have a large number of Raspberry Pis and, when you make changes to your configuration, how you can **avoid duplicating that SD card over and over again**.

Configuring a Raspberry Pi and updating software is relatively straightforward with most Linux distributions. However, native builds can take considerable time especially on the older versions of the hardware, and repeatedly downloading hundreds of megabytes per *apt-get* soon make one consider the duplication of a base image. There are fairly convenient programs for Windows and OS X around to mirror an SD card to disk and back on card, but even if the process takes just ten minutes per copy, deploying to a dozen Raspberry Pis can ruin a Saturday afternoon. It's getting **even more complicated if you don't have physical access** to the machines you want to update.
<br>
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/ben0NBOJIbA" frameborder="0" allowfullscreen></iframe></center>
<br>
In a recent short-talk at the [Cambridge Raspberry Jam](http://www.camjam.me), see video above, I outlined the deployment problem on the example of Raspberry Pis being used in Internet of Things projects (and why that may be a good idea).

I found [**resin.io**](http://www.resin.io) a viable solution for getting one and the same configuration on a set of Raspberry Pis. In short, after starting a project, *resin* offer a base image (*.img*) that checks every few minutes if you have changed the configuration of your Pi. It's doing that by connecting to an online system, quite similar to [Github](http://www.github.com) but in *resin*-space, and downloads your desired changes to the Raspberry Pis using that image. It's worth noting that you don't update that system with any binaries or *.img* files, but with a list of softwares you would like to see on that machine -- much like configuring a [Docker](http://www.docker.com) container, in that fact that's what *resin* is being a wrapper for.

Github, Docker, Cloud... It's fairly buzzword-heavy. However, that shouldn't scare you. There's a straightforward [walk-through on the resin website](http://docs.resin.io/#/pages/installing/gettingStarted.md) that exposes you to the **entire workflow in less than ten minutes**.