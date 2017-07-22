---
layout: post
title: Another big donation from ARM
date: '2014-07-09 09:34:41'
tags:
- hardware
- education
---

![](/content/images/2015/09/photo-300x224.jpg)

The Game-of-Life is an example of cellular automata, a conceptual framework that is inspired by the interaction of living cells in a confined space over time. Computer science students learn about Conway’s classic game because it teaches them about Turing completeness, biology students may learn about it as an introduction into discrete stochastic simulations.

We’ve previously used a Game-of-Life implementation on KL25Z microcontrollers (another [donation from the ARM University Programme](https://iot.ghost.io/donation-from-arm/) to provide a more haptic way for students to explore the properties of the game world. Each controller represents a cell whose survival is dependent on the neighbouring devices. However, for technical reasons the implementation relies on a serial ring bus to enable communication between the boards, which is very distinct from biological systems where all cells are in immediate contact with their neighbours.

We discussed this with the ARM University Programme, who suggested the use of wireless radio technology to communicate between our “cells”. Bluetooth Low Energy (BLE) is such an approach, and the Nordic nRF51822 mbed Kit is a low-power Cortex M0-controller with BLE on board. After a few emails with ARM, we’re now in a position to explore the properties of concurrent dynamic systems and compare them to the behaviour of living cells: A great learning experience for technical people and life scientists alike!

