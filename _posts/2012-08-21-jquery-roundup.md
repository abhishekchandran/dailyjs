---
layout: post
title: "jQuery Roundup: Infinity.js, lorem, oriDomi"
author: Alex Young
categories: 
- jquery
- plugins
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Infinity.js

![Infinity.js](/images/posts/infinityjs.png)

[Infinity.js](http://airbnb.github.com/infinity/) (GitHub: [airbnb / infinity](https://github.com/airbnb/infinity), License: _BSD_) from developers at Airbnb is an infinite scrolling plugin based on the iOS `UITableView` class.  It's implemented by using containers that move content in and out of the DOM based on throttled scroll events, to keep scrolling smooth.  The current version has some caveats -- ListViews can't be nested or have a height set by CSS.

To back up the performance claims, the authors have made demo pages with [Infinity.js turned on](http://airbnb.github.com/infinity/demo-on.html) and [turned off](http://airbnb.github.com/infinity/demo-off.html).  At least in my browser, it's clear that Infinity.js improves the performance.  Also, several performance enhancements are currently planned, including changing the internal `ListItem` array to use a self-balancing binary tree.

###lorem

[lorem](https://github.com/shyiko/lorem) (License: _MIT_, npm: [lorem](https://npmjs.org/package/lorem)) by Stanley Shyiko is a text generator that works with Node and browsers, and it includes optional jQuery plugin support:

{% highlight javascript %}
$(selector).ipsum();
{% endhighlight %}

The author has included Nodeunit tests, and a build script.

###oriDomi

[oriDomi](http://oridomi.com/) (GitHub: [dmotz / oriDomi](https://github.com/dmotz/oridomi), License: _MIT_) by Dan Motzenbecker is a small script with optional jQuery support that creates an effect on images and web fonts that looks like folding paper, by using CSS 3D transforms.

{% highlight javascript %}
$(selector).oriDomi({
  vPanels: 3
, hPanels: 10
, perspective: 200
, speed: 500
, shading: false
});
{% endhighlight %}

It works best when it can figure out the dimensions of the element it's applied to, so it's probably a good idea to ensure images used with the effect have `width` and `height` attributes.
