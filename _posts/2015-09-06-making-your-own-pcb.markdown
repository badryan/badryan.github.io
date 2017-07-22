---
layout: post
title: Making your own Printed Circuit Board
date: '2015-09-06 18:43:17'
tags:
- tinkering
- hardware
---

[CamJam](http://www.camjam.me) organiser [Michael Horne](https://twitter.com/recantha) is known for his Raspberry Pi-based tri-corder like [PiPod](http://www.recantha.co.uk/blog/?p=2663). In the most simple terms, it is a collection of a few environmental sensors and a retro-looking LCD display in a stylish Lego case - for Michael it was a learning journey into using active and passive electronic components. As he was way ahead of me when I first touched the Raspberry Pi GPIO pins, I was very surprised when he recently mentioned that he would like to do a PCB for the PiCorder, but feared time, effort and cost.


### It is not difficult to make a simple PCB
I received a lot of encouragement from [Andrew Lindsay](https://twitter.com/andrewdlindsay) and [Mark Setrem](https://twitter.com/ukmoose) when I first toyed with the idea of making a PCB; mostly because they've already successfully done it a couple of times, whereas I felt I had too little knowledge of electronics, no experience in circuit design, a fear of spilling corrosive substances on our living room table and other potential sinks of money.

<br>
**_Don't fear!_**  is all I can say.
<br><br>

* Fear #1: *I don't know enough electronics.*
Well. Maybe. We all live and learn. Building hardware is a bit like programming. In the beginning getting a few conditionals right seems like a huge challenge, but after two or three projects putting an additional capacitor in to give your circuit a bit more breathing space seems natural. I'm not saying we don't need university-trained electrical engineers (quite the opposite!), but: **If you can build a functional circuit on a breadboard, you have sufficient knowledge to make a PCB**.

* Fear #2: *I'm not very good with chemicals.* or *The tools are so expensive.*
That's fine. You don't need to buy anything. The times of etching are over, unless you really want to. These days, there are plenty of "board houses" that happily turn your digital designs into small slabs of plastic and copper. And, depending on your requirements of size, quality, and speed of delivery, UK manufacturer [Ragworm](http://www.ragworm.eu) would charge you £10 for a single 40x40mm PCB and 2 weeks turnaround, whereas China-based consortium [DirtyPCBs](http://dirtypcbs.com) will send you 8-12 50x50mm PCBs for the same price if you're happy to wait up to 2 months. Personally, I quite enjoy pushing components around on my designs just for saving a millimetre or two to get into a lower price tier.

* Fear #3: *PCB design software is awfully complex!*
True, but for most hobby projects, you can ignore about 90% of the functions and concentrate on your actual design. Think how much of your word processing software you're actually using!


### PCB design in ten simple steps
First, I should say that I do only have experience with [EAGLE](http://www.cadsoftusa.com/download-eagle/). It is free for hobbyists, runs under all major operating systems and EAGLE formats (both for inputting components and for outputting the design for the board house) are very common.

Some say with a bit of *Google foo* you won't need a book, but I found [*Make Your Own PCBs with EAGLE*](http://www.amazon.co.uk/Make-Your-Own-PCBs-Eagle/dp/0071819258/) by Simon Monk a very good introduction. The one QuickStart chapter with 20 pages was effectively all I needed to find my way around.
<br>
A typical workflow in EAGLE works like this:

1. Draw a **schematic** with parts from a **library of components**. (These a numerous, and if the default set of components isn't enough for you, you can download *.lbr files* e.g. from [Sparkfun](https://github.com/sparkfun/SparkFun-Eagle-Libraries) and [Adafruit](https://github.com/adafruit/Adafruit-Eagle-Library), or even draw your own). Component is a very general term here, the library contains everything but the kitchen sink. A resistor and an Intel 80286 anyone?
2. In most cases, you're going to place components like you would in a vector drawing program, with tools like move, copy and rotate. If the components are well annotated, you'll see labels on the terminals, so it's immediately obvious which bit is Vdd, ground, etc. You would then **draw electrical connections** between the components.
3. There are tools to organise many connections in a bus, or to clarify (to yourself and the auto-router) which wires simply cross each other and which ones are electrically connected in **junctions**. (You'll see *junction* and *bus* is actual terminology in the GUI. I'd say it's pretty intuitive.)
4. Once you're finished drawing the circuit, you'd switch to the **board view**.
5. In the beginning all components (with their relative sizes) are bunched together in a corner of your PCB. Your job is to move them around, aiming to **place the components somewhere sensible**, just as you would on a breadboard (e.g. power jack and temperature sensor at an edge, integrated circuits more central...). At that stage it's also important to keep in mind that, in contrast to jumper wires that can go all criss-cross, in most cases you are only going to have two layers available on a PCB. Situations that require electrical connections in more layers cost effort (or money). That's why it's easiest to have ICs with many connections more central than e.g. a simple diode.
6. The theoretical connections between components are called **air wires**, and you want to replace them with actual **routes** ("tracks") either on the top or bottom copper layer of your PCB. You can either do this manually, but although it is considered poor sportsmanship by some, use the **auto-router** tool. (Yes, I auto-route!).
7. Go back to 6. No, seriously. First time around was just proof-of-concept, but what you really want to aim for is a **mass ground fill** (say, of the bottom layer), and most other connections on the top layer. I can only hint here that it involves the polygon drawing tool and renaming its signal to GND. (I think I watched a video first time around. Google foo...).
8. Once you like the look of your board, invoke the **CAM processor**. I guess the name comes from photolithography, and that's suitable as we're now about to "print" the PCB to **[Gerber files](https://en.wikipedia.org/wiki/Gerber_format)** needed for tooling at the board house. (Another note: There are tools like **electrical check** and **design rule check** that are recommended to run before making the Gerbers, but I found manual checking-and-double-checking a lot more insightful for smaller projects).
9. You have to **load a *.cam* job**, which is the board house's description which layers of the PCB refer to which layer in their production line. Aforemenntioned Ragworm [adhere to a default file](http://www.ragworm.eu/rock-pool/article/exporting-eagle-files-to-gerbers), while DirtPCBs have their [own recipe](http://dirtypcbs.com/dirt_cheap_dirty_boards.v1.cam).
10. Zip your Gerber files and your EAGLE .sch and .brd files, and **upload your project to the board house**.

Once you have a bit of practise, steps 6-9 are really only going to take you a few minutes. In the worst case, you've wasted £10. But that only happened to me once since started doing PCBs, and it was a (my!) circuit design issue, nothing that's intrinsic to PCB production.
<br>
Go have fun!