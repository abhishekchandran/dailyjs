---
layout: post
title: "Grasp, Optimizing AngularJS"
author: Alex Young
categories:
- angularjs
- search
- productivity
- optimisation
---

###Grasp

George Zahariev sent in his latest project, [Grasp](http://graspjs.com/) (GitHub: [gkz / grasp](https://github.com/gkz/grasp), License: _MIT_, npm: [grasp](https://npmjs.org/package/grasp)).  Grasp allows you to search and replace JavaScript code based on its abstract syntax tree.

> Unlike programs such as "grep" or "sed", it searches the structure behind your code, rather than simply the text you've written - this allows for much more powerful searches.

It uses a language inspired by CSS selectors for creating intuitive search expressions.  For example, given this code:

{% highlight javascript %}
var obj = {
  toEven: function(x) {
    if (isEven(x)) {
      return x;
    } else {
      return x + 1;
    }
  }
};

assert.equal(false, isEven(7));
{% endhighlight %}

Searching for `obj.props func! #isEven` would match the call to `isEven` inside the property `toEven` on the object `obj`.  References outside, like the assertion at the bottom, will not be matched.

My preferred solution for searching code is [The Silver Searcher](http://usevim.com/2013/10/16/ag/), but I like the idea of combining an AST with search and replace -- it seems like a potentially fertile ground for experimentation.

###Optimizing AngularJS: 1200ms to 35ms

In [Optimizing AngularJS: 1200ms to 35ms](http://blog.scalyr.com/2013/10/31/angularjs-1200ms-to-35ms/), optimisations for AngularJS are discussed.  It's actually a lot deeper than you might expect: it goes from caching DOM elements to bypassing watchers for hidden elements, and deferring element creation:

> A straightforward AngularJS implementation of the log view took 1.2 seconds to advance to the next page, but with some careful optimizations we were able to reduce that to 35 milliseconds. These optimizations proved to be useful in other parts of the application, and fit in well with the AngularJS philosophy, though we had to break few rules to implement them. In this article, we'll discuss the techniques we used.

> The conventional wisdom for AngularJS says that you should keep the number of data-bound elements below 200. With an element per word, we were far above that level.

> Using Chrome's JavaScript profiler, we quickly identified two sources of lag. First, each update spent a lot of time creating and destroying DOM elements.  Second, each word had its own change watcher, which AngularJS would invoke on every mouse click. This was causing the lag on unrelated actions like the navigation dropdown.

The post got a huge amount of interest, so the authors are working on open sourcing their AngularJS directives.
