---
layout: post
title: "WDS2013, flyLabel.js"
author: Alex Young
categories:
- animation
- jquery
- webgl
---

###Web Directions South 2013 Opening Titles

![WDS2013](/images/posts/wds2013.png)

Hugh Kennedy sent in the [Web Directions South 2013 Opening Titles](http://run.south.im/) (GitHub: [smallmultiples / south.im](https://github.com/smallmultiples/south.im), _MIT, MPL and Creative Commons_).  This is an extremely impressive WebGL animation complete with a cool soundtrack.  It's partly demoscene inspired, but also reminds me of [Darwinia](http://www.introversion.co.uk/darwinia/).

> The code's open source, mostly MIT with a couple of files under the Mozilla Public License and assets under Creative Commons.

> Done in collaboration with Small Multiples' (http://small.mu) Jack Zhao and François Robichet, it's pushing some of the newer browser APIs quite a bit - WebGL, IndexedDB, Web Audio, Web Workers, etc.

###flyLabel.js

[flyLabel.js](http://athaeryn.github.io/flyLabel.js/) (GitHub: [athaeryn / flyLabel.js](https://github.com/athaeryn/flyLabel.js), License: _MIT_) by Mike Anderson is a jQuery plugin that adds fancy animations to form labels.  It uses CSS animations, and has a simple JavaScript API.  Mike's example uses Modernizr:

{% highlight javascript %}
if (Modernizr.input.placeholder) {
  $('body').flyLabels();
}
{% endhighlight %}

