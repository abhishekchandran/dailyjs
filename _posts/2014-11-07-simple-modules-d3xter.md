---
layout: post
title: "Simple Modules, D3xter"
author: "Alex Young"
image: "/images/posts/d3xter.png"
categories:
- sql
- modules
- libraries
- graphics
- graphs
---

###Simple Modules

If you've got legacy JavaScript that's badly structured, then one early refactoring strategy that can help is to add modules.  However, you might not be sure about the specific module system or framework that you'll eventually switch to, so what do you do?

George Mauer sent in simple-modules (GitHub: [togakangaroo/simple-modules](https://github.com/togakangaroo/simple-modules), License: _MIT_, Bower: _simple-modules_), a tiny module system that lets you `define` modules and then `require` them.  There's an [example](http://jsbin.com/tiriz/watch?js,console) that shows the main features, including a test for circular dependency detection.

George wrote an article about [converting legacy code](http://togakangaroo.github.io/2014/10/31/use-simple-modules-1.html), which shows how to include Simple Modules on the page and then how to identify possible modules.

###D3xter

![D3xter](/images/posts/d3xter.png)

D3xter (GitHub: [NathanEpstein/D3xter](https://github.com/NathanEpstein/D3xter), License: _MIT_, Bower: _d3xter_) by Nathan Epstein is a D3.js-based library for plotting graphs.  The functions in the library return SVG objects, so you can further customise them with the standard D3 API.

D3xter's built-in graphs should work well with minimal configuration, so if you're looking for a D3-friendly library then this one might be a good choice.  For example, given arrays of co-ordinates, you can plot a line graph like this:

{% highlight javascript %}
var lineGraph = xyPlot(index, y);
{% endhighlight %}

The readme has an additional example that shows how to query the resulting object with D3 and modify the colours.
