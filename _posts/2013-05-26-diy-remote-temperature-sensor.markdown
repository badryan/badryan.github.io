---
layout: post
title: DIY remote temperature sensor
date: '2013-05-26 10:07:29'
tags:
- iot
- tinkering
---


(If you’re not interested in the history and just want the technical bits, scroll down to Implementation.)

Over the past few months I have been playing with a [Raspberry Pi](http://www.raspberrypi.org) (RPi), an extremely cheap credit card-sized Linux computer (see [Do try this at home](http://iot.ghost.io/raspberry-pi-do-try-this-at-home/ "Raspberry Pi - do try this at home") for a report of my first explorations). One of my first experiments was about temperature and light level detection with an analog/digital converter connected to the RPi. My better half immediately spotted the weakness of the system: Often you’re interested in the temperature in places where you wouldn’t necessarily want to put a computer. Thanks to Google I soon discovered that radio is frequently used for communication between electronics devices and that there are a range of industry standards, for example [ZigBee](http://en.wikipedia.org/wiki/Zigbee). Amongst those ZigBee devices, the [Xbee](http://en.wikipedia.org/wiki/Xbee) has apparently become something like what Scotch Tape is for adhesive tape. Now there was a problem: I had (still have!) a smattering of electronics skills, I could just about query the [GPIO](http://en.wikipedia.org/wiki/GPIO) of the RPi, and my wife suggested me using devices that cost about £20 a pop and have a pin out not compatible to anything I had ever seen in my life. Not good.

Fast forward a handful boring seminars and Google, along with various permutations of “wireless”, “Raspberry Pi”, “cheap Xbee”, “remote sensor RPi” etc, and I had discovered the [XRF](http://shop.ciseco.co.uk/xrf-wireless-rf-radio-uart-rs232-serial-data-module-xbee-shape-arduino-pic-etc/) from [Ciseco](http://shop.ciseco.co.uk). Each XRF radio module comes for about £10, which I found affordable enough for a potentially failing experiment, they offer a [shield for the Raspberry Pi](http://shop.ciseco.co.uk/slice-of-pi-add-on-for-raspberry-pi/) to mount the radio (£4), and a [little search](http://bit.ly/12UIJtf) convinced me that some people must have succeeded with this before. Now what to do?

Thankfully, virologist [Peter Balfe](http://hcvpi.bham.ac.uk) at the University of Birmingham had discovered the RPi and the XRF modules about a year before me, and a put a website up that describes how he is using them for [freezer monitoring](http://hcvpi.bham.ac.uk/Freezer.html) where the temperature is sent to the RPi and rendered into a graph on the web. In other words: He’s sticking them into a -80 degree environment, and they still seem to work. If you think a little bit about that, you probably realise the potential of remote monitoring and the great many applications in your own lab, for very little money. For the freezer application, Peter had been using a thermistor (a temperature-dependent resistor), and if you know electronics, you realise that his sensor is worth less than a mere pound. Again, Ciseco have a useful range of products, and for £7 you get a platform to put any analog sensor into a [little battery-powered box](http://shop.ciseco.co.uk/analog-to-digital-xrf-development-sensor-12bit-adc/) and have it talk to your RPi. In theory a RPi base station can cater for several dozen sensors, as long as their is no cold room in the “line of sight” between the sensor and the receiver. Just looking at the price range of many analog sensors, one can be looking at a total sensor price based on: thermistors for low-temperature, e.g. -80C: Â£30; calibrated thermometers -30C to 125C: ~£21; light sensor: ~£19; water detector: ~£22; movement sensor: ~£19, or even air-pressure or detection of various gases for just a few pounds more.

A few weeks ago that was all Greek to me. Peter has put a very helpful [PDF with his building instructions online](http://hcvpi.bham.ac.uk/Publications/PDFs/Freezer.pdf), but in the meantime a few things had changed and I ran into a few unexpected problems, and so I’m putting my guide for fellow researchers here.

**Implementation**

Requirements: Basic soldering skills and a rough idea what the individual components are doing for assembling the hardware, reasonable Unix and scripting skills to programme the XRF and present the data on the RPi.

Shopping list for a freezer monitor: Assuming that you already have a RPi, you can get most of the rest from Ciseco ([thermistor kit](http://shop.ciseco.co.uk/temperature-xrf-development-sensor-thermistor/), [XRF](http://shop.ciseco.co.uk/xrf-wireless-rf-radio-uart-rs232-serial-data-module-xbee-shape-arduino-pic-etc/) for the RPi, [Slice of Pi](http://shop.ciseco.co.uk/slice-of-pi-add-on-for-raspberry-pi/) to mount it). Various other bits include a [2 AA battery box](http://www.maplin.co.uk/aa-size-battery-holders-31427), a [battery snap](http://www.maplin.co.uk/pp3-type-battery-snap-44392), a pair of Energizer Ultimate Lithium AAs (they have a rather steep price but don’t freeze at -80 degrees), and I personally recommend a [Glenfiddich Taster Pack](http://www.tesco.com/groceries/Product/Details/?id=268439451) for various reasons. So without the RPi and the booze, you’re looking at about £40 including your first set of batteries.

A slight warning: Ciseco is a small company run by enthusiasts, and they themselves say that they’re engineers, not writers. If you run into any problems, it’s probably best to discuss it in their [Support Forum](http://openmicros.org/index.php/component/kunena/10-ciseco-support?Itemid=0) rather than spending endless hours searching for the non-existent documentation.

![](/content/images/2015/09/thermistor-1.jpg)

**Step 1:** Build your Slice of Pi. So starting with the green board and the black headers, you build according to this [picture](http://openmicros.org/index.php/articles/94-ciseco-product-documentation/raspberry-pi/227-slice-of-pi).5-10min.

**Step 2:** Build your Thermistor box following a [pictorial guide](http://www.openmicros.org/index.php/articles/88-ciseco-product-documentation/211-ccb-coin-cell-board-pictorial-build-guide). Note that instead of the LDR, you would solder on the thermistor, and in my case, the surface mount 10k resistor was a standard 10k with wires. You don’t need the coin battery, but instead you solder the battery snap to the terminal near the capacitor (red goes to 3V3, black goes to GND). Don’t slot your batteries in as yet, first programme the XRF to be in analog mode with a reasonable sleep cycle (more about that later). 10-20min.

**Step 3:** Congratulate yourself to finishing off the soldering part of the project and have a bottle of your Glenfiddich Taster Pack. Keep the round package of the bottle. You will use it as a case for your freezer sensor.

**Step 4:** Mount a XRF on the Slice of Pi and stick it onto the RPi. Before that, you should already disable the default output from Debian to your serial port by editing cmdline.txt in /boot and remove any reference to ttyAMA0, and also comment out T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100 in /etc/inittab as indicated e.g. [here](http://www.irrational.net/2012/04/19/using-the-raspberry-pis-serial-port/), at [Ciseco](http://openmicros.org/index.php/articles/94-ciseco-product-documentation/raspberry-pi/283-setting-up-my-raspberry-pi) or in Peter’s document. I’ve had some technical problems and realised that the widely used webiopi demon interferes with the serial port, so you have to disable that as well in case you’ve installed it.

Step 5. Give your XRF a personality. By default all the XRFs act as pass-through devices, i.e. they can receive and send information over the serial port and use [AT commands](http://en.wikipedia.org/wiki/AT_command). The XRF that’s going into your freezer needs to get “analog personality”, which means that the XRF will periodically read the voltage from the thermistor and send that value to the XRF on the RPi.

This requires a firmware update and, if things go wrong, you can end up in a [world of pain](http://openmicros.org/index.php/component/kunena/10-ciseco-support/4683-xrf-on-slice-of-pi-not-responding?Itemid=0). However, they give you a rather good description of the [firmware process using the RPi](http://openmicros.org/index.php/articles/84-xrf-basics/215-xrf-firmware-upload-with-a-raspberry-pi). Everything you need is on GitHub, the [xrf_uploader](https://github.com/CisecoPlc/XRF-Uploader) and the most recent of the llapAnalog*.bin from the [firmware folder](https://github.com/CisecoPlc/XRF-Firmware-downloads/tree/master/XRF-LLAP). Care should be taken about the line feed issue. I recommend to do a test run without the XRF mounted on the Slice of Pi. If the xrf_uploader says something along the lines of “0 lines read”, you’re likely having issues and that would send your XRF into trouble (see above ‘world of pain’). If you’re seeing “xx lines read” (xx being >> 0), the xrf_upload will of course fail without an XRF, but you should be save for the real thing. 1-2hrs.

**Step 6:** Learn LLAP; name your XRF and send it to sleep. [LLAP](http://openmicros.org/index.php/articles/85-llap-lightweight-local-automation-protocol/101-llap-starter) (and [here](http://openmicros.org/index.php/articles/85-llap-lightweight-local-automation-protocol/112-llap)) is a light-weight protocol for the communication between your XRF devices. For example, once everything is up and running, the XRF in the freezer will regularly send something like “aX1ANA1234–”, which means the sensor with the name X1 has a reading of 1234 on his analog-digital converter. You can read this message with your XRF on the RPi using either a normal terminal program or a custom-written script, which then takes care of the rest like creating nice graphs. Depending on the personality of your XRF, there are [additional LLAP commands](http://openmicros.org/index.php/articles/87-llap-lightweight-local-automation-protocol/llap-devices-commands-and-instructions) the XRF will understand. (Note that this is where it’s useful to have a look at the [pin layout and firmware functions](http://openmicros.org/index.php/articles/87-llap-lightweight-local-automation-protocol/llap-devices-commands-and-instructions/190-llap-device-xrf-pinout) of the XRF – in more complex scenarios the XRF is well capable of reading different analog and digital sensors, and outputting voltage on specific pins for hardware to react at the remote site).

In contrast to Peter who chose to do everything programmatically, I installed minicom as terminal program and configured my XRF by copying LLAP commands into the console. Note that LLAP expects the full command to arrive at the XRF within a few milliseconds, so typing them doesn’t cut the mustard. Type your commands in a separate editor and then copy them across. See here for [installation and configuration of minicom](http://openmicros.org/index.php/articles/94-ciseco-product-documentation/raspberry-pi/283-setting-up-my-raspberry-pi). Add automatic line breaks, echo and wrapping for better readability.

I issued: a--CHDEVIDX1 (renames the XRF from it’s default name — to X1), aa--REBOOT-- (to reboot and save the name), aX1WAKE--, aX1INTVL030M, aX1CYCLE-- (these commands configure the XRF to wake up every 30 min to take a measurement, send it, and go back to sleep again). Once that’s finished, you can stick your XRF onto the thermistor board, put in the batteries, and mount them into the whiskey box.

Note that it can be tricky to reconfigure your XRF once it’s in sleep mode. The device sends it’s battery status every 10th cycle (so approximately every 5 hours) and you have about 100 ms to tell it it’s new cycling interval. I recommend the code in Peter Balfe’s writeup for a strategy how to deal with it.

**Step 7:** Mount your other XRF on the Slice of Pi.

**Step 8:** Listen. If you leave minicom open, you will see messages with the substring ANA come in about every 30 min. For room-temperature measurements and with the thermistor firmware (which exists), we would receive the actual temperature, but in our case, calibration is needed. Get the values at 4, -20 and -80 degrees to see what the effect of the cold is on your thermistor reading. I used this for a polynomial fit to approximate the temperature.

**Step 9:** Write some code to do stuff with your readings. This is where your creativity comes in. Again, Peter has a few interesting features in his solution. I only found that the messages from my remote XRF didn’t come in convenient 12 byte packages when I listen to the serial port using inWaiting() from the serial module in Python, but sometimes would break LLAP messages into random fragments. That’s clearly an issue with how the function is triggered. I introduced a
```
len = ser.inWaiting()  
  if len == 12 or len == 24 or len == 36 :  
  msg = ser.read(ser.inWaiting())
```
and that seems to capture the messages appropriately.

I may put some example code up once I’m happy with my functionality.

 

Final note: -80 degrees is bloody cold, and although Nasa has a requirement for batteries not to freeze at that temperature, the stuff you get in normal consumer markets isn’t totally up for that. The Energizer Ultimate Lithium batteries dropped from 3.6V to 2.8V within minutes of putting them into the freezer. The continuously froze and lost another 0.03V every further 5 hrs. In the meantime Peter sent me a chart with his battery readings, and they seem to stabilise around 2.15V and stay there for a few months of monitoring.

