---
layout: post
title: "pde-engine, colormap, Dimsum"
author: Alex Young
categories:
- libraries
- graphics
- physics
- node
- modules
- fastfood
---

###pde-engine and colormap

<div class="image">
  <img src="/images/posts/pde-engine.png" alt="" />
  <small>Wave example running on benpostlethwaite.ca</small>
</div>

Ben Postlethwaite sent in two libraries this week.  The first, pde-engine (GitHub: [bpostlethwaite / pde-engine](https://github.com/bpostlethwaite/pde-engine), License: _MIT_, npm: [pde-engine](https://npmjs.org/package/pde-engine)), can be used to create "nice looking physically realistic effects in websites or games".

Ben's site, [benpostlethwaite.ca](http://benpostlethwaite.ca/) has live examples for the "wave" and "heat" equations, and the project takes advantage of Typed Arrays to improve performance.  Ben suggests using [browserify](https://npmjs.org/package/browserify) to generate a browser-friendly version of code using pde-engine.

The colours in Ben's examples come from his second project, colormap (GitHub: [bpostlethwaite / colormap](https://github.com/bpostlethwaite/colormap), License: _MIT_, npm: [colormap](https://npmjs.org/package/colormap)).  This project generates color values based on Matlab's plot colours, and apparently works well with [D3.js](http://d3js.org/).

Both projects come with example code and documentation in the readme files.

###Dimsum

I don't mind a bit of dim sum now and again, particularly those steamed buns with custard fillings.  My computer can't yet 3D print Chinese dumplings though, so instead I recommend [Dimsum](http://ninjascribble.github.com/dimsum/) (GitHub: [ninjascribble / dimsum](https://github.com/ninjascribble/dimsum), License: _MIT_, npm: [dimsum](https://npmjs.org/package/dimsum)) by Scott Grogan.  It generates lorem ipsum text, and can be used with Node or browsers.

Dimsum includes two flavours: `latin` and `jabberwocky`.  New flavours can also be added, so you could dump in some generic marketing text to get a more accurate mockup going.

Scott has thoughtfully included Mocha tests as well.
