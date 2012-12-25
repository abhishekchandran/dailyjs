---
layout: post
title: "jQuery Roundup: jquery.columns, stackable.js"
author: Alex Young
categories:
- jquery
- plugins
- columns
- responsive
- tables
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jquery.columns

[jquery.columns](https://github.com/elclanrs/jquery.columns) (License: _MIT_) by Cedric Ruiz extends the `$.css` method to support [viewport-percentage lengths](http://www.w3.org/TR/css3-values/#viewport-relative-lengths), basically making it a lot easier to work with responsive grids.

The plugin provides a `$.columns` method, but passing sizes with `vw` units to `$.css` will work as well.

There's a demo here: [jquery.columns demo](http://elclanrs.github.com/jquery.columns/).

###stacktable.js

[stacktable.js](http://johnpolacek.github.com/stacktable.js/) (GitHub: [johnpolacek / stacktable.js](https://github.com/johnpolacek/stacktable.js/), License: _MIT/GPL_) by John Polacek is a plugin for stacking tables on small screens.  It's designed to work in responsive layouts by using media queries.

To make tables fit smaller screens, this plugin stacks each column vertically in order.  The headers will be placed in the correct order as well.  Behind the scenes, tables are actually replaced with the stacked version -- by passing a specific class name to the plugin responsive layouts can be supported.
