---
layout: post
title: "jQuery Roundup: SocialCount, Literally Canvas, Socrates"
author: Alex Young
categories:
- jquery
- plugins
- social
- markdown
- apps
- images
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###SocialCount

Social buttons can slow down page loading times due to a variety of reasons.  One solution is to lazy load them, and this is exactly what the [SocialCount](http://fgte.st/SocialCount/examples/index.html) (GitHub: [filamentgroup / SocialCount](https://github.com/filamentgroup/SocialCount/), License: _MIT_) from Filament Group does.  It can show "like" style buttons, counts, and lazy load the social network's original buttons.

It's designed using progressive enhancement techniques, and is tested against IE 7+, as well as the other major browsers, and various touchscreen devices.  It also includes QUnit tests.

###Literally Canvas

<div class="image">
  <img src="/images/posts/literallycanvas.png" alt="" />
  <small>Drawing with a trackpad is tricky business.</small>
</div>

[Literally Canvas](http://literallycanvas.com/) (GitHub: [literallycanvas / literallycanvas](https://github.com/literallycanvas/literallycanvas), License: _BSD_) by Stephen Johnson and Cameron Paul is a drawing widget built with jQuery and Underscore.js.  It has some basic drawing tools and can upload images to imgur.

The plugin accepts an options object that can be used to enable or disable certain features:

{% highlight javascript %}
$('.literally').literallycanvas({
  backgroundColor: 'rgb(255, 0, 0)', // default rgb(230, 230, 230)
  keyboardShortcuts: false,          // default true
  sizeToContainer: false,            // default true
  toolClasses: [LC.Pencil]           // see coffee/tools.coffee
});
{% endhighlight %}

###Socrates

<div class="image">
  <img src="/images/posts/socrates.png" alt="" />
  <small>Real-time Markdown editing with Socrates.</small>
</div>

[Socrates](http://socrates.io/) (GitHub: [segmentio / socrates](https://github.com/segmentio/socrates), License: _MIT_) by Ilya Volodarsky and Ian Storm Taylor is a Markdown editor and previewer.  It's built with jQuery, Backbone.js, and a client-side Markdown parser by Christopher Jeffrey.

The data is stored in [Firebase](https://www.firebase.com/), so you'll need an account with Firebase to install your own instance of Socrates.

