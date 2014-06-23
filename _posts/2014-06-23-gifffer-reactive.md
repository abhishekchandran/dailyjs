---
layout: post
title: "Gifffer, Composing Discrete Events with RxJS"
author: "Alex Young"
categories:
- gif
- animation
- reactive
---

###Gifffer

Gifffer (GitHub: [krasimir / gifffer](https://github.com/krasimir/gifffer), License: _MIT_) by Krasimir Tsonev is a small library for adding a play control to animated gifs.  It works by drawing a play button over the image, and dynamically inserting an image element when play is clicked.  To prevent the gif from playing when the page loads, the `data-gifffer` attribute is used instead of the `src` attribute.

Krasimir has a blog with gifs that illustrate browser features, so he wanted to be able to handle playing gifs more elegantly than the default behaviour.  Here's an example: [Gifffer example](http://work.krasimirtsonev.com/git/gifffer/example/).  You can click it to toggle playback.

###Composing Discrete Events with RxJS

[Composing Discrete Events with RxJS](http://blog.bolshchikov.net/post/89367775878/composing-discrete-events-with-rxjs) by Sergey Bolshchikov is a post that compares `addEventListener` with RxJS.  If you've ever used Reactive Extensions then you should be at home with the use of `selectMany`, `combineLatest`, and so on.

Here's the full example:

{% highlight javascript %}
var mouseDowns = Rx.Observable.fromEvent(document, 'mousedown');
var mouseMoves = Rx.Observable.fromEvent(document, 'mousemove');
var mouseUps = Rx.Observable.fromEvent(document, 'mouseup');

var moves = mouseDowns.selectMany(function(md) {
  var start = {
    x: md.clientX,
    y: md.clientY
  };
  return mouseMoves.combineLatest(mouseUps, function(mm, mu) {
    var stop = {
      x: mu.clientX,
      y: mu.clientY
    };
    return {
      start: start,
      stop: stop
    };
  }).takeUntil(mouseUps);
});

moves.subscribe(function(res) {
  var body = document.querySelector('body');
  body.innerHTML = 'Start: x = ' + res.start.x + ', y = ' + res.start.y + '; Stop: x = ' + res.stop.x + ', y = ' + res.stop.y;
});
{% endhighlight %}


