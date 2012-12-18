---
layout: post
title: "jQuery Roundup: 1.9, UI 1.10, Maskew"
author: Alex Young
categories:
- jquery
- plugins
- mobile
- effects
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery 1.9 Beta 1

[jQuery 1.9 Beta 1](http://blog.jquery.com/2012/12/17/jquery-1-9-beta-1-released/) has been released, and this version removes previously deprecated features so you'll want to pay attention.  Fortunately, Dave Methvin has been working on [jquery / jquery-migrate](https://github.com/jquery/jquery-migrate), which is a plugin for figuring out which deprecated features are being used in your projects.  The development version shows console warning messages, and these are stored in `jQuery.migrateWarnings` for browsers that don't support `console`.  There's a full list of the warnings in [jQuery Migrate Plugin - Warning Messages](https://github.com/jquery/jquery-migrate/blob/master/warnings.md).

The focus of 1.9 has been API cleanup, and there's also a [jQuery 1.9 Upgrade Guide](http://jquery.com/upgrade-guide/1.9/), where these API changes have been documented.

###jQuery UI 1.10 Beta

[jQuery UI 1.10 Beta](http://blog.jqueryui.com/2012/12/jquery-ui-1-10-beta/) is out.  This version features a new API for the [Dialog widget](http://forum.jquery.com/topic/dialog-api-redesign), and a redesigned [Progressbar API](http://forum.jquery.com/topic/progressbar-api-redesign).

There are major API changes in 1.10, so if you haven't updated to 1.9 yet then you might want to read through the [1.9 upgrade guide](http://jqueryui.com/upgrade-guide/1.9/).

###Maskew

<div class="image">
  <img src="/images/posts/maskew.png" alt="" />
  <small>Get skewed.</small>
</div>

[Maskew](http://oxism.com/maskew/) (GitHub: [dmotz / maskew](https://github.com/dmotz/maskew), License: _MIT_) by Dan Motzenbecker is a small plugin that can skew elements along a specified angle.  It has an optional jQuery plugin, but also has a simple prototype class API.  It has support for touchscreen events, specified by passing `{ touch: true }` as an argument.

Dan has included the build script and some tests.

