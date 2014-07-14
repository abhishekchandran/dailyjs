---
layout: post
title: "An Alternative to AMD: CMD"
author: "Alex Young"
categories:
- modules
- amd
- harmony
---

By now most of us use AMD or CommonJS as our module API.  With Harmony on the horizon, there doesn't seem to be much need to innovate where libraries like RequireJS have established a niche.  Despite this, John Wu sent me his module loader that can be found in his project [wd.js](https://github.com/tjwudi/wd.js/wiki/module-loader).

This approach uses a chainable API which allows modules to be loaded asynchronously in a browser-friendly way, without AMD's less fluent syntax:

{% highlight javascript %}
wd.module('core.util')
  .require('core.bar')
  .require('core.foo')
  .body(function() {
    // foo and bar are now loaded
  });
{% endhighlight %}

John calls this style CMD, which stands for Chainable Module Definition.  Although it seems like an obvious idea, it's new to me and I think it fits in well with other modern JavaScript libraries.

