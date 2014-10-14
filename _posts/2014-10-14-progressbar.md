---
layout: post
title: "Make Slicker Progress Bars with ProgressBar.js"
author: "Alex Young"
image: "/images/posts/progressbarjs.gif"
categories:
- ui
- design
- libraries
---

![ProgressBar.js](/images/posts/progressbarjs.gif)

Kimmo Brunfeldt sent in [ProgressBar.js](http://kimmobrunfeldt.github.io/progressbar.js/) (GitHub: [kimmobrunfeldt / progressbar.js](https://github.com/kimmobrunfeldt/progressbar.js), License: _MIT_, Bower: _progressbar.js_), a library for creating responsive progress bars.  It uses animated SVG paths, so the results look very clean and cool.

The library has some built in shapes: Line, Circle, and Square.  You can provide properties that are used to style the elements:

{% highlight javascript %}
var element = document.getElementById('example-line-container');

var line = new ProgressBar.Line(element, {
  color: '#FCB03C',
  trailColor: '#aaa'
});

line.animate(1, function() {
  line.animate(0);
});
{% endhighlight %}

If you want to include a number in the progress bar, then you can just set the text of a node.  There's a clock example in the documentation that does this:

{% highlight javascript %}
var element = document.getElementById('example-clock-container');
element.innerHTML = '<header id="clock-seconds"></header>';
var textElement = document.getElementById('clock-seconds');

var seconds = new ProgressBar.Circle(element, {
  duration: 200,
  color: '#FCB03C',
  trailColor: '#ddd'
});

setInterval(function() {
  var second = new Date().getSeconds();
  seconds.animate(second / 60, function() {
    textElement.innerHTML = second;
  });
}, 1000);
{% endhighlight %}

You can also add arbitrary shapes with `ProgressBar.Path`.  There's a really nice example that uses the Plough (Big Dipper) and connects each star together.

Part of the magic behind the animation in ProgressBar.js is powered by [Shifty](http://jeremyckahn.github.io/shifty/).  This is a tweening engine created by Jeremy Kahn which can "tween" numbers or even CSS strings.

I really like the look of the progress bars Kimmo has used in the documentation, so I expect these will start appearing on websites soon.
