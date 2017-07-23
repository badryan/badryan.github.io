---
layout: post
title: Turning a Nook Simple Touch into a wireless screen
date: '2014-03-18 14:21:30'
tags:
- tinkering
---

![](/content/images/2015/09/nook-300x226.jpg)

At the recent [Open IoT Hackathon](/2014/03/10/open-iot-hackathon.html) my closest competitor Ajith Shadakshari presented a hardware hack that utilised a [Nook Simple Touch](http://en.wikipedia.org/wiki/Nook_Simple_Touch) e-reader device as a low-energy wireless screen to dynamically display room occupancy, as informed by a data stream. I’m usually not one for hardware hacks as it is quite simple to brick your device and lose your investment, however, the low cost of the Nook (£50 at the time of writing) convinced me to have a go at it.

Hacking Nook devices seems to be a common sport and people with jailbreak/product hacking experience will find plenty of [tutorials on the internet](http://lmgtfy.com/?q=hacking+nook+simple+touch). This was my first exploration in this direction, and I didn’t want to “just hack it” but turn it into a useful home product: A wireless display for sensor data and Twitter updates that can go several days without recharging.

**Breaking it**

Ingredients for the hack:

- Nook Touch Simple, box fresh, with firmware v1.2.1
- microSD card, with SD adapter for my iMac
- a Google account for installing Android software from Google Play
- some basic Unix skills

I’m not going to copy&paste commands into here, but will highlight relevant bits from other tutorials which I followed. My main guide was [Turning a Nook Simple Touch into a minimalist writing tablet](http://http://www.alexroddie.com/2013/06/Nook-Simple-Touch-rooted-minimalist-writing-tablet.html) by Alex Roddie. He pointed me to two forum entries at a mobile developer website,

- [Rooting the Nook with NookManager – a graphical rooter](http://forum.xda-developers.com/showthread.php?t=2040351)
- [Installing NTGAppsAttack – Google Apps installer add-on for NookManager](http://forum.xda-developers.com/showthread.php?t=2086582)

I followed the first forum entry slavishly from 1. to 8. Everything else seems to concern trouble shooting and some technical background, but the gist really is in the first forum post. I was using a 4GB microSD card and I “burned” the image of the NookManager v0.5 using the *dd* command on my Mac (note: if you don’t know what an image or *dd* is, you probably don’t want to mess with your device). So this essentially puts a core Android installation to your feet. You are effectively running Unix now as root.

The second set of forum posts deals with installing NTGAppsAttack. Again, I followed all steps 1. to 23. from the first post slavishly (I didn’t have to 3.), and yes, where it says “23. … *Keep reading*“, you should. Installing SearchMarket was my final step. I remember the update process on the Nook showed something about downloading the app, which seemed to take forever, but in fact it took a reboot to find that the app had long been installed and the Nook was ready for action.

**Installing it**

The screen you can see above shows a HTML/CSS encoded website served from my [Raspberry Pi running NodeRED](/2014/02/12/airpi-speaks-nodered.html). Details on the software side of things to follow, in brief it’s using the *template* node to take data from my AirPi to make the website.

As Ajith had pointed out in his project description, he was using the [Dolphin Browser Mini](https://play.google.com/store/apps/details?id=com.dolphin.browser) that allows to run a web browser in windowless mode. The interval refresh of the page displaying all info is part of the NodeRED flow, as detailed in [Layer Zero Lab’s excellent blog post](http://l0l.org.uk/2014/01/simple-node-red-web-page/).

**Further tweaks**

…the awkward moment when you want to show off your Nook wireless screen, and it shows you the Barnes and Noble screen saver. Although already looking like a proper IoT device, in its core your Nook still thinks it’s an e-book reader. Not pressing any button or the screen results in screen saver activity and various sleep modes. Plus, it also think it’s a phone and wastes and awful lot of energy running phone apps. Both behaviours are not great if you want to leave your display for remote updates, without user interference.

The e-book software doesn’t support “no screen saver” and setting it to the slowest response just delays the inevitable. I’ve come to use the [WakeTimer](https://play.google.com/store/apps/details?id=schaze.waketimer) which keeps both the screen and the wifi connection alive. There are alternative suggestions including the manipulation of an internal SQLite database which contains the seconds to sleep, but starting up WakeTimer after every reboot isn’t too bad for now.

The energy wasted by the completely unnecessary phone services amounted to ~75% of the battery. In Alex Roddie’s blog post, he identifies those issues and recommends removal of *Phone.apk* and *TelephonyProvider.apk* in */system/app/* as possible solutions. However, he talks about the ES File Explorer in this context, and in my hands that application only gave me grief because for some reason */system* was mounted on a read-only partition, which opposite to some claims was not changeable on my Nook. Ultimately, I resorted to some manly command-line tinkering as root using a terminal program (can’t remember which one). I followed the example shown on [StackOverflow](http://stackoverflow.com/questions/5467881/a-terminal-command-for-a-rooted-android-to-remount-system-as-read-write) to remount /system as read/write partition (note that the exact mount points may be called differently on your device). Thereafter, I entered */system/app* with a chainsaw and deleted most of the applications listed in this forum entry: [Nook Simple Touch (N2E) power management / battery optimization](http://forum.xda-developers.com/showthread.php?t=1933615)

**At this stage, on a completely recharged battery, my Nook Simple Touch runs about two-three days as wireless display without any further intervention (other than starting up WakeTimer and Dolphin).**

