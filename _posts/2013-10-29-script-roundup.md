---
layout: post
title: "Script Roundup: jWebAudio, Scrolling Component"
author: Alex Young
categories:
- jquery
- plugins
- browser
- audio
- scrolling
---

<div class="intro">
Note: You can send your scripts and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jWebAudio

[jWebAudio](http://01org.github.io/jWebAudio/) (GitHub: [01org / jWebAudio](https://github.com/01org/jWebAudio), License: _Apache 2.0_) by Wenli Zhang and published by Intel's Open Source Technology Center is an audio library focused on games:

> Web Audio seeks to process and synthesize audio in web applications. jWebAudio keeps the technical details of Web Audio under the hood and makes it easier to control your audio.

It has a jQuery API and also a framework-agnostic JavaScript API.  Playing a set of sounds looks like this:

{% highlight javascript %}
$('.sound').each(function() {
  var $this = $(this);
  var url = $this.data('sound');
  $(this).jWebAudio('addSoundSource', {
    url: url,
    preLoad: true,
    callback: function() {
      $this.jWebAudio('play');
    }
  });
});
{% endhighlight %}

jWebAudio also supports synthesis and effects:

> Sound effects include telephonize and cathedral currently. And you may create new sound effects using the combination of LOWPASS, HIGHPASS, BANDPASS, LOWSHELF, HIGHSHELF, PEAKING, NOTCH, ALLPASS.

There's a demo here: [jWebAudio demo](http://01org.github.io/jWebAudio/).

Wenli also writes about JavaScript.  Here's a post about the gruesome details of `Number`, `parseFloat`, and `parseInt`: [Converting To Numbers In JavaScript](http://zhangwenli.com/blog/2013/10/23/converting-to-numbers-in-javascript/).

###Scrolling.js Component

Guille Paz sent in [Scrolling.js Component](http://pazguille.github.io/scrolling/) (GitHub: [pazguille / scrolling](https://github.com/pazguille/scrolling), License: _MIT_, component: _pazguille/scrolling_).  It allows you to decouple scrolling from callbacks to avoid generating too many scroll events (the old debouncing issue):

{% highlight javascript %}
var scrolling = require('scrolling');

scrolling(document.querySelector('#box'), callback);
{% endhighlight %}

The project is distributed as a [component](https://github.com/component), and has a demo on the homepage.
