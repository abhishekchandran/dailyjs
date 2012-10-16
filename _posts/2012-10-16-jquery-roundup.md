---
layout: post
title: "jQuery Roundup: jq-tiles, plusTabs, Kwicks"
author: Alex Young
categories:
- jquery
- jquery-ui
- tabs
- plugins
- slideshow
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jq-tiles

![jq-tiles](/images/posts/jqtiles.png)

[jq-tiles](http://elclanrs.github.com/jq-tiles/) (GitHub: [elclanrs / jq-tiles](https://github.com/elclanrs/jq-tiles), License: _MIT_) is a slideshow plugin that breaks images up into tiles and uses CSS3-based effects.  The number of tiles can be changed, and the transition and animation speeds can be configured.

To use the plugin, call `$('.slider').tilesSlider(options)` on an element that contains a set of images.  Events are used to stop and start the slideshow: `$('.slider').trigger('start')`.

###plusTabs

![plusTabs compared with standard tabs](/images/posts/plustabs.png)

[plusTabs](http://jsfiddle.net/jasonday/fdhaS/embedded/result/) (GitHub: [jasonday / plusTabs](https://github.com/jasonday/plusTabs), License: _MIT/GPL_) by Jason Day groups jQuery UI tabs under a tab with a menu.  Jason's example is scaled to a slim resolution that might be found on a smartphone, showing how jQuery UI tabs become cluttered and messy in such circumstances.

###Kwicks

[Kwicks](http://devsmash.com/projects/kwicks) (GitHub: [jmar777 / kwicks](https://github.com/jmar777/kwicks), License: _MIT_) by Jeremy Martin is a sliding panel plugin.  It can display vertical or horizontal panels, and grow or shrink them on hover.  It can also be used to create a slideshow.

Kwicks works with nested elements like an unordered list, but it'll actually work with any tag, so `<li>` isn't hardwired.
