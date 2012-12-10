---
layout: post
title: "Extender, Gridy.js, grunt-reduce"
author: Alex Young
categories:
- libraries
- build
- grunt
- tv
- browser
---

###Extender

[Extender](http://doug-martin.github.com/extender/) (GitHub: [doug-martin / extender](https://github.com/doug-martin/extender), npm: [extender](https://npmjs.org/package/extender), License: _MIT_) by Doug Martin is a library for making chainable APIs.  It works as a Node module or with RequireJS.

Extender has a `define` method that accepts a function and an object with methods that will form the API:

{% highlight javascript %}
function isString(obj) {
  return !isUndefinedOrNull(obj) && (typeof obj === "string" || obj instanceof String);
}

var myExtender =
  .define(isString, {
    multiply: function(str, times) {
      var ret = str, i;
      for (i = 1; i < times; i++) {
        ret += str;
      }
      return ret;
    },
    toArray: function(str, delim) {
      delim = delim || '';
      return str.split(delim);
    }
  });

myExtender('hello').multiply(2).value(); // hellohello
{% endhighlight %}

The author has included tests and lots of examples.  Although making chainable APIs is pretty straightforward, Extender might be a more explicit and testable way to do it.

###Gridy.js

![Gridy.js](/images/posts/gridyjs.png)

In the UK only one of my favourite shows is on Netflix.  The situation might be better in the US with Hulu, but if you're a cult TV fan outside of the US finding content can be challenging.  Even with a dearth of legitimate content sources, I'll always prefer hacking my TV to using locked down devices -- I had loads of fun this weekend with a Raspberry Pi and open source media projects.

One thing that's often lacking is cool web interfaces for media software.  Igor Alpert sent in [Gridy.js](http://ialpert.github.com/gridy.js/) (GitHub: [ialpert / gridy.js](https://github.com/ialpert/gridy.js)), which is a library designed for building media browser interfaces.  It includes tools for carousels, grids, and sliders.

Igor said he's tested it with the Samsung SDK, [Opera TV](http://dev.opera.com/tv), and Google TV for the LG and Vizio platforms.

###grunt-reduce

[grunt-reduce](https://github.com/Munter/grunt-reduce) by Peter Müller is a Grunt task for [AssetGraph](https://github.com/One-com/assetgraph) and other related projects from One.com.  AssetGraph is a Node-based module for optimising web pages.  By adding grunt-reduce to your project, you can bundle and minify assets, rename assets to MD5-sums of their content, optimise images, and even generate automatic CSS sprites.

Although AssetGraph doesn't currently work with AngularJS, Peter notes that this is being addressed: [#84: Support AngularJS templates](https://github.com/One-com/assetgraph/issues/84).

