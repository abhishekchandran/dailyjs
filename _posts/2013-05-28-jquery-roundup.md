---
layout: post
title: "jQuery Roundup: 1.10.0, 2.0.1, AopJS, Backbone.Cache and Backbone.Cleanup"
author: Alex Young
categories:
- jquery
- plugins
- backbone.js
- aspect-oriented
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###1.10.0 and 2.0.1

[jQuery 1.10.0 and 2.0.1](http://blog.jquery.com/2013/05/24/jquery-1-10-0-and-2-0-1-released/) were released last week:

> Our main goal with these two releases is to synchronize the features and behavior of the 1.x and 2.x lines, as we pledged a year ago when jQuery 2.0 was announced. Going forward, we'll try to keep the two in sync so that 1.11 and 2.1 are feature-equivalent for example.

Even though these newer jQuery releases have shed the legacy IE support baggage, there are still IE-specific fixes: [IE9 focus of death](http://bugs.jquery.com/ticket/13393).

###AopJS

AopJS (GitHub: [victorcastroamigo / aopjs](https://github.com/victorcastroamigo/aopjs), License: _MIT_, jQuery: [aop](http://plugins.jquery.com/aop/)) by Víctor Castro Amigo is a minimal aspect oriented library for JavaScript, with a jQuery plugin.  It has a chainable API that can be used to define _advice_, with various types: `before`, `after`, `afterReturning`, `afterThrowing`, and `around`.

The author has included unit tests, and the readme has plenty of examples.  The jQuery portion of the project doesn't add any specific aspect-oriented enhancements to jQuery itself, it just binds to `$.aop.aspect`.

###Backbone.Cache and Backbone.Cleanup

Naor Ye sent in some of his Backbone.js plugins.  [Backbone.Cache](https://github.com/naorye/BackboneCache) allows you to define a cache object that models and collections can use.  You'll need to make your models and collections inherit from the right classes: `Backbone.CachedModel` and `Backbone.CachedCollection` provide a `cacheObject` property that can be used to point to a suitable object to use as a cache.

[Backbone.Cleanup](https://github.com/naorye/BackboneCleanup) offers parent classes for views and `Backbone.Router` to help you clean and reuse nested views.  A method called `markCurrentView` is used to set the current view, so when the view is no longer active its `cleanup` method will be triggered.
