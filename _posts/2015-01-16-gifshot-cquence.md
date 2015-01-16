---
layout: post
title: "Gifshot, Cquence.js"
author: Alex Young
image: "/images/posts/gifshot.png"
categories:
- libraries
- animations
---

###Gifshot

![Gifshot](/images/posts/gifshot.png)

[Gitshot](http://yahoo.github.io/gifshot/) (GitHub: [yahoo/gifshot](https://github.com/yahoo/gifshot), License: _MIT_) by Chase West and Greg Franko at Yahoo Sports is a library for creating animated GIFs from video streams or images.  It's client-side and uses Web Workers, so you can use it with existing sites without too much server-side work.  To generate GIFs themselves it uses lots of modern APIs, like WebRTC, FileSystem, Video, Canvas, Web Workers, and (everyone's favourite!) Typed Arrays.

Gifshot is ideal for adding overlays to animations, or for extracting thumbnails from videos.  You could capture footage from the webcam and share it to users as part of a chat service or game, for example.  It comes with a demo that uses Node, so you can easily see the kinds of options it supports.

The basic API is just `gifshot.createGIF`, which accepts an options object that specifies the type of content.  For example, generating a GIF from a video stream can be done with `gifshot.createGIF({ video: ['example.mp4', 'example.ogv'] })`.

###Cquence.js

Cquence.js by Ramon Gebben (GitHub: [RamonGebben/Cquence](https://github.com/RamonGebben/Cquence), License: _MIT_) is a small animation library.  The author developed it for advertising banners, and it has an interesting compositional style:

{% highlight javascript %}
var render = combine(
  sequence(
    sleep(100),
    linear('frame3', 10000, { left: -900 }, { left: 300 })
  ),
  sequence(
    easeOut('frame1', 2000, { left: -1000 }, { left: 120 }),
    // ...
{% endhighlight %}

It goes against that "globals are bad" API style, but it would be possible to repackage it as a CommonJS module.  It uses `requestAnimationFrame` and has older IE support for opacity.

There's a [demo](http://ramongebben.github.io/Cquence/) that demonstrates the kind of sequential animations you can build up with it.
