---
layout: post
title: "Layer, Thorax, Emacs.js, Chrome OS Dev"
author: "Alex Young"
categories: 
- libraries
- node
- proxies
- editors
- backbone.js
- chrome-os
---

###Layer

Layer (GitHub: [lovebear / layer](https://github.com/lovebear/layer), License: _BSD_, npm: [layer](https://npmjs.org/package/layer)) by "lovebear" is a module for creating proxies without changing existing code.  Given a function, it can augment it with another function that will run first.  The returned values from the new function will be supplied as arguments to the original function.

The author's example looks like this:

{% highlight javascript %}
// add a simple proxy without modifying any existing code!
var addBig = function(x, y) {
  x = x * 100;
  y = y * 100;
  return [x, y];
}
layer.set(null, add, addBig);

// existing code...
function add(x, y) {
  return x + y;
}

add(2, 2); // 400
{% endhighlight %}

The `layer.set` method is used to invoke `addBig` _before_ `add`, and passes the arguments to `add`.  If you look at the source you'll notice that the author has left a note saying "what if the return value isn't an arrray?", but it seems like the proxy functions should always map return values to the original function's arguments.

Layer works in both Node and browsers.

###Thorax

[Thorax](http://thoraxjs.org/) (GitHub: [walmartlabs / thorax](https://github.com/walmartlabs/thorax), License: _MIT_, npm: [thorax](https://npmjs.org/package/thorax)) by Ryan Eastridge and Kevin Decker is another Walmart Labs project that brings together Backbone and Handlebars to provide an "opinionated, battle tested framework for building large scale web applications".

Thorax has some sugar to help with tasks like data binding and events.  Descendants of `Thorax.View` automatically have their properties mapped to template variables, and binding a model will cause the model's attributes to be bound.  Models and collections can also trigger view events, and events are inheritable.

Collections can also be rendered using the `collection` keyword in the template, and the views will stay current as models in the collection change.

It seems like Thorax fits in with my particular way of working with Backbone, and it looks like it might cut down a lot of the boilerplate I find myself writing so I'm going to give it a go.

###emacs.js

If you're looking for an easy to use solution for JavaScript development in Emacs, then take a look at emacs.js (GitHub: [azer / emacs.js](https://github.com/azer/emacs.js)) by Azer Koculu.  It comes with tools for npm, syntax checking and highlighting for JavaScript and CoffeeScript, and some snippets and autocompletion.

Azer make a screencast about it here: [emacs.js screencast](http://www.youtube.com/watch?v=4iSfLy8qfbM).

###Chrome OS Development Follow Up

After I wrote about the [Chromebook Pixel](http://dailyjs.com/2013/02/25/chromebook-pixel-testing/) last week, I noticed a post in the Google+ Chromebook community about [creating a Chrome OS development environment](https://code.google.com/p/chromium/issues/detail?id=149036):

> We really need to design and implement a proper application, extension, and theme development environment.

> It could be implemented as a web ui page, as chrome://extensions/ is today, or even cooler, it could conceivably be its own packaged application.

My opinion on this is they should find a Chrome OS "native" way of making our existing development tools more accessible.  I think being able to run Node and Vim/Emacs natively and sensibly on Chrome OS would be huge.  I'm actually doing that in developer mode -- Chrome OS is my GUI and I do development in a shell with Vim and tmux.
