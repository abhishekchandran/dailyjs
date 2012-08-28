---
layout: post
title: "jQuery Roundup: jQuery Color 2.1.0, jQuery UI 1.9 RC, Avgrund Modal"
author: Alex Young
categories: 
- jquery
- plugins
- jqueryui
- effects
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery Color 2.1.0

[jQuery Color 2.1.0](http://blog.jquery.com/2012/08/24/jquery-color-2-1-0/) (GitHub: [jquery / jquery-color](https://github.com/jquery/jquery-color/), License: _MIT_) has been released.  This plugin includes lots of methods for defining, parsing, and otherwise manipulating and animating colours.  Version 2 includes new API methods that allow colours to be created and modified, and this includes support for RGBA and HSLA colours and animations.

Here are some examples of the plugin in use:

{% highlight javascript %}
// String colour parsing
$.Color('#abcdef');
$.Color('rgba(100,200,255,0.5)');
$.Color('aqua');

// RGB
$.Color(255, 0, 0);

// RGBA
$.Color(255, 0, 0, 0.8);

// Objects work as well
$.Color({ red: red, green: green, blue: blue, alpha: alpha });

// Getters and setters
$.Color(255, 100, 130)
  .green(101)
  .green(); // 101

// Conversion
$.Color(255, 100, 130).toRgbaString(); // 'rgb(255,100,130)'
{% endhighlight %}

###jQuery UI 1.9 RC

[jQuery UI 1.9 RC](http://blog.jqueryui.com/2012/08/jquery-ui-1-9-rc/) has been released, and updates jQuery to 1.8 and jQuery Color to the 2.0 series.  The jQuery UI team are also working on upgrading the project's infrastructure:

> We're working on a new web site, new download builder, and new documentation site to accompany the new release.

###Avgrund Modal

![Avgrund](/images/posts/avgrund.png)

[Avgrund Modal](http://labs.voronianski.com/jquery.avgrund.js/) (GitHub: [voronianski / jquery.avgrund.js](https://github.com/voronianski/jquery.avgrund.js), License: _MIT_) by Dmitri Voronianski is a modal plugin that attempts to create the impression of depth as the modal appears on the page.  The main content zooms out as the modal appears -- the overall effect is surprisingly slick.  Basic usage is `$(selector).avgrund()`, but the plugin has lots of options:

{% highlight javascript %}
$('element').avgrund({
  width: 380
, height: 280
, showClose: false
, showCloseText: ''
, holderClass: ''
, overlayClass: ''
, enableStackAnimation: false
, template: 'Your content goes here..'
});
{% endhighlight %}

This plugin is based on the [Avgrund concept](http://lab.hakim.se/avgrund/) by [Hakim El Hattab](https://twitter.com/hakimel).
