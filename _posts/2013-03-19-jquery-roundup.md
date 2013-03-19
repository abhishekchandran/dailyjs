---
layout: post
title: "jQuery Roundup: Panzoom, jQuery.Feedback, shurikenJS"
author: Alex Young
categories:
- jquery
- plugins
- animation
- frameworks
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Panzoom

Panzoom (GitHub: [timmywil / jquery.panzoom](https://github.com/timmywil/jquery.panzoom/), License: _MIT_) by Timmy Willison is a plugin for adding panning and zooming behaviour to an element.  It works in jQuery 1.9+, and uses CSS transforms and matrix functions to take advantage of GPU acceleration where available.

Any element can be potentially panned or zoomed, including Canvas and videos.  It supports touch gestures, including pinch, so it should work well in a mobile project.

There's a [demo in the form of Panzoom's unit tests](http://timmywil.github.com/jquery.panzoom/test/).

###jQuery.Feedback

[jQuery.Feedback](http://siong1987.com/jquery.feedback/) (GitHub: [siong1987 / jquery.feedback](https://github.com/siong1987/jquery.feedback), License: _MIT_) by Teng Siong Ong is a clone of the feedback widget found on [Branch](http://branch.com/).  It has some nice CSS transform animations, and just expects a callback for handling sending the resulting message.

###shurikenJS

![shurikenJS](/images/posts/shuriken.png)

[shurikenJS](http://shurikenjs.com/) (GitHub: [shurikenjs](https://github.com/shurikenjs), License: _MIT_) by Stephan Fischer is a JavaScript framework that uses recent ECMAScript methods and an API based around native DOM objects.  The `Node` object is enhanced with new chainable methods, for example: `Node.css('color', 'red').hide().show()`.

Stephan hasn't included any tests yet, but I've included it here because it's so different to jQuery it should get you thinking.  The combination of modern ECMAScript with native DOM code is an interesting approach to client-side development.
