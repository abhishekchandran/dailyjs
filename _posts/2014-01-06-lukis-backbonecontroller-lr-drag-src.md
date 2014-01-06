---
layout: post
title: "Lukis, Backbone.Controller, lrDragNDrop"
author: Alex Young
categories:
- node
- modules
- testing
- types
---

###Lukis

[Lukis](http://keripix.github.io/lukis/build/index.html) (GitHub: [keripix / lukis](https://github.com/keripix/lukis), License: _MIT_) by Keripix is an experimental image editor, built with Twitter's [Flight](http://twitter.github.io/flight/) and [Fabric.js](http://fabricjs.com/).

It's event driven, so each main drawing component is nicely decoupled.  This is based on Flight's API, where behavior is mapped to DOM nodes.

###Backbone.Controller

Backbone.Controller (GitHub: [artyomtrityak / backbone.controller](https://github.com/artyomtrityak/backbone.controller), License: _MIT_) by Artyom Trityak is a Backbone controller that supports declarative routes.  It makes Backbone feel more like traditional MVC, which may appeal to you if you're brainwashed by other MVC frameworks.

Artyom has included some documentation showing how to bind routes using `Backbone.Controller.extend`, and there's also a RequireJS AMD snippet so you can get started quickly.

###lrDragNDrop

[lrDragNDrop](http://lorenzofox3.github.io/lrDragNDrop/) (GitHub: [lorenzofox3 / lrDragNDrop](https://github.com/lorenzofox3/lrDragNDrop), License: _MIT_) by Laurent Renard is an AngularJS module for managing collections of items using drag and drop.

You can use it as a directive, and load it with `angular.module('myApp',['lrDragNdrop'])`.  Items can be dragged from one collection to another, copied, and sorted.
