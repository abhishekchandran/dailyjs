---
layout: post
title: "New npm Site, Amelie Music Visualiser"
author: "Alex Young"
image: "/images/posts/amelie.png"
categories:
- npm
- audio
---

### New npm Site

![npm](/images/posts/npm-pg.png)

[npm](https://www.npmjs.org/) has a new website!  There's an [announcement blog post](http://blog.npmjs.org/post/104856015780/npm-has-a-new-website) that explains what has changed, and what's next, including this information about private modules:

> Our next immediate goal is to support private npm modules on the website. This will allow individuals and teams to publish, install, and view private code using all the familiar npm mechanisms.

The website is now responsive, so it'll look better on mobile devices.  I found it looked nicer when I tiled my browser windows, which I often like to do when juggling material for DailyJS posts.

### Amelie Music Visualiser

![Amelie](/images/posts/amelie.png)

Adam Timberlake sent in a music visualisation experiment made with React, D3, and SVG: [amelie.herokuapp.com](http://amelie.herokuapp.com/) (GitHub: [Wildhoney/Amelie](https://github.com/Wildhoney/Amelie), Bower: _amelie_).  It uses [AnalyserNode](https://developer.mozilla.org/en-US/docs/Web/API/AnalyserNode) to get frequency data from the audio file:

> The `AnalyserNode` interface represents a node able to provide real-time frequency and time-domain analysis information. It is an AudioNode that passes the audio stream unchanged from the input to the output, but allows you to take the generated data, process it, and create audio visualizations.


Because the `AnalyserNode` API does the more complicated FFT stuff, the source is actually fairly easy to understand.  Take a look at [Amelie.jsx](https://github.com/Wildhoney/Amelie/blob/master/module/Amelie.jsx) to see how the colours are generated and then plotted using D3.js.

