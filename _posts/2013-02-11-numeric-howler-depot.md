---
layout: post
title: "Numeric JavaScript, howler.js, depot.js"
author: "Alex Young"
categories: 
- localStorage
- html5
- mathematics
- audio
---

###Numeric JavaScript

[Numeric JavaScript](http://numericjs.com/) (GitHub: [sloisel / numeric](https://github.com/sloisel/numeric), License: _MIT_) by Sébastien Loisel is a library that provides tools for matrix and vector calculations, convex optimisation, and linear programming.  This library was sent in by Emil Bay, who uses it for computationally intensive tasks like genetic programming and AI.  Emil says it's extremely fast, and the Numeric author has some [detailed benchmarks of Numeric](http://numericjs.com/benchmark.html) with comparisons against Closure and Sylvester.

###howler.js

![howler.js](/images/posts/howlerjs.png)

[howler.js](http://goldfirestudios.com/blog/104/howler.js-Modern-Web-Audio-Javascript-Library) (GitHub: [goldfire / howler.js](https://github.com/goldfire/howler.js), License: _MIT_) by James Simpson and GoldFire Studios is an audio library that works with Web Audio and HTML5 Audio.  Like similar libraries, it can automatically load the right file format for a given browser, but also comes with a bevy of other features as well.  It has an event-based API, and methods like `fadeIn` for handling some of the basic tasks you'll face when working with audio.

It implements a cache pool and automatically fetches the audio files, which explains why it seemed so fast when I played around with the examples.  It's implemented without any dependencies, and I noticed the source was consistently formatted and easy to follow.

###depot.js

depot.js (GitHub: [mkuklis / depot.js](https://github.com/mkuklis/depot.js), License: _MIT_, bower: _depot_) by Michal Kuklis is a `localStorage` wrapper that can be used with CommonJS or AMD, but also works with plain-old `script` tags.  To use it, define a store and then call methods on the store's instance:

{% highlight javascript %}
var todoStore = depot('todos');

todoStore.save({ title: 'todo1' });
todoStore.updateAll({ completed: false });

// Fetch all:
todoStore.all();
{% endhighlight %}

It comes with Mocha tests which can be run with PhantomJS.
