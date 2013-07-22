---
layout: post
title: "RgbQuant, Scoping AngularJS Directives"
AUthor: Alex Young
categories:
- images
- libraries
- browser
- AngularJS
---

###RgbQuant

![RgbQuant](/images/posts/rgbq.png)

[RgbQuant](http://o-0.me/RgbQuant/) (GitHub: [leeoniya / RgbQuant.js](https://github.com/leeoniya/RgbQuant.js), License: _MIT_) by Leon Sorokin is an image quantization library that runs in browsers:

> Color quantization is the process of reducing an image with thousands or millions of colors to one with fewer (usually 256). The trick is to balance speed, cpu and memory requirements while minimizing the perceptual loss in output quality. More info can be found on [wikipedia](http://en.wikipedia.org/wiki/Color_quantization). Various algorithms can be found on [rosettacode.org](http://rosettacode.org/wiki/Color_quantization).

Internally it uses typed arrays, some ES5 array methods, and a Canvas element.  The API allows the number of colours to be defined, and some more low-level control over the algorithm.

###Scoping AngularJS Directives

James Donaghue sent in his articles about scoping AngularJS directives: [Scoping AngularJS Directives Part 1](http://spectaclelabs.io/blog/2013/06/22/scoping-angularjs-directives-part-1/) and [Scoping AngularJS Directives Part 2](http://spectaclelabs.io/blog/2013/06/23/scoping-angularjs-directives-part-2/).

> ... when both are applied to the same element, regardless of order, they have the same scope which is the scope type 3 (isolated scope). This is the most important combination to understand as you other directives may be expecting either direct or prototypical access to the nearest controller scope, but when paired with an isolated scope directive they no longer have this access. This can lead to many unexpected errors. In my opinion isolated scopes should be used only very judiciously and with exact intention understanding this behavior.

