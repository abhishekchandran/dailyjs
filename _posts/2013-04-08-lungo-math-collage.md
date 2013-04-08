---
layout: post
title: "LungoJS, Math.js, Collage"
author: "Alex Young"
categories: 
- mobile
- maths
- frameworks
- libraries
- ui
---

###LungoJS

![LungoJS](/images/posts/lungo.png)

[LungoJS](http://lungo.tapquo.com/) (GitHub: [TapQuo / Lungo.js](https://github.com/TapQuo/Lungo.js), License: _GPLv3_) from TapQuo is a framework for HTML5 apps that aims to be cross-device.  It supports mobile, desktop, and TV devices.  The [JavaScript API](http://lungo.tapquo.com/howto/core/) has support for working with the DOM, localStorage, caching, navigation routing, remote services, and views.

There's a [designer-focused tutorial](http://lungo.tapquo.com/docs/designers/) that explains how to create an application with Lungo, and a [Google group](https://groups.google.com/forum/#!forum/lungojs) (which currently requires permission to join).

###Math.js

[Math.js](http://mathjs.org/) (GitHub: [josdejong / mathjs](https://github.com/josdejong/mathjs), License: _Apache 2.0_, npm: _mathjs_, bower: _mathjs_) by Jos de Jong is a maths library for client-side JavaScript and Node.  It supports complex numbers, units, strings, arrays, and matrices, built-in functions and constants, as well as mathematical expression parsing.

It has no dependencies and is compatible with the built-in `Math` library.  One feature I particularly like is the expression parser:

{% highlight javascript %}
var parser = math.parser();
parser.eval('1.2 / (2.3 + 0.7)'); // 0.4
parser.eval('a = 5.08 cm');
parser.eval('a in inch');         // 2 inch
parser.eval('sin(45 deg) ^ 2');   // 0.5
{% endhighlight %}

This opens up some interesting possibilities for storing mathematical expressions in databases then safely evaluating them later on.

The project includes unit tests, and detailed documentation can be found in the readme file.

###Collage

[Collage](http://oztu.org/collage/) (GitHub: [ozanturgut / collage](https://github.com/ozanturgut/collage), License: _Apache 2.0_) by Ozan Turgut is a framework for creating interactive collages.  It can knit together remote APIs then present media in a two-dimensional space.

This example demonstrates some of the APIs that are supported as standard:

{% highlight javascript %}
var collage = Collage.create(document.getElementById('PopcornCollage'));
collage.load('popcorn media', {
  flickr: [{ tags: 'popcorn'}],
  googleNews: ['popcorn'],
  twitter: [{ query: 'popcorn' }]
}).then(function(){
  collage.start('popcorn media');
  collage.speed(8);
});
{% endhighlight %}

