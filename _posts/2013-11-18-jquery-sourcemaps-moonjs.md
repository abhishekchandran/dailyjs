---
layout: post
title: "Moonjs, jQuery Removes Sourcemap Comments"
author: Alex Young
categories:
- jquery
- space
- simulation
---

###Moonjs

[Moonjs](http://svtsim.com/moonjs/agc.html) (GitHub: [siravan / moonjs](https://github.com/siravan/moonjs), License: _GPL_) by Shahriar Iravanian is a port of the Apollo Guidance Computer using Emscripten.

> AGC was the main computer system of the Apollo program that successfully landed 12 astronauts on Moon. There was one AGC on each of the Apollo Command Modules and another one on each Lunar Module. There was also a second backup computer system called Abort Guidance System (AGS) on the Lunar Modules, which is simulated by Virtual AGC, but not the current version of Moonjs.

> Recent advances in the JavaScript language - such as optimized engines, ahead-of-time (AOT) compilation, and asm.js - make it possible to write computationally extensive applications in JavaScript. My previous experience with online JavaScript-based simulation (svtsim and hemosim) was very positive and convinced me of the suitability of the HTML5/JavaScript combination in writing portable, easy-to-use simulators.

I was going to try figuring it out, but it reminded me of [Kerbal Space Program](https://kerbalspaceprogram.com/) and I got distracted...

###jQuery 1.11.0/2.1.0

[jQuery 1.11.0/2.1.0 Beta 2 were released last week](http://blog.jquery.com/2013/11/15/jquery-1-11-02-1-0-beta-2-released/).  The beta includes AMD support, which is still the headline feature.

Something that I found interesting was the removal of the sourcemap comment:

> One of the changes we've made in this beta is to remove the sourcemap comment. Sourcemaps have proven to be a very problematic and puzzling thing to developers, generating scores of confused questions on forums like StackOverflow and causing users to think jQuery itself was broken.

> We'll still be generating and distributing sourcemaps, but you will need to add the appropriate sourcemap comment at the end of the minified file if the browser does not support manually associating map files (currently, none do). If you generate your own jQuery file using the custom build process, the sourcemap comment will be present in the minified file and the map is generated; you can either leave it in and use sourcemaps or edit it out and ignore the map file entirely.

That fact sourcemaps generate so much confusion is worth thinking about, because it's one of those things that people cite as making compile-to-JavaScript languages easier to work with.
