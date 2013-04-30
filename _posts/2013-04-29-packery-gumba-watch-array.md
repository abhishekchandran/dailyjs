---
layout: post
title: "Packery, Gumba, watch-array"
author: "Alex Young"
categories: 
- browser
- libraries
- ui
- arrays
- events
---

###Packery

![Packery](/images/posts/packery.png)

Victor sent in [Packery](http://packery.metafizzy.co/) (GitHub: [metafizzy / packery](https://github.com/metafizzy/packery), License: _MIT/Commercial_, bower: _packery_) from Metafizzy, which is a [bin packing](http://en.wikipedia.org/wiki/Bin_packing_problem) library.  It organises elements to fit around the space available.  Certain elements can be "stamped" into a specific position, fit an ideal spot, or be [draggable](http://packery.metafizzy.co/draggable.html).

Packery can be configured in JavaScript using the `Packery` constructor function, or purely in HTML using a class and data attributes.  jQuery is not required, but the project does have some dependencies, so the authors recommend installation with Bower.

The project can be used under the MIT license, but commercial projects require [a license that starts at $25](http://packery.metafizzy.co/license.html).

###Gumba

[Gumba](http://gumba.welldan97.com/) (GitHub: [welldan97 / gumba](https://github.com/welldan97/gumba), License: _MIT_, npm: [gumba](https://npmjs.org/package/gumba)) by Dmitry Yakimov is CoffeeScript for the command-line:

{% highlight text %}
$ echo '1234567' | gumba 'toNumber().numberFormat()'
1,234,567
{% endhighlight %}

It's a bit like Awk or sed, but for the chainable text operations supported by CoffeeScript and [Underscore.string](https://github.com/epeli/underscore.string).

###watch-array

watch-array (GitHub: [azer / watch-array](https://github.com/azer/watch-array), License: _BSD_, npm: [watch-array](https://npmjs.org/package/watch-array)) by Azer Koçulu causes arrays to emit events when mutator methods are used.  Usage is simple -- just call `watchArray` on an array, and pass it a callback that will be triggered when the array changes:

{% highlight javascript %}
var watchArray = require('watch-array');
var people = ['Joe', 'Smith'];

watchArray(people, function(update) {
  console.log(update.add);
  // => { 1: Taylor, 2: Brown }

  console.log(update.remove);
  // => [0]
});

people.shift();
people.push('Taylor', 'Brown');
{% endhighlight %}

In a way this is like a micro version of what data binding frameworks implement.  The author has included tests written with his [fox](https://github.com/azer/fox) test framework.

