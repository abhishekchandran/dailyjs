---
layout: post
title: "jQuery Roundup: jQuery.IO, Animated Table Sorter, jQuery-ui-pic"
author: Alex Young
categories:
- jquery
- plugins
- forms
- json
- icons
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery.IO

jQuery.IO (GitHub: [sporto / jquery_io.js](https://github.com/sporto/jquery_io.js), License: _MIT_) by Sebastian Porto can be used to convert between form data, query strings, and JSON strings.  It uses `JSON.parse`, and comes with tests and a Grunt build script.

Converting a form to a JavaScript object is just `$.io.form($('form')).object()`, and the output has form names as keys rather than the array results [.serializeArray](http://api.jquery.com/serializeArray/) returns.

###Animated Table Sorter

[Animated Table Sorter](http://www.matanhershberg.com/plugins/jquery-animated-table-sorter/) (GitHub: [matanhershberg / animated_table_sorter](https://github.com/matanhershberg/animated_table_sorter), License: _MIT_, jquery: [AnimatedTableSorter](http://plugins.jquery.com/AnimatedTableSorter/)) by Matan Hershberg is a table sorting plugin that moves rows using `.animate` when they're reordered.

All you need to do is call `.tableSort()` on a table.  CSS and images have been provided for styling the selected column and sort direction.

###jQuery-ui-pic

[jQuery-ui-pic](http://rtsinani.github.com/jQuery-ui-pic/) (GitHub: [rtsinani / jQuery-ui-pic](https://github.com/rtsinani/jQuery-ui-pic)) by Artan Sinani provides an extracted version of the icons from Bootstrap and the image sprites from jQuery UI.

In this version the CSS classes are all prefixed with `pic-`, so you can use them like this: `<i class="pic-trash"></i>`.  This might prove useful if you're looking for a quick way to reuse jQuery UI's icons without using the rest of jQuery UI.  I licensed [Glyphicons Pro](http://glyphicons.com/glyphicons-licenses/) myself because I find myself using them so much.

