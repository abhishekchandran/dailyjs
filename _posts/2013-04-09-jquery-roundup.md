---
layout: post
title: "jQuery Roundup: 2.0 Beta 3, betterToggle, Cavendish.js"
author: Alex Young
categories:
- jquery
- plugins
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery 2.0 Beta 3

[jQuery 2.0 Beta 3](http://blog.jquery.com/2013/04/09/jquery-2-0-beta-3-released/) is out:

> ... we really need your help in finding and fixing any bugs that may be hiding in the nooks and crannies of jQuery 2.0. We want to get all the problems ironed out before this version ships, and the only way to do that is to find out whether it runs with your code.

This release introduces Node compatibility, so you can now load it with `require()`.  It also makes it work in Windows 8 Store apps.

###betterToggle

[betterToggle](http://jquer.in/betterToggle-jquery-plugin/) (GitHub: [kanakiyajay / betterToggle](https://github.com/kanakiyajay/betterToggle), License: _GPLv2_) by Jay Kanakiya is a plugin for toggling elements with CSS3 transforms.  As an added bonus it allows multiple elements to be toggled.

Usage is similar to `.toggle`: `$(selector).betterToggle()`, and the project's homepage has plenty of demos.

###Cavendish.js

[Cavendish.js](http://michaek.github.io/cavendish.js/index.html) (GitHub: [michaek / cavendish.js](https://github.com/michaek/cavendish.js), License: _MIT_) by Michael Hellein is a slide manager plugin aimed at front-end developers well-versed in CSS.  It has a plugin-based API that allows it to support different styles for displaying and navigating slides:

{% highlight javascript %}
var cavendish = $('.cavendish').cavendish('cavendish');
cavendish.plugins['player'].start();
{% endhighlight %}

The bundled plugins include a simple player that pauses on hover, a pager, previous and next arrows, and a parallax scrolling effect.  The API also exposes the events used, so you can add listeners to see when Cavendish has been initialised and after a slide has been transitioned.
