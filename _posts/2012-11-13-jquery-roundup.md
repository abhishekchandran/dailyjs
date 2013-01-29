---
layout: post
title: "jQuery Roundup: SliderShock, printThis, readMore"
author: Alex Young
categories:
- jquery
- slideshow
- printing
- truncation
- sponsored-content
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery SliderShock

<div class="sponsored-content" style="background-color: #f0f4cf; padding: 0; margin: 10px 0; border-radius: 5px; font-size: 90%; width: 530px; padding: 0 1px">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

![SliderShock example](/images/posts/slidershock-1.png)

[jQuery SliderShock](http://www.jqueryslidershock.com/) is a responsive slider plugin that can be dropped into WordPress sites.  There's full documentation for [regular websites](http://www.jqueryslidershock.com/?page_id=31) and [WordPress sites](http://www.jqueryslidershock.com/?page_id=36).  The WordPress version has some additional features, like built-in support for sliders from external data sources like RSS.  The plugin supports various options, including up to 31 transition effects, control over delay time and positioning, and easy styling.

Clicking _Build Your Own_ on the SliderShock homepage displays all of the available options:

![SliderShock options](/images/posts/slidershock-2.png)

SliderShock can display text captions within slides, and comes bundled with lots of CSS3-based effects.  The free version, licensed for use in personal projects, has 10 effects, and the premium  version has 31 effects and 39 skins.  A license for a single site costs $19, while multiple sites costs $29.  There's also a developer license for $99 that allows resale.  "Combo" licenses are available if you wish to buy both the WordPress and jQuery versions at once, otherwise you'll have to license them separately.

###jquery.printThis

[jquery.printThis](https://github.com/jasonday/printThis) (License: _MIT/GPL_) by Jason Day is a fork of [permanenttourist / jquery.jqprint](https://github.com/permanenttourist/jquery.jqprint), and based on Ben Nadel's [Ask Ben: Print Part Of A Web Page With jQuery](http://www.bennadel.com/blog/1591-Ask-Ben-Print-Part-Of-A-Web-Page-With-jQuery.htm) post -- a combination of several things to solve the problem of printing a given element on a page.  Jason's changes can optionally include page styles, import additional stylesheets, and avoids using `document.write`.

It's interesting to see how this works internally -- the plugin is concise but it takes a bit of `iframe` manipulation to get the desired results.

###jQuery.readMore

Dealing with dynamically truncating content is tricky, and there are many solutions out there.  Stephan Ahlf sent in his solution, [jQuery.readMore](http://saquery.com/jquery-readmore/) (GitHub: [s-a / jQuery.readMore](https://github.com/s-a/jQuery.readMore), License: _MIT/GPL_) which uses a method called `$.isOverflowed` to add text until there isn't room for any more.

Previously covered related plugins include [jQuery.smarttruncation](http://polarblau.github.com/smarttruncation/), and [jQuery.textFit](https://github.com/STRML/jquery.textFit).
