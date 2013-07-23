---
layout: post
title: "jQuery Roundup: Audio Sort, Improving fn.on with Generic Function Overloading"
author: Alex Young
categories:
- jquery
- plugins
- ideas
- audio
- sort
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###Audio Sort

![Audio Sort](/images/posts/audiosort.png)

I've had a difficult week of dealing with Windows 8, IE, and Visual Studio, so forgive me if I don't indulge myself a little bit by writing about [Audio Sort](http://skratchdot.github.io/audio-sort/index.html) (GitHub: [skratchdot / audio-sort](https://github.com/skratchdot/audio-sort/), License: _MIT_).  It's written by "skratchdot" and is a visualisation of sort algorithms using jQuery, [D3.js](http://d3js.org/), [subcollider.js](http://mohayonao.github.io/subcollider.js/), and Bootstrap.

When it comes to sort visualisations, I don't think anything will beat [Quick-sort with Hungarian folk dance](http://www.youtube.com/watch?v=ywWBy6J5gz8) (thanks [Matias](https://twitter.com/mz2)) for sheer eccentricity, but it's a solid piece of work, and the inclusion of sound is somewhat idiosyncratic.

In a previous life I was also interested in audio programming, and [subcollider.js](http://mohayonao.github.io/subcollider.js/) is new to me.  If you've ever seen SuperCollider but prefer JavaScript's syntax then you may enjoy it.

###Improving fn.on with Generic Function Overloading

Sergii Kliuchnyk sent in [js-fn-overloading](https://github.com/redexp/js-fn-overloading):

> I looked at the code for the `Jquery.fn.on` method and realized how many methods they have which take different argument types.  They do many checks to change argument values to the right types. Here's my proposition for how to make the code clearer: [js-fn-overloading](https://github.com/redexp/js-fn-overloading) and here's an example of what `Jquery.fn.on` looks like with it: [jqueyr-on.js](https://github.com/redexp/js-fn-overloading/blob/master/examples/jquery-on.js)

The example in the readme is quite straightforward:

{% highlight javascript %}
var obj = {
  func: Overload('{Object|String}event, {String}[selector], {*}[data], {Function}fn', function(event, selector, data, fn){
    ok(this === obj);
    ok(typeof event === 'object' || typeof event === 'string');
    ok(typeof selector === 'undefined');
    ok(typeof data !== 'undefined');
    ok(typeof fn === 'function');
  });
};

obj.func('', 1, function(){});
{% endhighlight %}

The `Overload` function takes a configuration string which determines what types the overloaded methods should support, and how they should be mapped to arguments.
