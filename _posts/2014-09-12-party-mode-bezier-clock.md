---
layout: post
title: "Party Mode, Bézier Clock"
author: "Alex Young"
categories:
- d3
- audio
---

###Party Mode

![Party Mode](/images/posts/partymode.png)

[Party Mode](http://preziotte.com/partymode/) (GitHub: [preziotte / party-mode](https://github.com/preziotte/party-mode), License: _MIT_) by Mathew Preziotte is a music visualiser with a slick UI and lots options.  If you press `m` it'll show a menu for each visual effect, and there's also a keyboard icon near the bottom of the screen that documents each shortcut.

The author built it with d3.js and the [Web Audio API](http://www.w3.org/TR/webaudio/).

> Using the web audio api, I can get an array of numbers which corresponds to the waveform of the sound an html5 audio element is producing. There's a [good tutorial](http://www.developphp.com/view.php?tid=1348) on how to do this. Then, using `requestAnimationFrame` (with a little frame limiting for performance reasons) I'm updating that array as the music changes. I then normalize the data a bit (or transform it slightly depending on the visualization) and redraw the screen based on the updated array. I'm using d3.js to draw and redraw SVG based on this normalized data. Each visualization uses the data a bit differently -- it was mostly trial and error to get some stuff I liked looking at.

###Bézier Clock

Jack Frigaard sent in his [Bézier Clock](http://jackf.net/bezier-clock/), which got lots of attention on Hacker News this week.  It's made with [Processing.js](http://processingjs.org/), which is loads of fun to play with, and you can click it to visualise the curve splines and poitns.

There are keyboard options as well:

* `space`: Toggle continual animation
* `s`: Show intermediate figures and the standard ones
* `a`: Cycle through linear, quadratic, cubic and sinusoidal easing
