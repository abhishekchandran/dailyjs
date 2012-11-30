---
layout: post
title: "Viewport Component, grunt-saucelabs, FastClick"
author: Alex Young
categories: 
- grunt
- mobile
- components
- libraries
---

###Viewport Component

[Viewport Component](https://github.com/pazguille/viewport) (License: _MIT_, component: `pazguille/viewport`) by Guille Paz can be used to get information about a browser's viewport.  This includes the width and height as well as the vertical and horizontal scroll positions.

It also emits events for scrolling, resizing, and when the top or bottom has been reached during scrolling.
{% highlight javascript %}
var Viewport = require('viewport')
  , viewport = new Viewport()
  ;

viewport.on('scroll', function() {
  console.log(this.scrollY);
});

viewport.on('top', function() {
  console.log('Top');
});

viewport.on('bottom', function() {
  console.log('Bottom');
});
{% endhighlight %}

###grunt-saucelabs

[grunt-saucelabs](https://github.com/axemclion/grunt-saucelabs) (License: _MIT_, npm: `grunt-saucelabs`) by Parashuram N (axemclion) is a Grunt task for qunit and jasmine tests using [Sauce Labs' Cloudified Browsers](https://saucelabs.com/).  This is similar to the built-in [qunit Grunt task](https://github.com/gruntjs/grunt/blob/master/docs/task_qunit.md), but uses the remote service provided by Sauce Labs instead.

[Sauce Connect](https://saucelabs.com/docs/sauce-connect) can be used to create a tunnel for testing pages that aren't accessible on the Internet.

###FastClick

[FastClick](https://github.com/ftlabs/fastclick) (License: _MIT_, npm: [fastclick](https://npmjs.org/package/fastclick), component: `ftlabs/fastclick`) from the Financial Times helps remove the delay in mobile browsers that occurs between a tap and the trigger of `click` events.

The authors have included some simple tests, documentation, and examples.  The project is extremely well packaged, including support for npm, component, AMD, and Google Closure Compiler's `ADVANCED_OPTIMIZATIONS`.

Internally, FastClick works by binding events to a "layer" and binding several touch event handlers.  These handlers use internal properties to determine how elements are being interacted with.  If certain conditions are met, then a `click` event will be generated, and several attributes will be added to the event to allow further tracking.

The event handlers can be easily removed using `FastClick.prototype.destroy`, and the project has a wide range of special cases for handling divergent behaviour in iOS and Android.
