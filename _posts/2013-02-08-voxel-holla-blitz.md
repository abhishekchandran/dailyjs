---
layout: post
title: "voxel.js, holla, Blitz, OneJS 2.0"
author: "Alex Young"
categories: 
- graphics
- games
- webrtc
- WebSocket
- frameworks
- modules
---

###voxel.js

![voxel.js](/images/posts/voxeljs.png)

When I was at [BathCamp](http://bathcamp.org/) this week, Andrew Nesbitt mentioned [voxel.js](http://voxeljs.com/) -- a collection of projects for building browser-based 3D games.  The core components were written by Max Ogden and James Halliday, take a look at voxel-engine (GitHub: [maxogden / voxel-engine](https://github.com/maxogden/voxel-engine#api), License: _BSD_, npm: [voxel-engine](https://npmjs.org/package/voxel-engine)) if you want to see some code examples.

There are lots of [demos on the voxel.js site](http://voxeljs.com/#gallery), at the moment most of them support simple world traversal and the removal of blocks just like Minecraft.  The project also has add-ons which includes [voxel-creature](http://voxeljs.com/#gallery) for adding NPCs and [player-physics](https://github.com/maxogden/player-physics).  A huge amount of effort has already gone into the project, and it was apparently inspired by the awesome [0 FPS blog posts about voxels](http://0fps.wordpress.com/2012/07/07/meshing-minecraft-part-2/).

###holla

holla (GitHub: [wearefractal / holla](https://github.com/wearefractal/holla), License: _MIT_, npm: [holla](https://npmjs.org/package/holla)) from Fractal is a module for [WebRTC](http://www.webrtc.org/) signalling.  The author calls it "WebRTC sugar" -- compared to the underlying API the library's use of methods like `.pipe` make it a lot easier to get the hang of.

It has some helpers for creating audio and video streams, and there's a demo up at [holla.jit.su](http://holla.jit.su/) that accesses your webcam and microphone.

###Blitz

Blitz (GitHub: [Blitz](https://github.com/EliSnow/Blitz), License: _Modified MIT_) by Eli Snow can help safely extend objects, overload functions based on types and arguments, and provides some native type recognition across global contexts:

> Unlike other frameworks that have one generic wrapper for every object, Blitz creates unique wrappers for every prototype. So, for example, instead of having one method `replace` that works only with `Arrays` we can have a `replace` method for `Arrays` another for `HTMLElements` and/or any other object type.

Some of the functionality is accessible through a chainable API, so you can do things like this:

{% highlight javascript %}
// [35, 16]
blitz([35, 16, 21, 9]).length(2).value;
{% endhighlight %}

Function overloading works using `blitz.overload`, which accepts an object that lists types alongside target functions.

###OneJS 2.0

Azer Koculu has updated [OneJS](https://github.com/azer/onejs) to version 2.0.  OneJS converts CommonJS modules to standalone, browser-compatible files.  It now supports splitting bundles into multiple files, and loading them asynchronously.  It also has a more flexible build system: you can use it from the command-line, package.json, or from within a Node script.

