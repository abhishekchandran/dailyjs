---
layout: post
title: "jQuery Roundup: UI 1.10.3, simplePagination.js, jQuery Async"
author: Alex Young
categories:
- jquery
- plugins
- async
- pagination
- jquery-ui
- ui
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery UI 1.10.3

[jQuery UI 1.10.3](http://blog.jqueryui.com/2013/05/jquery-ui-1-10-3/) was released last week.  This is a maintenance release that has fixes for Draggable, Sortable, Accordion, Autocomplete, Button, Datepicker, Menu, and Progressbar.

###simplePagination.js

![simplePagination](/images/posts/simplepagination.png)

[simplePagination.js](http://flaviusmatis.github.io/simplePagination.js/) (GitHub: [flaviusmatis / simplePagination.js](https://github.com/flaviusmatis/simplePagination.js), License: _MIT_) by Flavius Matis is a pagination plugin that supports Bootstrap.  It has options for configuring the page links, next and previous text, style attributes, onclick events, and the initialisation event.

There's an API for selecting pages, and the author has included three themes.  When selecting a page, the truncated pages will shift, so it's easy to skip between sets of pages.

###jQuery Async

![jQuery Async](/images/posts/jqasync.png)

[jQuery Async](http://acavailhez.github.io/jquery-async/demo.html) (GitHub: [acavailhez / jquery-async](https://github.com/acavailhez/jquery-async), License: _Apache 2_) by Arnaud Cavailhez is a UI plugin for animating things while asynchronous operations take place.  It depends on Bootstrap, and makes it easy to animate a button that triggers a long-running process.

The documentation has some clever examples that help visualise how the plugin works -- two buttons are displayed so you can trigger the `'success'` and `'error'` events by hand.  It's built using `$.Deferred`, so it'll work with the built-in Ajax API without much effort.
