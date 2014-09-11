---
layout: post
title: "BiMap, jQuery breakpoint"
author: "Alex Young"
categories:
- jquery
- responsive
- data
- modules
- libraries
- node
---

###BiMap

BiMap (GitHub: [alethes / bimap](https://github.com/alethes/bimap), License: _MIT_, npm: [bimap](https://www.npmjs.org/package/bimap)) by James Daab is a bidirectional map implementation.  This is a data structure that allows you to query for values by keys and keys by values:

{% highlight javascript %}
bimap.push({
  a: {
    b: 1,
    c: {
      d: 2
    }
  }
});
bimap.key('a.b'); // => 1
bimap.val(2); // => "a.c.d"
{% endhighlight %}

###jQuery breakpoint

jQuery breakpoint (GitHub: [joshbambrick / breakpoint](https://github.com/joshbambrick/breakpoint), License: _MIT_) by Joshua Bambrick is a plugin for tracking page resizes, and is ideal for when you need JavaScript to trigger in a responsive design.

You can attach listeners with `$.breakpoint.on`, and an array is accepted so you can respond to different preset device sizes.  There's also `$.breakpoint.off` for removing listeners, and `$.breakpoint.changeBreakpoints` for changing the globally recognised device sizes.
