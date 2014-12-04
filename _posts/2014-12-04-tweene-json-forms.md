---
layout: post
title: "Tweene, JSON Forms"
author: "Alex Young"
image: "/images/posts/tweene.png"
categories: 
- libraries
- animation
- json
- forms
---

### Tweene

[Tweene](http://tweene.com/) (GitHub: [SkidX/tweene](https://github.com/SkidX/tweene), License: _Artistic License 2.0_, npm: [tweene](https://www.npmjs.org/package/tweene), Bower: _tweene_) by Federico Orrù is an API that wraps around popular animation libraries so you can switch implementation more easily.  Rather than having to worry about whether you need to use `translateX` or just `x`, you can use Tweene's API instead.

These are the [supported libraries](http://tweene.com/html/libraries/) right now:

* [GSAP](https://github.com/greensock/GreenSock-JS/)
* [Transit](https://github.com/rstacruz/jquery.transit)
* [Velocity.js](https://github.com/julianshapiro/velocity/)
* jQuery

To create animations, you have to make tween instances using `Tweene`, and then call methods that set the duration and easing.  It actually has several API styles based on GASP, jQuery, and Velocity, but I prefer the fluent API:

{% highlight javascript %}
Tweene.get($target)
  .to({ opacity: 0, left: '+=50px' })
  .duration(500)
  .easing('easeOutQuad')
  .on('complete', completeCallback)
  .play();
{% endhighlight %}

The documentation for Tweene is detailed, and there are some [examples on CodePen](http://codepen.io/collection/KriHc/).

###jQuery JSON HTML Forms

Cezary Wojtkowski sent in [jquery-html-json-forms](https://github.com/cezary/jquery-html-json-forms), a project that aims to support the [W3C HTML JSON form submission specification](http://www.w3.org/TR/html-json-forms/):

> This specification defines a new form encoding algorithm that enables the transmission of form data as JSON. Instead of capturing form data as essentially an array of key-value pairs which is the bread and butter of existing form encodings, it relies on a simple name attribute syntax that makes it possible to capture rich data structures as JSON directly.

This basically means you can use an `enctype` attribute of `application/json` in forms.  This makes it a lot easier to create forms that send data to JSON APIs, rather than using the standard form encoding.

Cezary's project allows you to use `enctype='application/json'` and then get JSON out with `$(formElement).JSONencode()`.  You can also enable and disable the plugin.

The HTML JSON form specification is new to me, but it seems really cool for those of us who create lots of JSON APIs.
