---
layout: post
title: "Curl Converter, aja.js, sneakpeek"
author: Alex Young
categories:
- libraries
- utilities
- dom
- ui
- ajax
- rest
- http
---

###Curl Converter

Chrome's "Copy as cURL" menu item is useful, but what if you want to duplicate the same request with Node? [Curl Converter](http://curl.trillworks.com/#node) (GitHub: [NickCarneiro/curlconverter](https://github.com/NickCarneiro/curlconverter), License: _MIT_, npm: [curlconverter](https://www.npmjs.com/package/curlconverter)) by Nick Carneiro can convert between cURL syntax and Node's popular [request](https://www.npmjs.com/package/request) module.  It also supports Python, and can be installed with npm.

###aja.js

[aja.js](https://github.com/krampstudio/aja.js) (Bower: `aja`, npm: [aja](https://www.npmjs.com/package/aja), License: _MIT_) by Bertrand Chevrier is an Ajax library that supports JSON and JSONP.  It can be used to load large chunks of HTML or JSON, and can be installed with npm or Bower.

The API is fluent, so it can be used as a REST client like this:

{% highlight javascript %}
aja()
  .method('GET')
  .url('/api/customer')
  .data({ firstname: 'John Romuald' })
  .on('200', function(response) {})
  .go();
{% endhighlight %}

It also supports some DOM manipulation:

{% highlight javascript %}
aja()
  .url('/views/page.html')
  .into('.container')
  .go();
{% endhighlight %}

It comes with tests that can be run with Grunt, and the readme has more examples for things like posting data.

###sneakpeek

If you're looking for a library to hide the header when the page is scrolled, then [sneakpeek](http://htmlpreview.github.io/?https://github.com/antris/sneakpeek/blob/master/demo.html) (GitHub: [antris/sneakpeek](https://github.com/antris/sneakpeek), License: _MIT_, npm: [sneakpeek](https://www.npmjs.org/package/sneakpeek)) is nice because it's small, installable with npm, and has no external dependencies.

It's a bit like [headroom.js](https://github.com/WickyNilliams/headroom.js), but easier to use with Browserify.
