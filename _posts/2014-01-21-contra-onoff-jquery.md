---
layout: post
title: "Contra, jquery.onoff, jQuery 1.11.0 RC1 and 2.1.0 RC1"
author: Alex Young
categories:
- jquery
- plugins
- ui
- flow-control
- async
---

###Contra

![Contra](/images/posts/contralambda.png)

Contra (GitHub: [bevacqua / contra](https://github.com/bevacqua/contra), License: _MIT_, npm: [contra](https://npmjs.org/package/contra), Bower: _contra_) by Nicolas Bevacqua is a flow control library, similar to [async](https://npmjs.org/package/async), but more suited to client-side development.

It has three sets of methods: flow control, functional, and uncategorized.  The flow control methods are for executing groups of functions, like `λ.waterfall(tasks, done)`.  The functional methods are a subset of what you might expect to find in Underscore.js -- `λ.each` and `λ.filter` for example.  I noticed that `λ.each` can handle both arrays and objects, so it's different to `forEach`.

Each method can be exported separately, so you could just pull in a single method if you wanted to.  It has Mocha tests, and can be installed with Bower.

###jquery.onoff

jquery.onoff (GitHub: [timmywil / jquery.onoff](https://github.com/timmywil/jquery.onoff), License: _MIT_) by Timmy Willison is a toggle switch that uses checkboxes.  It supports IE 9 and above, and can be loaded with an AMD loader.

Although it's a relatively simple project, Timmy has included tests, and a Grunt build script.

###jQuery 1.11.0 RC1 and 2.1.0 RC1

[jQuery 1.11.0 RC1 and 2.1.0 RC1](http://blog.jquery.com/2014/01/16/jquery-1-11-0-rc1-and-2-1-0-rc1-released/) have been released.  These releases are maintenance releases, so there aren't any API changes.

The announcement notes that these releases should work properly with Browserify, and can be installed using npm.
