---
layout: post
title: "ResponsiveComments, jQuery Evergreen"
author: Alex Young
categories:
- responsive
- design
- jquery
- es6
---

###ResponsiveComments

[ResponsiveComments](http://responsivecomments.com/) (GitHub: [chambaz / ResponsiveComments](https://github.com/chambaz/ResponsiveComments), License: _MIT_) by Adam Chambers is designed to support conditional loading using HTML comments:

> Through the use of HTML comments, markup can be introduced to progressively enhance an experience as various media queries or feature detections evaluate to true.

Data attributes are used with valid media queries to conditionally display HTML.  For example:

{% highlight html %}
<div data-responsive-comment-media="(min-width: 769px)">
  <!-- <div><p>Any content can go in here</p></div> -->
</div>
{% endhighlight %}

IE 9 and below support requires the [matchMedia.js polyfill](https://github.com/paulirish/matchMedia.js/), but otherwise browser support is pretty good.

###jQuery Evergreen

What would jQuery look like if it was written for modern browsers with ES6 modules?  [jQuery Evergreen](http://webpro.github.io/jquery-evergreen/) (GitHub: [webpro / jquery-evergreen](https://github.com/webpro/jquery-evergreen), License: _MIT_, Bower: _jquery-evergreen_) by Lars Kappert is an attempt at answering that question.

> jQuery Evergreen works with modern browsers. It has the same familiar API as jQuery, and is lean and mean with the following, optional modules: selector, class, DOM, event, attr and html.
> The source is written in the ES6 Modules format, and transpiled to an AMD version, and a "browser global" version using the ES6 Module Transpiler.

It'll work with current versions of most browsers thanks to [transpilation](http://square.github.io/es6-module-transpiler/) and an IE9 polyfill for `classList`.

You can even create custom builds with Grunt, like this:

{% highlight text %}
grunt --exclude=attr,class,dom,event,html,mode,selector
{% endhighlight %}

