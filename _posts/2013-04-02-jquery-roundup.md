---
layout: post
title: "jQuery Roundup: Sidr, Huey, Backbone.Advice"
author: Alex Young
categories:
- jquery
- plugins
- backbone.js
- graphics
- components
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Sidr

![Sidr](/images/posts/sidr.png)

[Sidr](http://www.berriart.com/sidr/) (GitHub: [artberri / sidr](https://github.com/artberri/sidr), License: _MIT_) by Alberto Varela creates menus that look like the sidebars found in recent iOS apps.  It can cope with multiple menus on a page, and can load content remotely.  It's also responsive, so it should work well in mobile projects.

The author has written up documentation complete with demos, and has included a Grunt build script.  It seems like the exact sort of UI component that the next great web-based RSS reader might use...

###Huey

[Huey](http://michaelrhodes.github.com/huey/) (GitHub: [michaelrhodes / huey](https://github.com/michaelrhodes/huey), License: _MIT_) by Michael Rhodes will find the dominant colour of an image and return it as an RGB array.  This is all performed client-side, and doesn't even depend on jQuery.  It could be used to create the kind of effect seen in iTunes, where the background colour changes to suit the selected album art.

###Backbone.Advice

Backbone.Advice (GitHub: [rhysbrettbowen / Backbone.Advice](https://github.com/rhysbrettbowen/Backbone.Advice), License: _MIT_) by Rhys Brett-Bowen is a Backbone plugin based on Angus Croll's [advice pattern](http://javascriptweblog.wordpress.com/2011/05/31/a-fresh-look-at-javascript-mixins/).  It basically adds functional mixins to Backbone objects, and can be wrapped like this:

{% highlight javascript %}
Backbone.Advice.addMixin(Backbone.Views);
{% endhighlight %}

Rhys sent in a whole bunch of other Backbone-related projects, including [Backbone.ComponentView](https://github.com/rhysbrettbowen/Backbone.ComponentView) and [Backbone.ModelRegistry](https://github.com/rhysbrettbowen/Backbone.ModelRegistry).  Backbone.ComponentView is based on [goog.ui.component](http://closure-library.googlecode.com/svn/docs/class_goog_ui_Component.html) from Closure Library, and also works with Backbone.Advice.
