---
layout: post
title: "jQuery Roundup: Touch-box, Elevate Zoom, textareaHelper"
author: Alex Young
categories:
- jquery
- plugins
- images
- zoom
- touchscreen
- textarea
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Touch-box

Dannie Hansen sent in [Touch-box](http://danniehansen.com/touch_box/) (GitHub: [danniehansen / Touch-box](https://github.com/danniehansen/Touch-box), License: _GPL_), a plugin for resizing and dragging elements on touchscreen devices.  Although the documentation mentions iPad, I tested it on Android Chrome and both seemed to work well.

Dannie suggested an interesting idea for a gallery, where the resize event could automatically cause higher resolution images to be fetched through a callback:

{% highlight javascript %}
$('.box').TouchBox({
  resize: true,
  drag: true,
  callback_touches: function(touches) {
  },
  callback_change: function() {
  }
});
{% endhighlight %}

###Elevate Zoom

<div class="image">
  <img src="/images/posts/elevatezoom.png" alt="" />
  <small>Elevate Zoom's tint feature.</small>
</div>

[Elevate Zoom](http://www.elevateweb.co.uk/image-zoom) (GitHub: [elevateweb / elevatezoom](https://github.com/elevateweb/elevatezoom), License: _MIT/GPL_) by Andy Eades is an image zoom plugin that has FancyBox support.  It has some cool features like "tinting", where the unzoomed portion of the image is tinted -- [demos are available](http://www.elevateweb.co.uk/image-zoom/examples) for each of the main features.

###textareaHelper

[textareaHelper](https://github.com/Codecademy/textarea-helper) by Amjad Masad and Codecademy transparently copies a `textarea`'s contents into a `div`, so it can be manipulated in ways not supported by `textarea`.  It will try to copy the styles from the `textarea` as well, and can fetch the caret's position.

Mocha tests have been included, which includes a `setSelectionRange` implementation to test the caret handling.

