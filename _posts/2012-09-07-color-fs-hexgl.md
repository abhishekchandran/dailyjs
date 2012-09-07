---
layout: post
title: "HexGL, one.color, fs.js"
author: "Alex Young"
categories: 
- webgl
- libraries
- html5
- filesystem
---

###HexGL

![HexGL](/images/posts/hexgl.png)

[HexGL](http://hexgl.bkcore.com/) is a WebGL-powered racing game similar in style to WipEout, developed by Thibaut Despoulain.  It's built using three.js, and is a pretty solid and fun game.  One aspect that impressed me is there's a selector for changing the quality, based on settings tailored for "Mobile", "Mainstream", and "Ultra" -- the author suggests that the game should always run at 60fps.

Thibaut is planning on open sourcing the game, [and his blog](http://bkcore.com/blog/index.html) has a feed so you can stay up to date that way or by following [@BKcore](https://twitter.com/BKcore) on Twitter.

###one.color

[one.color](https://github.com/One-com/one-color) (License: _BSD_, npm: [onecolor](https://npmjs.org/package/onecolor)) is a browser and Node colour manipulation library.  [Morgan Roderick suggested](https://twitter.com/mrgnrdrck/status/240711414883442688) this library on Twitter after seeing our jQuery Color coverage, and also pointed out that one of the creators has posted a video about it: [Peter Müller: One-color.js](http://video.copenhagenjs.dk/video/3712505/peter-mller-one-colorjs).

This library has a chainable API, supports alpha channels and colour names, and has Vows tests to back it all up.

###fs.js

[fs.js](https://github.com/OptimalBits/fs.js) (License: _MIT_, npm: [fs.js](https://npmjs.org/package/fs.js)) by Manuel Astudillo is a wrapper for the HTML5 File API, based on Node's `fs` module.  It's got some Mocha unit tests, and supports the use of prefixed file systems:

{% highlight javascript %}
var sizeInBytes = 1024 * 1024
  , prefix = 'filetest';

FSFactory.create(sizeInBytes, 'testfs', function(err, fs) {
  fs.read('foo', function(err, data){
    // data contains file contents.
  });
});
{% endhighlight %}
