---
layout: post
title: "Switchery, circles"
author: Alex Young
categories:
- browser
- ui
- iOS
- graphs
---

###Switchery

![Switchery](/images/posts/switchery.gif)

[Switchery](http://abpetkov.github.io/switchery/) (GitHub: [abpetkov / switchery](https://github.com/abpetkov/switchery), License: _MIT_, bower: _switchery_) by Alexander Petkov is a checkbox replacement, inspired by iOS 7, complete with animations.

The basic usage is `new Switchery(elem)`.  You can pass extra options for the disabled state, the colour, and the animation speed.

Switchery is written using CommonJS modules, but Alexander builds a [standalone version](https://github.com/abpetkov/switchery/blob/master/standalone/switchery.js) that doesn't need `require`.

###Circles

![Circles](/images/posts/circles-graphs.png)

Circles (GitHub: [lugolabs / circles](https://github.com/lugolabs/circles), License: _MIT_) by Artan Sinani is a small script for creating circular graphs.  It doesn't have any dependencies, and can be used like this:

{% highlight javascript %}
Circles.create({
  id:         'circles-1',
  percentage: 43,
  radius:     60,
  width:      10,
  text:       7.13,
  colors:     ['#D3B6C6', '#4B253A']
});
{% endhighlight %}

