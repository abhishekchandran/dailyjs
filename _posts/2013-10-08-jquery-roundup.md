---
layout: post
title: "jQuery Roundup: Ideal Forms 3, httpinvoke, jquery.brightness.js"
author: Alex Young
categories:
- browser
- server
- node
---

###Ideal Forms 3

Ideal Forms 3 (GitHub: [elclanrs / jq-idealforms](https://github.com/elclanrs/jq-idealforms), License: _GPL/MIT_) by Cedric Ruiz is a library for working with responsive HTML5 forms.  It uses JavaScript to adapt form controls to the size of the container, so it works without using media queries.  It supports keyboard shortcuts, custom checkboxes and file inputs, and a date picker.

The CSS now uses Stylus, and it uses classes in the HTML markup for denoting field types.

###httpinvoke

httpinvoke (GitHub: [jakutis / httpinvoke](https://github.com/jakutis/httpinvoke), License: _MIT_, npm: [httpinvoke](https://npmjs.org/package/httpinvoke), bower: _httpinvoke_) by Vytautas Jakutis is a module for making HTTP requests that works with Node and browsers.  It's designed with a focus on promises, and Node's callback-style API:

{% highlight javascript %}
httpinvoke('http://example.org', 'GET').then(function(res) {
  console.log('Success', res.body, res.statusCode, res.headers);
}, function(err) {
  console.log('Failure', err);
});
{% endhighlight %}

The readme has full documentation for each API style and the accepted options.  It's unit tested, and also available through Bower.

###jquery.brightness.js

[jquery.brightness.js](https://gist.github.com/kozo002/6806421) is a small plugin by Kozo Yamagata that detects CSS background colours and returns the brightness.  Calling `$(selector).brightness()` returns either `'light'` or `'dark'`.  It's distributed as a Gist as it's a short and sweet little snippet.
