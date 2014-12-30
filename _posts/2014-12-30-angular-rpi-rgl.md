---
layout: post
title: "React-Grid-Layout, Angular Debug Bar and Reading Position"
author: Alex Young
image: "/images/posts/rpi.gif"
categories:
- angularjs
- react
- responsive
- layout
---

###React-Grid-Layout

Samuel Reed sent in [React-Grid-Layout](https://strml.github.io/react-grid-layout/examples/1-basic.html) (GitHub: [strml/react-grid-layout](https://github.com/strml/react-grid-layout), License: _MIT_), a grid system that is responsive.  It requires React but doesn't require any other library (including jQuery).

You can use the `ReactGridLayout` custom element in templates which allows you to cleanly specify how many rows and columns you'd like.  It also supports props for columns, rows, responsive breakpoints, and layout change events.

Although the author states it has fewer features than Packery or Gridster, it supports some cool stuff like vertical auto-packing and dragging and resizing.

###Angular Debug Bar and Reading Position Indicator

Maciej Rzepiński sent in two useful Angular projects:

* [angular-debug-bar](http://mrzepinski.github.io/angular-debug-bar/) (GitHub: [mrzepinski/angular-debug-bar](https://github.com/mrzepinski/angular-debug-bar), License: _MIT_)
* [angular-rpi](http://mrzepinski.github.io/angular-rpi/) (GitHub: [mrzepinski/angular-rpi](https://github.com/mrzepinski/angular-rpi), License: _MIT_)

angular-debug-bar allows you to including a new element, `angular-debug-bar`, to show some statistics about the current page.  This includes a count of `$watch` and `$listener` items, DOM objects, and page load time.  Each metric is defined with a `registerPlugin` method, so you might be able to add new metrics although I haven't tried that myself.

angular-rpi is based on the [Reading Position Indicator](http://css-tricks.com/reading-position-indicator/) post from CSS-Tricks.  It shows a bar at the top of the page as you scroll the document:

![RPI](/images/posts/rpi.gif)

You can use it with the `rpi` directive.  Both projects have a demo that you can run locally.  If you want to edit the progress bar styles, then you can use the `.scss` file and run `npm install ; bower install ; gulp`.
