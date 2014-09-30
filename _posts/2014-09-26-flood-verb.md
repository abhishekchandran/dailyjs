---
layout: post
title: "verb: A CAD Library for the Web"
author: "Alex Young"
categories:
- webgl
- graphics
- libraries
- modules
---

 Peter Boyer shared two modules related to 3D graphics: [Flood](http://www.floodeditor.com), a visual programming language, and [verb](http://verbnurbs.com/), a library for working with NURBS surfaces.

Flood (GitHub: [pboyer / flood](https://github.com/pboyer/flood), License: _MIT_) behaves a bit like a 3D modelling application.  It uses a Scheme interpreter that's written with JavaScript, with immutable data and first order functions.

The beta application allows you to sign in with a Flood account, Google+, or Facebook.  You can add nodes that perform arithmetical operations, shapes, and even functions.

![Flood](/images/posts/floodeditor.png)

It's built with Grunt and Bower, and uses libraries like three.js and Bootstrap.

Peter's other project is verb (GitHub: [pboyer / verb](https://github.com/pboyer/verb), License: _MIT_), a library for creating and manipulating NURBS surfaces.  It works with browsers and Node and supports advanced tools like derivative evaluation, adaptive tessellation, and intersection.

[The examples](http://verbnurbs.com/geometry.html) include things like arcs, Béziers curves, and various extrusions.  You can rotate the examples if you click and drag.

NURBS are used in CAD, I don't think they're particularly popular for game graphics, so presumably Peter intends to use this with the Flood project.

