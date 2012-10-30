---
layout: post
title: "jQuery Roundup: jQuery UI 1.9.1, IndexedDB on Cordova, Backbone.ViewKit"
author: Alex Young
categories:
- jquery
- jquery-ui
- indexeddb
- backbone.js
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery UI 1.9.1

[jQuery UI 1.9.1](http://blog.jqueryui.com/2012/10/jquery-ui-1-9-1/) was released a few days ago.  This is a maintenance release that includes bug fixes for many widgets and the core library.  The [jQuery UI 1.9.1 Changelog](http://jqueryui.com/changelog/1.9.1/) has full details of the fixes.

###Bootstrap 2.2.0

![Bootstrap 2.2.0 templates](/images/posts/bootstrap-templates.png)

[Bootstrap 2.2.0](http://blog.getbootstrap.com/2012/10/29/bootstrap-2-2-0-released/) is out.  This version includes much needed additional templates, a media component, a new variable-driven typographic scale, and other more minor tweaks.

###IndexedDB on Cordova

Parashuram Narasimhan has got his IndexedDB polyfill working on on Cordova.  This means it can be used with iOS and Android applications:

* [IndexedDB Example on Cordova - Android](http://blog.nparashuram.com/2012/10/indexeddb-example-on-cordova-phonegap_12.html)
* [IndexedDB Example on Cordova - iOS](http://blog.nparashuram.com/2012/10/indexeddb-example-on-cordova-phonegap.html)

Parashuram's posts include details on the techniques he uses to get IndexedDB working on each platform.  For example, with Android he currently has to use JavaScript to inject the polyfill during the `deviceready` event.

###Backbone.ViewKit

[Backbone.ViewKit](https://github.com/scttnlsn/backbone.viewkit) (License: _MIT_) by Scott Nelson is a Backbone.js plugin for managing views with transitions in an iOS-inspired fashion.  It adds `Backbone.ViewKit.ViewPort` which renders sets of views, displaying one at a time.  Stacks of views are managed using `Backbone.ViewKit.ViewStack`, which allows views to be pushed or popped as required.

Transition animations can be triggered using `Backbone.ViewKit.Transition`:

{% highlight javascript %}
new Backbone.ViewKit.Transitions.Slide({
   reverse: false
 , duration: 0.4
 , easing: 'ease-out'
 , delay: 0
});
{% endhighlight %}

There's a demo here: [Backbone.ViewKit demo](http://fiddle.jshell.net/scttnlsn/xQxRY/show/).
