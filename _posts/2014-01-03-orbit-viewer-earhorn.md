
---
layout: post
title: "Orbit Viewer, Earhorn"
author: Alex Young
categories:
- webgl
- space
- instrumentation
- debugging
---

###Orbit Viewer

![Orbit Viewer](/images/posts/orbitviewer.png)

[Orbit Viewer](http://orbits.wthr.us/) is a [Chrome Experiment](http://www.chromeexperiments.com/detail/orbit-viewer/?f=webgl) by Kevin Gill that helps visualise the orbits of comets and satellites.  You can watch the famous comet Shoemaker–Levy 9, or see the current position of the International Space Station.  It should work with most WebGL capable browsers.

> A sort of "Where are they now" for spacecraft and comets: Check out realtime positions, along with historical and projected flight paths of our solar system's trailblazing spacecraft and comets. All in a zoomable/rotatable 3D interface. Using historical and real-time trajectory information for NASA's JPL Horizons system, and in-browser WebGL and Three.js rendering.

###Earhorn

Earhorn (GitHub: [omphalos / earhorn](https://github.com/omphalos/earhorn), License: _MIT_) by "omphalos" is a library for instrumenting JavaScript.  You pass `earhorn$` a label and a function, and then you can view the function as the values change.

The [mouse example](http://omphalos.github.io/earhorn/index.html#/iframe=examples/mouse.html) shows how this works: the source for a jQuery `mousemove` listener is displayed, and whenever you move the mouse the integer values for the current coordinates will be reflected in real time.

An iframe is used that loads the `earhorn/index.html` page which knows how to display an instrumented version of the function.  Internally, Earhorn uses [Esprima](http://esprima.org/) to generate an abstract syntax tree that is manipulated to allow the code to be observed.

It reminds me a little bit of the [Watches feature in Light Table](http://www.chris-granger.com/2013/08/22/light-table-050/), and some of the recent improvements to WebKit Inspector.
