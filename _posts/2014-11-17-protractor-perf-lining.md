---
layout: post
title: "Protractor-perf, lining.js"
author: "Alex Young"
image: "/images/posts/liningjs.png"
categories:
- libraries
- testing
- performance
- angularjs
---

###Protractor-perf

[Protractor-perf](http://blog.nparashuram.com/2014/11/protractor-perf-performance-regression.html) (GitHub: [axemclion/protractor-perf](https://github.com/axemclion/protractor-perf), License: _MIT_, npm: [protractor-perf](https://www.npmjs.org/package/protractor-perf)) by Parashuram can help you test for performance regressions while running [Protractor](https://github.com/angular/protractor) AngularJS tests.

To use it, you can add performance-based assertions that are ignored by Protractor.  These performance statements will only be used when tests are run with the `protractor-perf` command-line tool.

The available metrics are quite sophisticated -- for a list of metrics take a look at the [browser-perf metrics](https://github.com/axemclion/browser-perf/wiki/Metrics).  Some examples are `evaluateScript` (the time spent evaluating the page's scripts) and `meanFrameTime` (average time taken to render each frame).

###Lining.js

[Lining.js](http://zencode.in/lining.js/) (GitHub: [zmmbreeze/lining.js](https://github.com/zmmbreeze/lining.js), License: _MIT_) by mzhou is a library for addressing lines within an element.  To use it, add the `data-lining` attribute to an element, then add CSS to style each line.  You can even apply styles to ranges with the `data-from` and `data-to` attributes.

There's a JavaScript API which is event based.  For example:

{% highlight javascript %}
var poem = document.getElementById('poem');

poem.addEventListener('beforelining', function(e) {
  // prevent lining if you want
  e.preventDefault();
}, false);

var poemLining = lining(poem, {
  autoResize: true,
  from: 2,
  to: 3,
  lineClass: 'my-class'
});
{% endhighlight %}

The author suggests that it can be used for creative typography, and poems are used in the documentation which is a nice example.  It also supports effects, so you can do things like animate sections of text using transitions.
