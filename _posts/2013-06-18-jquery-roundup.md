---
layout: post
title: "jQuery Roundup: Magnific Popup, blend.js"
author: Alex Young
categories:
- jquery
- plugins
- graphics
- images
- lightbox
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Magnific Popup

![Magnific Popup](/images/posts/magnific-popup.png)

[Magnific Popup](http://dimsemenov.com/plugins/magnific-popup/) (GitHub: [dimsemenov / Magnific-Popup](https://github.com/dimsemenov/Magnific-Popup), License: _MIT_, jQuery: [magnific-popup](http://plugins.jquery.com/magnific-popup/)) by Dmitry Semenov is a responsive lightbox plugin that should work with mobile devices and also Zepto.js.  It's modular and has a build tool so you can generate a build that only includes the features you need.  Sass is used for CSS, so you could easily customise the styles to suit your project.

Keyboard shortcuts are supported, the arrow keys and escape allow images to be navigated -- see the [gallery demo](http://codepen.io/dimsemenov/pen/vKrqs) for an example of this.

A lot of the work is done by CSS, which means high DPI displays are supported:

> Default controls are made with pure CSS, without external graphics. For the main image there is a built in way to provide appropriate source for different pixel density displays.

Content other than images is supported as well.  The documentation has examples of using Magnific Popup with Google Maps and videos.  For more information, see [the Magnific documentation](http://dimsemenov.com/plugins/magnific-popup/documentation.html).

###blend.js

[blend.js](http://www.qur2.eu/blend.js/) (GitHub: [qur2 / blend.js](https://github.com/qur2/blend.js), License: _MIT_) by Aurélien Scoubeau applies effects to images using Canvas.  The effects themselves are functions that receive pixels.  Processing is applied to sections of the image in a two-dimensional grid.

Custom parameters can be passed to blending functions:

{% highlight javascript %}
// Create some effects that will use additional arguments
var colorfx = blend.cfx(function(color, context) { return context; });
var anglefx = blend.pfx(function(angle, radius, pixels) { return pixels; });

blender.fx(colorfx, 'rgb(255, 123, 123)').fx(anglefx, [Math.PI, .25]);
blender.fx(colorfx, '#FFF', '#AAA', '#666', '#111');

// Null is used to skip zones
blender.fx(colorfx, '#FFF', null, null, '#111');

// Update the image
blender.update();
{% endhighlight %}

There are some bundled effects as well: desaturate, neutralize, vignette, and contrast.  These can be found under `blend.fx`.

The author has included Mocha tests which can be ran in a browser here: [blend.js/test.html](http://www.qur2.eu/blend.js/test.html).
