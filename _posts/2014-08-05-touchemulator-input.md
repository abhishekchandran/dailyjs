---
layout: post
title: "Touch Emulator, Input by Font Bureau"
author: "Alex Young"
categories:
- libraries
- ui
- mobile
- fonts
---

###Touch Emulator

When working with iOS applications, the gesture shortcuts in the simulator quickly become second nature.  Sometimes I use the iOS Simulator for web development purely to check responsive designs, mainly because it starts up more quickly than the Android emulator.  [Touch Emulator](http://hammerjs.github.io/touch-emulator/) (GitHub: [hammerjs / touchemulator](https://github.com/hammerjs/touchemulator), License: _MIT_) from Hammer.js is a way to emulate multi-touch events on the desktop, based on the W3C specifications.

Once it's installed you can listen for events in the standard way:

{% highlight javascript %}
document.body.addEventListener('touchstart', log, false);
document.body.addEventListener('touchmove', log, false);
document.body.addEventListener('touchend', log, false);
{% endhighlight %}

[The demo](http://rawgit.com/hammerjs/touchemulator/master/tests/manual/hammer.html) is what reminded me of the iOS Simulator -- you can press shift to fake a second touch point, which allows pinch to zoom to work.

###Input by Font Bureau

![Input](/images/posts/fontb.png)

I recently had a spate of font experimentation in Visual Studio.  I'm typically a terminal/Vim user, so I'm not used to the way Windows handles font rendering.  Since then I've been tweaking my fonts everywhere, although I keep ending up back on Menlo or Meslo.

André Mora sent in Font Bureau's [Input](http://input.fontbureau.com/) typeface:

> Input is a flexible system of fonts designed specifically for code by David Jonathan Ross. It offers both monospaced and proportional fonts, all with a large range of widths, weights, and styles for richer code formatting.

There's an interesting page with more details about Input, called [Questioning Monotheism](http://input.fontbureau.com/info/):

> Monospaced fonts aren't great for setting normal text, but they have become the de facto standard for setting code. Since all characters are constrained to the same fixed width, the page becomes a grid of characters, and the mechanics of typesetting are drastically simplified. However, this comes at an aesthetic cost: wide characters are forced to squeeze; narrow characters are forced to stretch. Uppercase letters look skinny next to lowercase, and bold characters don't have enough room to get very bold.

It goes on to present several arguments about how to position text for code:

> By mixing typographic variation with the power of syntax highlighting, by composing text that transcends a fixed-width grid, and by choosing and combining multiple font styles, we can end all up with code and data that is ultimately easier to read and write.

You can download Input for private use, or license it for commercial publications (including websites).
