---
layout: post
title: "PrototypeJungle, Slick, Cash"
author: "Alex Young"
categories:
- modules
- libraries
- browser
- svg
---

###PrototypeJungle

[PrototypeJungle](http://prototypejungle.org/) (GitHub: [chrisGoad / prototypejungle](https://github.com/chrisGoad/prototypejungle/tree/svg), License: _MIT_) by Chris Goad is a tree-based object model and inspector.  The inspector makes all of the underlying data structures visible, so you can explore and manipulate it.

![PrototypeJungle](/images/posts/prototypejungle.png)

For example, [this is a bar chart](http://prototypejungle.org/inspect?item=/sys/repo0/example/BarChart2&intro=1&cf=1), displayed with SVG.  You can drill down into each bar and edit things like the bar height, colour, stroke, and so on.

> Elements of the model can be serialized and saved in files, and represent things of various complexities, from simple infographic marks such as bars or bubbles, to axes or legends, to complete charts.
>
> Often, an element serves as a prototype (in the general sense). For example, consider a prototypical bubble or bar which is instantiated once for each data point. When an instance of an element is wanted, a special variety of deep copy is made which inherits as appropriate from the original using JavaScript's prototype formalism. Subsequent adjustments to the original will be inherited by all of the instances, at least in those aspects that have not been overriden.

Chris says it's at an early stage, but I think it's a pragmatic look at data visualisation that readers might find interesting.

###Slick, Cash

Ken Wheeler sent in some client-side projects that he's been working on.  One is [Slick](http://kenwheeler.github.io/slick/) (GitHub: [kenwheeler / slick](https://github.com/kenwheeler/slick), License: _MIT_), a carousel that supports a huge amount of things: CSS3 animations when available, touch and mouse gestures, infinite loop, autoplay, adaptive height, lazy loading, fade effects, and it's responsive as well.

It has an API so you can dynamically add and remove slides.  It depends on jQuery 1.7+.

Ken's other project is [cash](https://github.com/kenwheeler/cash), a jQuery alternative.  It supports lots of methods from jQuery's API, and is written using separate modules so the source is quite easy to follow.  The build system is Gulp.  You might find it interesting if you like using or writing small libraries that don't depend on jQuery and want to see how DOM stuff works without legacy cruft.
