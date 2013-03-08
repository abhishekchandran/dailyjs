---
layout: post
title: "Validatr, pointeraccuracy.js, Testacular Updates"
author: "Alex Young"
categories: 
- libraries
- node
- testing
- mobile
- accessibility
- jquery
- polyfills
---

###Validatr

![Validatr logo](/images/posts/validatr.png)

[Validatr](http://jaymorrow.github.com/validatr/) (GitHub: [jaymorrow / validatr](https://github.com/jaymorrow/validatr/), License: _MIT_, jquery: [validatr](http://plugins.jquery.com/validatr/)) by Jay Morrow is a cross-browser HTML5 form validation library.  That means it provides validators for the new native widgets, like `color` and `date`.  The [Validatr fields documentation](http://jaymorrow.github.com/validatr/fields.html) lists all of the supported inputs and also features demos.

The library requires jQuery, and usage looks like this:

{% highlight javascript %}
$('form').validatr('addTest', 'example', function(element) {});
{% endhighlight %}

Jay has also included [QUnit tests for Validatr](http://jaymorrow.github.com/validatr/tests.html).

###pointeraccuracy.js

pointeraccuracy.js (GitHub: [n-fuse / pointeraccuracy.js](https://github.com/n-fuse/pointeraccuracy.js), License: _MIT_) by Thomas Hoppe is a polyfill for the [media query level 4 property "pointer"](http://dev.w3.org/csswg/mediaqueries4/#pointer).  This API heuristically determines the pointer accuracy, returning `coarse` or `fine` depending on the input device's accuracy:

> This media feature does not indicate that the user will never be able to click accurately, only that it is inconvenient for him to do so. Authors are expected to react to a value of `coarse` by designing pages that do not rely on accurate clicking to be operated.

###Testacular Updates

[Testacular](http://testacular.github.com/0.6.0/index.html), used by the AngularJS team, has been updated.  The new version includes code coverage, Growl and TeamCity reporters, and an adapter for QUnit.

Vojta Jína posts about the project to his Google+ account: [+Vojta Jína](https://plus.google.com/117663020319348671498/posts).
