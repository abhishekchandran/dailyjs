---
layout: post
title: "jQuery Roundup: Airbnb Style Guide, jPanelMenu, Crumble, imgLiquid"
author: Alex Young
categories:
- jquery
- style-guides
- images
- on-page guidance
- mobile
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Airbnb JavaScript Style Guide

[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) is a pretty detailed JavaScript style guide that includes [suggestions for jQuery](https://github.com/airbnb/javascript#jquery).  As a bonus, the [Resources](https://github.com/airbnb/javascript#resources) section includes links to other style guides (and DailyJS, thanks Airbnb!)

I've been using [Google's Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml) for a few projects, although I don't necessarily have a preference for any style guide.  The code style used in examples on DailyJS came from trying to use horizontal space effectively (the blog has a fixed-width narrow design), but also by trying to make things explicit for beginners.  Even these humble goals are subjective enough to cause endless arguments.  The best advice I could give on the matter is to pick a style and be consistent.

###jPanelMenu

![jPanelMenu screenshot](/images/posts/jpanelmenu.png)

[jPanelMenu](http://jpanelmenu.com/) (GitHub: [acolangelo / jPanelMenu](https://github.com/acolangelo/jPanelMenu)) by Anthony Colangelo creates a navigation panel similar to those found in recent mobile applications.  It can be configured to use selectors for the menu and an element that opens the menu:

{% highlight javascript %}
var jPM = $.jPanelMenu({
  menu: '#custom-menu-selector'
, trigger: '.custom-menu-trigger-selector'
});

jPM.on();
{% endhighlight %}

This creates two `div` elements that contain the menu and the corresponding panel for the content.

jPanelMenu is well documented, and the documentation itself is built using the plugin so it doubles as a detailed example.

###Crumble

[Crumble](http://tommoor.github.com/crumble/) (GitHub: [tommoor / crumble](https://github.com/tommoor/crumble), License: _MIT_) by Tom Moor is an interactive tour built using [grumble.js](https://github.com/jamescryer/grumble.js).  Similar to the plugins mentioned by Oded Ben-David in [Introduction to On-Page Guidance](http://dailyjs.com/2012/11/02/on-screen-guidance-intro/), Crumble shows help bubbles that draw attention to elements on a page.

###imgLiquid

[imgLiquid](https://dl.dropbox.com/u/6983010/wserv/imgLiquid/examples/imgLiquid.html) (GitHub: [karacas / imgLiquid](https://github.com/karacas/imgLiquid), License: _MIT/GPL_) by Alejandro Emparan is a plugin for resizing images to fit a given container.  It can try to fill a container or shrink the image instead, by using CSS:

{% highlight javascript %}
$(selector).imgLiquid({ fill: true });
{% endhighlight %}

There's also a `fadeInTime` option that'll trigger a [fadeTo](http://api.jquery.com/fadeTo/) animation.
