---
layout: post
title: On-the-fly GPS visualisation through Node-RED
date: '2014-04-14 10:22:29'
tags:
- tinkering
- node-red
---

![](/content/images/2015/09/arfmap.jpg)

After I’ve had [@ceejay](https://twitter.com/ceejay) and [@hardware_hacks](https://twitter.com/Hardware_Hacks) send me code examples for putting geographical coordinates onto [Open Street Maps](http://www.openstreetmap.org) or [Google Maps](https://maps.google.com), I feel I should at least publicly document how I’ve gone about it in the end.

I’m receiving JSON sentences through a serial-in node in [Node-RED](http://nodered.org). These are already well formatted an look like *{“lat”:”0.18544534″,”lon”:”52.343545″}* when I receive them. The serial-in is connected to a websocket-out node. Here I set a path */admin/ws/map*, as I’ve learned from code from both CJ and Chris.

Both of them put flags on distinct positions of the map (CJ had sent me code for OSM and Chris for Google Maps). However, for my application, I wanted to express a percentage of data points in a particular perimeter. On the search for a suitable set of [leaflet.js](http://leafletjs.com) commands (a framework recommended by CJ), I stumbled across [heatmap.js](http://www.patrick-wied.at/static/heatmapjs/), a framework that does all the hard work for you. In particular, their heatmap object (which can deal with cartesian and geographical coordinates!) has a persistent data store, that is, you can continously push new coordinates into it and it takes care of the relative frequency and visualisation of the same all by itself. In my case, I used the example *heatmap.js-master/demo/maps_heatmap_layer/gmaps.html*, which one can [load from Github](https://github.com/pa7/heatmap.js/archive/master.zip).

I stripped most of the example and the gist is about 150 lines of well spaced HTML/JavaScript, most of which deals with loading appropriate online and offline libraries (see here for [an example](http://www.patrick-wied.at/static/heatmapjs/example-heatmap-googlemaps.html)). Along with yout HTML file, you just need to add two libraries *heatmap-gmaps.js* and *heatmap.js* into your web directory. Thanks to CJ and Chris I knew the JavaScript needed to connect from the HTML page to the websocket created in Node-RED. I promised CJ not to share his under-development code, you may want to have a look at Chris’ [Node-RED example that he’s put online](http://flows.nodered.org/flow/1aab1d44e387da96b3fe). In the context of the *gmaps.html.* The actual “putting a point onto the map” is then just the following:

```
ws.onmessage = function (evt) { try { var data = JSON.parse(evt.data); heatmap.addDataPoint(data.lat,data.lon,1); }
```
and all the magic happens automatically, as shown in the teaser image.


