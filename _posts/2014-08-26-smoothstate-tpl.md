---
layout: post
title: "jquery.smoothstate.js, underscore-tpl"
author: "alex young"
categories:
- libraries
- ui
- jquery
- animation
---

###jquery.smoothState.js

[jquery.smoothState.js](http://weblinc.github.io/jquery.smoothState.js/index.html) (GitHub: [weblinc / jquery.smoothState.js](https://github.com/weblinc/jquery.smoothState.js), License: _MIT_) by Miguel Angel Perez promises to improve the early page loading experience by reducing the amount of sudden visual cuts.

By using unobtrusive JavaScript, jquery.smoothState.js loads content asynchronously and updates the URL with `history.pushState`.  Animations are used as a visual cue to indicate when the main page content has been replaced.

The project's documentation uses these techniques, but [take a look at the demo](http://weblinc.github.io/jquery.smoothState.js/demos/typical/index.html) for a more basic example to get started.

###underscore-tpl

underscore-tpl (GitHub: [creynders / underscore-tpl](https://github.com/creynders/underscore-tpl), License: _MIT_) by Camille Reynders allows you to expand placeholders stored within objects:

{% highlight javascript %}
var config = {
  baz: '<%= qux.mofo %>',
  major: {
    badass: '<%= badass %>'
  },
  '<%= foo %>': 'bar'
{% endhighlight %}

It can use mustache-style tags instead of ERB, and accepts the same options as <a href="http://lodash.com/docs#templateSettings">_.templateSettings</a>.

I've found myself using this type of thing for generating seed data or fixtures in tests, but I imagine it might also be useful if you're passing plain objects around with data-binding libraries as well.
