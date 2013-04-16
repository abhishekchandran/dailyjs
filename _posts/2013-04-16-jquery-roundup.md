---
layout: post
title: "jQuery Roundup: TyranoScript, Sly, FPSMeter"
author: Alex Young
categories:
- jquery
- plugins
- graphics
- animations
- games
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###TyranoScript

![TyranoScript](/images/posts/tyranoscript.png)

Evan Burchard sent in [TyranoScript](http://tyrano.jp/) (GitHub: [ShikemokuMK / tyranoscript](https://github.com/ShikemokuMK/tyranoscript), License: _MIT_), a jQuery-powered HTML5 interactive fiction game engine:

> The game engine was only in Japanese, so I spent the last week making it available in English.
> As far as what it does, it sits somewhere between an interactive fiction scripting utility and a presentation library like impress.js.  It has built in functions (tags) for things like making text and characters pop up, saving the game, changing scenery and shaking the screen.  But it supplies interfaces for arbitrary HTML, CSS and JavaScript to be run as well, so conceivably one could use it for presentations or other types of applications.  One of the sample games on the project website demonstrates this with a compelling YouTube API integration.  The games created with TyranoScript can run on modern browsers, Android, iPad and iPhone.

Evan's English version is at [EvanBurchard / tyranoscript](https://github.com/EvanBurchard/tyranoscript).  For a sample game, check out the delightfully nutty [Jurassic Heart](http://hima.gptouch.com/games/jurassic_heart/) -- a game where you date a dinosaur (of course)!

###Sly

[Sly](http://darsa.in/sly/) (GitHub: [Darsain / sly](https://github.com/Darsain/sly), License: _MIT_, Bower: _sly_) by Darsain is a library for scrolling -- it can be used where you need to replace scrollbars, or where you want to build your own navigation solutions.

The author has paid particular attention to performance:

> Sly has a custom high-performance animation rendering based around the Animation Timing Interface written directly for its needs. This provides an optimized 60 FPS rendering, and is designed to still accept easing functions from jQuery Easing Plugin, so you won't event notice that Sly's animations have nothing to do with jQuery :).

Sly's site has a few examples -- check out the [infinite scrolling](http://darsa.in/sly/examples/infinite.html) and [parallax](http://darsa.in/sly/examples/parallax.html) demos.

###FPSMeter

![FPSMeter](/images/posts/fpsmeter.png)

Sly's author also sent in FPSMeter.  When working on graphically-oriented projects, it's sometimes useful to display the frames-per-second of animations.  [FPSMeter](http://darsa.in/fpsmeter/) (GitHub: [Darsain / fpsmeter](https://github.com/Darsain/fpsmeter), Bower: _fpsmeter_) measures FPS using `WindowAnimationTiming`, with a polyfill to patch in browser support for most browsers, including IE7+.

FPSMeter can measure FPS, milliseconds between frames, and the number of milliseconds it takes to render one frame.  It can also cope with multiple instances on a page, and has show/hide methods that will pause rendering.  It also supports [theming](https://github.com/Darsain/fpsmeter/wiki/Theming), so you should be able to get it to sit in nicely in your existing interface.
