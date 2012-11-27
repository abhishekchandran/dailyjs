---
layout: post
title: "jQuery Roundup: 1.8.3, UI 1.9.2, oolib.js"
author: Alex Young
categories:
- jquery
- jquery-ui
- oo
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery 1.8.3


[jQuery 1.8.3](http://blog.jquery.com/2012/11/13/jquery-1-8-3-released/) and [jQuery Color 2.1.1](http://blog.jquery.com/2012/11/23/jquery-color-2-1-1-released/) are out.  There are a few interesting bug fixes in this release that you might want to check out:

* [#12690: Non-ASCII characters caused IE7 to fail to load jQuery on pages with a non-UTF8 encoding](http://bugs.jquery.com/ticket/12690)
* [#12357: jQuery 1.8.0 Not parseable by XUL Runner applications](http://bugs.jquery.com/ticket/12357)
* [#12837: All animations break after zooming a lightbox on an iPad](http://bugs.jquery.com/ticket/12837)
* [#12497: Animations crashing stock Android 2.3.4 browser](http://bugs.jquery.com/ticket/12497)

###jQuery UI 1.9.2

[jQuery UI 1.9.2](http://blog.jqueryui.com/2012/11/jquery-ui-1-9-2/) is out:

> This update brings bug fixes for Accordion, Autocomplete, Button, Datepicker, Dialog, Menu, Tabs, Tooltip and Widget Factory.

The [1.9.2 changelog](http://jqueryui.com/changelog/1.9.2/) contains a full breakdown of the recent changes.

###oolib.js

[oolib.js](http://idya.github.com/oolib/) (GitHub: [idya / oolib](https://github.com/idya/oolib), License: _MIT_) by Zsolt Szloboda is a JavaScript object-oriented library that is conceptually similar to jQuery UI's Widget Factory.  It supports private methods, class inheritance, object initialisation and deinitialisation, super methods, and it's fairly small (min: 1.6K, gz: 0.7K).

It looks like this in practice:

{% highlight javascript %}
var MyClass = oo.createClass({
  _create: function(foo) {
    this.myField = foo;
  },

  _myPrivateMethod: function(bar) {
    return this.myField + bar;
  },

  myPublicMethod: function(baz) {
    return this._myPrivateMethod(baz);
  }
});

var MySubClass = oo.createClass(MyClass, {
  _myPrivateMethod: function(bar) {
    return this.myField + bar + 1;
  }
});
{% endhighlight %}
