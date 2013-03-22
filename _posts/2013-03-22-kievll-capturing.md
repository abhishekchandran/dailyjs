---
layout: post
title: "KievII, Capturing, Mobify 2.0"
author: "Alex Young"
categories: 
- audio
- mobile
---

###KievII Host

<div class="image">
  <img src="/images/posts/kievii.png" alt="" />
  <small>The KievII audio plugin host</small>
</div>

[KievII Host](http://kievii.net/k2h.html) (GitHub: [janesconference / KievIIHost](https://github.com/janesconference/KievIIHost), License: _MIT_) by Cristiano Belloni is an audio plugin host based on the Web Audio API.  The plugins are loaded dynamically using RequireJS from a GitHub repository, and already include lots of cool effects like a phaser, wah-wah, and pitch shift. 

If you want to try out the [KievII demo](http://bitterspring.net/k2h/), which is a lot of fun, you'll need Chrome and to enable _Web Audio Input_ in `chrome://flags`.  I tested it in Chrome 25 on a Mac and it ran pretty solidly.  It allows audio to be routed from the mic through various effects, and there's also a sample player with a keyboard for triggering audio samples at different pitches.

There's more information about KievII at [kievii.net](http://kievii.net/), which has a demo of a step sequencer.

###Capturing for Responsive Design

Shawn Jansepar sent in his post at the Mozilla Hacks blog, called [Capturing - Improving Performance of the Adaptive Web](https://hacks.mozilla.org/2013/03/capturing-improving-performance-of-the-adaptive-web/), about a client-side API he's developed called Capturing:

> Our approach to give you resource control is done by capturing the source markup before it has a chance to be parsed by the browser, and then reconstructing the document with resources disabled.

> The ability to control resources client-side gives you an unprecedented amount of control over the performance of your website.

> Capturing was a key feature of Mobify.js 1.1, our framework for creating mobile and tablet websites using client-side templating. We have since reworked Mobify.js in our 2.0 release to be a much more modular library that can be used in any existing website, with Capturing as the primary focus.

One example Shawn uses is using a polyfill for the `picture` element, which only includes an extra `img` tag for browsers without JavaScript turned on.  This is in contrast to other solutions that require `noscript` tags.

###Mobify.js 2.0

Meanwhile, [Mobify.js 2.0](http://www.mobify.com/mobifyjs/) (GitHub: [mobify / mobifyjs](https://github.com/mobify/mobifyjs), License: _MIT_) has been released as a developer preview.  This includes the Capturing API mentioned in Shawn's post above.

The goal of Mobify.js is to help existing sites better support mobile devices.  The [examples](http://www.mobify.com/mobifyjs/v2/examples/) included are the `picture` polyfill mentioned above, using media queries, and templating.

