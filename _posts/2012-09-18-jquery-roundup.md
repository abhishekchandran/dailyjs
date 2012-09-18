---
layout: post
title: "jQuery Roundup: equalize.js, jQuery Builder, Gridster.js"
author: Alex Young
categories:
- jquery
- plugins
- design
- ui
- layout
- grid
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###equalize.js

This plugin comes from the "should I just use a table?" department of design technicalities that we still have to deal with in 2012: [equalize.js](http://tsvensen.github.com/equalize.js/) (GitHub: [tsvensen / equalize.js](https://github.com/tsvensen/equalize.js/), License: _MIT/GPL_).  Created by Tim Svensen, this plugin resizes elements to match their height or any other dimension supported by [jQuery Dimensions](http://api.jquery.com/category/dimensions/).

It works by calling a single method on the parent selector:

{% highlight javascript %}
// Height is the default
$('#height-example').equalize();

$('.parent').equalize('outerHeight');
$('.parent').equalize('innerHeight');
$('.parent').equalize('width');
$('.parent').equalize('outerWidth');
$('.parent').equalize('innerWidth');
{% endhighlight %}

The documentation has full examples.

###jQuery Builder

[jQuery Builder](http://projects.jga.me/jquery-builder/) (GitHub: [jgallen23 / jquery-builder](https://github.com/jgallen23/jquery-builder), License: _MIT_, npm: [jquery-builder](https://npmjs.org/package/jquery-builder)) by Greg Allen is a web-based tool for building a custom version of jQuery 1.8.1.  As jQuery has evolved it's got a lot easier to include only the components necessary for a given project.  This particular solution has been made using Node, and is installable with npm.

###Gridster.js

[Gridster.js](http://gridster.net/) (GitHub: [ducksboard / gridster.js](https://github.com/ducksboard/gridster.js), License: _MIT_) from [Ducksboard](http://ducksboard.com/) is a grid plugin that allows layouts to be designed by drag and drop.  Elements can span multiple columns, and by dynamically added and removed.  Any element can be used because Gridster is based around data attributes.

Gridster is distributed with suitable CSS, and supports IE 9+, Firefox, Chrome, Safari, and Opera.
