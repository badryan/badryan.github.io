---
layout: post
title: IoT book review
date: '2016-07-06 09:42:44'
tags:
- iot
- education
---

In a field like IoT the most relevant news are delivered online. But books aren't dead. Currently authoring an [IoT textbook](https://iot.ghost.io/update-higher-education-in-the-time-of-iot-june-16/) myself, I'm occasionally buying the odd IoT book to see if my own writing is vastly redundant or to provide contextual glue between more specialised works.

First off, I'm usually **not buying "hands-on" books**, i.e. tutorials how to do things. The reason for that is simple: In IoT like many other technological fields, the tools aren't static. By the time books go into print, the versions of programming languages, syntax of software libraries and APIs, and even hardware products they are recommending, are usually already outdated. Their overall recommendations might still be valid, but the latent feeling of *technical debt* remains when you're even remotely aware that there's already something better out there. That's probably a long-winded way of saying you're typically **better off asking Google for advice**, and there are a great many tutorials, code examples and videos out there that teach you how to do things.

So I'm more into books that explain concepts or define new paradigms rather than take you on tours of mouse clicks. Here are a few I've acquired over the past two years:

![](/content/images/2016/07/books.jpg)

* McEwen & Cassimally: **Designing the Internet of Things** (2014)
* Rose: **Enchanted Objects** (2014)
* Rowland et al.: **Designing Connected Products** (2015)
* Bates: **thingalytics** (2015)
* Guinard & Trifa: **building the web of things** (2016)
* Jamthe: **IoT Disruptions** (2015 - Kindle edition)

They're all rather different in what they're trying to achieve, so it doesn't make sense to interpret whatever I'm writing as a ranking between them. Rather, I'm reflecting on what I liked and didn't like, so you can make a decision for yourself.
<br>
**Designing the Internet of Things**

This book, with its own Twitter handle [@aBookofThings](https://twitter.com/aBookofThings), has been one of the first books covering the IoT from a maker and innovator perspective. I have to admit when I first bought it, I didn't like it. Most information seemed rather superficial and I couldn't quite put my finger on who their target audience was. Being a technologist, I felt the book tried to explain to me what I've already known from *spending hours and hours on the web everyday*... ...hold on, that may be the point: if you're just starting to explore the IoT and you don't have a technology background, it probably makes sense to briefly mention keywords from the world of networking, say what an Arduino and its difference to a BeagleBone is, or how crowdfunding works. Would I buy it again? No. Would I give it to a friend to see what IoT is all about? Only if they're not too geeky. Is it a waste of time? Definitely not. [McEwen](https://twitter.com/amcewen) and Cassimally have quite a few anecdotes to tell from their first steps in IoT (like, when it wasn't called IoT...), and there's the occasional informative glimpse even for routiniers.

**Enchanted Objects**

There has been a lot of hype about this book (Twitter [@enchanted_objs](https://twitter.com/enchanted_objs)) and [David Rose](https://twitter.com/davidrose) is without a doubt a MIT Media Lab IoT Technology Entrepreneur Spin Doctor (but in a good way!). This book is the essence of a few years of academic and entrepreneurial work. The message of the book is quite simple: *Don't stare at the glass slab* - i.e. try to find alternatives to the phone screen for your connected product. There are dozens of ways Rose is explaining this approach and he defines *the paradigm of enchanted objects* with many great examples how to go about the user experience challenges in IoT. The book is full of good narratives that drive this message home. It's one I've read front to back in a day, and I absolutely recommend it to anyone who's interested in IoT product design.

**Designing Connected Products**

If Enchanted Objects is the planning board, Designing Connected Products by [Rowland](https://twitter.com/clurr) is the battle field. This textbook for product designers opens with the smartest dedication of them all: to Rowland's son "*who will never know an Internet without all the Things*". Over 15 chapters this book defines what the IoT is, how designing products with a network connection is different, how products need to gracefully degrade and still be useful even if the server providing added value is no longer existent, etc etc etc. It's all about making a connected product useful and pleasant, which in turn makes the upfront work by the designer a whole lot harder. As Rowland and co-authors draw on years of experience in the real world, the book does not provide recipes but exemplifies a lot on existing products. It is also definitely worthwhile to just flick through the book and have a look at the figures - the view guided by a designer reveal more than what usually meets the eye of an amateur. Designing Connected Products is probably the most expensive book in my collection (RRP $49.99), but at 700 pages it teaches a lot of background information and delivers concrete recommendations how to go about IoT product design.

**thingalytics**

[Bates](https://twitter.com/drjohnbates) likes puns, as one can also tell by the title of his follow-up book: *thinganomics*. If you are somebody who has to sell the value of data (to a customer, to a boss), this might be your book. It's brief, it's neatly typeset, punchlines are highlighted and there are plenty of URLs that substantiate the claims. A lot of it is based on concrete examples. Read it on the flight to your board meeting, and you're all set. It also comes with a [nice website](http://www.thingalyticsbook.com), containing some up-to-date information on IoT. However, the subtitle "Smart Big Data Analytics for IoT" is slightly misleading, or at least, I don't see how the examples in the book are any smarter or the bigger from an analytical perspective than what any IoT data analytics person would do. Also, don't expect technical details in this book. It's all about the possibilities to save money through analytics, mostly in a M2M context.

**building the web of things**

This book ([@WoTbook](https://twitter.com/WoTbook)) is interesting, because at first, I didn't know what to make of it. Writing a book to push your company profile is a strategy I've seen with *thingalytics*. The book has multiple parts and shows a considerable amount of node.js code as well as hardware examples using a Raspberry Pi. [Guinard](https://twitter.com/domguinard) and [Trifa](https://twitter.com/vladounet) are founders of an IoT platform and do use *that platform* quite a bit in hands-on examples. However, this book also aims to teach some basic IoT principles and the reader gets to learn about network topologies, IoT protocols like MQTT and CoAP, or Internet security. But most importantly, they're trying to establish a paradigm which they refer to as 'web of things' - an IoT in which interoperability is a solved problem. It's especially this part where I see the biggest value of the book. If you're entering IoT as a programmer and 'service technician', your company may have a silo attitude in which things do not collaborate. The book aims to change that view. The web of things concept shows how IoT as an ecosystem of discoverable and interoperable things might work. Would I buy this book again? Maybe not (well, I would, because Dom is a very likeable guy!). Would I recommend it as a first start? Yes, to somebody who prefers a well-structured printed book over a bunch of web tutorials.

**IoT Disruptions**

This book by [Jamthe](https://twitter.com/sujamthe) is a brainstorming brought to paper. I got it on Amazon for £2, which is just about what I'd be willing to pay for a random list of IoT examples. I think it suffers from the same issues as *Designing the Internet of Things*: It doesn't go very deep, it's not very systematically compiled nor comprehensive. Unfortunately, the McEwen book has some 320 pages and gets around to mentioning quite a few things, whereas this one is also short. It's not wrong(!), but every single chapter left me with with an "...aaaaaaand?". Maybe if you're absolutely new to the field, that sort of cursory overview is useful, but if you haven't spent your time under a technological rock in the past years, you're likely in for a disappointment.