---
layout: post
title: "jQuery Roundup: One Page Scroll, crSpline"
author: Alex Young
categories:
- jquery
- plugins
- animation
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###One Page Scroll

[One Page Scroll](http://www.thepetedesign.com/demos/onepage_scroll_demo.html) (GitHub: [peachananr / onepage-scroll](https://github.com/peachananr/onepage-scroll)) by Pete Rojwongsuriya enables pages to scroll in the vertical locking style like Apple's new iPhone 5S page.  It's based around sections -- any selector can be used -- and jQuery's animations:

{% highlight javascript %}
$('.main').onepage_scroll({
   sectionContainer: 'section',
   easing: 'ease',
   animationTime: 1000,
   pagination: true,
   updateURL: false
});
{% endhighlight %}

I had a look at the source and it includes Eike Send's `$.fn.swipeEvents` so it should work with touchscreens.

###jquery.crSpline

<div class="image">
  <img src="/images/posts/crspline.png" />
  <small>A visualisation of movement along Catmull-Rom splines.</small>
</div>

[jquery.crSpline](http://ijin.net/crSpline/demo.html) (GitHub: [MmmCurry / jquery.crSpline](https://github.com/MmmCurry/jquery.crSpline), License: _MIT_) by M. Ian Graham is an animation plugin that moves objects along waypoints, smoothing the edges with splines.

The name crSpline comes from [Catmull-Rom](http://en.wikipedia.org/wiki/Cubic_Hermite_spline#Catmull.E2.80.93Rom_spline):

> The curve is named after Edwin Catmull and Raphael Rom. In computer graphics, Catmull–Rom splines are frequently used to get smooth interpolated motion between key frames. For example, most camera path animations generated from discrete key-frames are handled using Catmull–Rom splines.

The plugin includes `$.crSpline.buildSequence` which can be used to generate spline animation objects.  At the moment there isn't much documentation, but [demo.js](http://ijin.net/crSpline/demo.js) should get you started.
