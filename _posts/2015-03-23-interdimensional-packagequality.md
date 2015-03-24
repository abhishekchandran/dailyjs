---
layout: post
title: "Interdimensional, Package Quality"
author: Alex Young
image: "/images/posts/packagequality.png"
categories:
- touchscreen
- mobile
- npm
- modules
---

###Interdimensional

[Interdimensional](http://vodkabears.github.io/interdimensional/) (GitHub: [vodkabears/Interdimensional](https://github.com/vodkabears/Interdimensional/), License: _MIT_, npm: [interdimensional](https://www.npmjs.com/package/interdimensional), Bower: `interdimensional`) by Ilya Makarov is a library for responding to gyroscope events on devices that support the `deviceorientation` event.  The [demo site](http://vodkabears.github.io/interdimensional/) will start responding to tilts when you tap the polygon icon at the bottom-left of the screen.

The library's behaviour can be tweaked by changing the `PPD` option (pixels per difference between tilts), and there's also an `insensitivity` option for the minimum difference between tilts.

To start using spatial scrolling, call `Interdimensional.charge`.  The library will emit events on the `document` object, so you can detect when the feature is enabled (`interdimensional:charge`), and if it wasn't possible to enable it (`interdimensional:fail`).

###Package Quality

![Package Quality](/images/posts/packagequality.png)

[Package Quality](http://packagequality.com) by Alex Fernández is a service that evaluates npm packages based on npm and GitHub metrics.  It's ideal if you want to quickly compare several competing packages.

The source is on GitHub ([alexfernandez/package-quality](https://github.com/alexfernandez/package-quality)) and the project is written with Express and MongoDB.  The readme for the project has more details about how package quality is determined.  The authors admit that any such measurements are potentially problematic, but they explain how version, downloads, and repo quality is measured so you can see what the numbers really mean.
