---
layout: post
title: A user perspective on Eclipse IoT
date: '2016-04-02 12:01:43'
tags:
- iot
- software
---

A few weeks ago I spoke at the [Eclipse User Group](http://www.meetup.com/London-Eclipse-User-Group/) in London about the offerings the Eclipse Foundation has around open source IoT software. It was an interesting event with a very diverse set of speakers, ranging from geographic information systems to edu-tech and open source advocacy. Organizer [Tracy Miranda](https://twitter.com/tracymiranda) wrote up a very nice [summary of the **#eclipseldn** event on her website](http://kichwacoders.com/2016/03/24/eclipse-converge/).

Under the organisational lead of [Ian Skerrett](https://twitter.com/IanSkerrett) and [Benjamin Cabé](https://twitter.com/kartben), one of the seven main working groups is **[Eclipse IoT](http://iot.eclipse.org)**. This is probably a good moment to explain to the uninitiated reader that *Eclipse* simply used to be an open source integrated development environment for Java (and still is: [download the IDE](https://www.eclipse.org/downloads/)), but over the past almost fifteen years has restructured into a foundation that works language-agnostic on a wide range of projects; very much like *Apache* used to be a web server and now is a software foundation. Eclipse IoT is an umbrella project that coordinates the work of developers that are primarily based at a dozen companies with an interested in IoT or M2M. Amongst those are major players such as IBM, Bosch and Siemens, but also smaller companies that work in particular corners of the IoT, like dc-square and openHAB.

I set out to give an overview when and where particular Eclipse IoT projects can help to build IoT solutions. While it's possible to find all that information in a [table on the Eclipse website](http://iot.eclipse.org/projects), it can be daunting if you're just getting started on an IoT project to understand what you need and where it fits. Good time to let my artistic streak come through:

![](/content/images/2016/04/slide4.png)

One can think about the various Eclipse IoT projects in terms of **ecosystems, standards and components**. On the ecosystem level, Eclipse acts as integrator for projects that are required to build a complete end-to-end solution, starting from embedded code on microcontrollers to message brokers on gateways to backend software.

<br>
I demonstrated one possible scenario how the **ecosystem** bit helps designing M2M/IoT using this schematic around end device management:
![](/content/images/2016/04/slide6.png)

The [Vorto](http://www.eclipse.org/vorto/index.html) GUI allows one to provide language-independent descriptions of devices, which via the Vorto code generators can be conveniently translated into objects/classes in any programming language for which such generator exists. (See my [recent blog post about Vorto](/2016/03/11/hands-on-with-vorto-iot-information-models.html)). On a very abstract level, a programmer could refer to "the radio" and "send x bytes" in their code, an interface presented by the [EDJE](https://projects.eclipse.org/proposals/edje) hardware abstraction layer that takes care of the technical differences between various devices. Once developed, one can deploy the new code via [hawkBIT](https://projects.eclipse.org/proposals/hawkbit) to a large number of devices at once. As such, hawkBIT reminds me of resin.io, which I [wrote about earlier](/2015/09/14/deploying-raspberry-pi-images-at-scale.markdown). On the device itself then, the [Concierge](https://projects.eclipse.org/projects/rt.concierge) system is a small footprint Java core that would run that code.

<br>
On the **component level**, [Eclipse Kura](http://www.eclipse.org/kura/) deserves a very honourable mention in the very long list of projects that can simply be deployed in one own's IoT solutions. Kura is an easy-to-use gateway system that acts between sensor devices and a backend. Traditionally used for demonstrations on a Raspberry Pi, Kura and Pi now almost always go together, with e.g. the [openHAB](http://www.openhab.org) being widely used by hobbyists for home automation on the Pi.

<br>
While it is always possible to drill into the actual code of Eclipse projects (open source, *sic!*), both on the ecosystem and the component level one doesn't necessarily have to engage with the nitty-gritty of the underlying code. However, as Eclipse IoT also embraces important **standards**, their libraries for M2M/IoT device communication via MQTT or CoAP are extremely powerful.

![](/content/images/2016/04/slide5.png)

In my presentation I focussed on the explanation of MQTT as a very common protocol to send information from devices to gateways to servers. While the [Mosquitto broker](http://mosquitto.org) (another 'component') takes care of all of the message handling, the programmer only needs to memorise a few lines of syntax of e.g. the [Paho library](https://www.eclipse.org/paho/) to connect to the broker or react to particular MQTT topics via callback functions.

<br>
I concluded my talk with a wishlist for Eclipse IoT: We need a project for data analytics and visual data representation. However, I had missed that the Eclipse had just embraced the [Open Analytics project](http://www.openanalytics.eu/architect) a few days earlier... The complete slides are available on [SlideShare](http://www.slideshare.net/BorisAdryan/eclipse-iot-ecosystem).