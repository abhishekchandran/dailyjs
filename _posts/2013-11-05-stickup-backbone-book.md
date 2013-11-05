---
layout: post
title: "stickUp, Backbone.js Guide"
author: Alex Young
categories:
- books
- backbonejs
- jquery
- plugins
- ui
---

###stickUp

[stickUp](http://lirancohen.github.io/stickUp/) (GitHub: [LiranCohen / stickUp](https://github.com/LiranCohen/stickUp), License: _LGPL_) by Liran Cohen is a plugin for handling navigation bars that stick at the top of the page when it's scrolled:

> stickUp is a simple plugin that "sticks" an element to the top of the browser window while scrolling past it, always keeping it in view. This plugin works on multi-page sites, but has additional features for one-pager layouts.

It can detect the vertical position of the element and automatically fix it to the right position:

{% highlight javascript %}
$('.navbar-wrapper').stickUp({
  marginTop: 'auto'
});
{% endhighlight %}

###Backbone.js Guide

Julio Cesar Ody's [Backbone.js Guide](http://pragmatic-backbone.com/) is a freely available and somewhat opinionated book about Backbone that he's currently in the process of writing.  There are five chapters so far, and two more should be coming soon.  The source is on GitHub at [juliocesar / backbone-book](https://github.com/juliocesar/backbone-book).

> The rule of thumb is get the hell away from the DOM. You won't read from it ever (e.g.: getting an element's class name, or the length of a list counts as that), because your data layer knows what has what value and in what state anything is at any given time. You'll write to the DOM only by rendering views. If you like this approach, it's totally ok to use just regular JS or jQuery.

