---
layout: post
title: "RWDPerf, respimage"
author: "Alex Young"
image: "/images/posts/rwdperf.png"
categories:
- modules
- libraries
- responsive
- mobile
---

###RWDPerf

![RWDPerf report](/images/posts/rwdperf.png)

RWDPerf (GitHub: [lafikl / RWDPerf](https://github.com/lafikl/RWDPerf), License: _MIT_, npm: [rwdperf](https://www.npmjs.org/package/rwdperf)) by Khalid Lafi is a tool for analysing responsive pages.  It calculates the page weight, so you can see what the download bloat is like.

It works using Chrome's remote debugging API, so it should be more accurate than a DOM simulation.  It accepts arguments on the command-line for configuring things like device scale factor, width, height, and user agent.

It also has an API, which is ideal for dropping it into a build script.

###respimage

If RWDPerf indicates that your page has a lot of unused images, then you might want a better responsive image replacement library.  Respimage (GitHub: [aFarkas / respimage](https://github.com/aFarkas/respimage), License: _MIT_) by Alexander Farkas is a responsive image polyfill for `picture` and `srcset`.

Respimage works using the `picture` element or the `srcset` image attribute.  The `srcset` implementation supports descriptors for width and density.

There's also a JavaScript API, so you can also support dynamically generated content.
