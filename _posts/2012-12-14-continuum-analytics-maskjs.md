---
layout: post
title: "Continuum, Analytics.js, MaskJS"
author: Alex Young
categories: 
- libraries
- templates
- browser
---

###Continuum

[Continuum](http://benvie.github.com/continuum/) (GitHub: [Benvie / continuum](https://github.com/Benvie/continuum), License: _MIT_, npm: [continuum](https://npmjs.org/package/continuum)) by Brandon Benvie is an ES6 virtual machine written in ES3.  By using [Esprima](http://esprima.org/) to parse a given source file, it generates bytecode which is then executed within an ES6 runtime environment.

If this doesn't sound enough like science fiction to you, then think about it like this: this project will run your ECMAScript 6 code inside its own space-time continuum that allows legacy browsers to support ECMAScript 6 features.

Brandon has already implemented a slew of ES6 features, but hasn't yet added support for array comprehensions, tail call optimisation, or the binary data API.  What you do get, however, is destructuring assignment, spread in arguments and array initializers, "rest" parameters, classes and super, arrow functions, and even Map, Set, and WeakMap.

If you want to get an idea of how this project works, take a look at the `engine/assembler.js` and `engine/runtime.js` files to see the opcodes and how the stack is used.

###Analytics.js

[Analytics.js](http://segmentio.github.com/analytics.js/) (GitHub: [segmentio / analytics.js](https://github.com/segmentio/analytics.js), License: _MIT_) from Segment.io is a simplified API for supporting various web analytics services, including Google Analtyics, KISSmetrics, Mixpanel, and Chartbeat.

It provides a single API for defining events that should be tracked, allowing you to focus on getting the data out of activities on your site without becoming bogged down in a given service's implementation peculiarities.

Segment.io also made [Socrates.io](http://socrates.io/), which seems to be very popular.  I recommend keeping an eye on the [GitHub Segment.io](https://github.com/segmentio) account for more cool projects.

###MaskJS

[MaskJS](http://libjs.it/#/mask) (GitHub: [tenbits / MaskJS](https://github.com/tenbits/MaskJS), License: _MIT_) by Alexander Kit is a template engine for Node and browsers.  The author has built it with performance and mobile devices in mind, and has a [jsperf benchmark](http://jsperf.com/javascript-template-engine-compare/27) that compares it against other template engines.

It supports custom tags, which are designed to help encapsulate markup into reusable components, and the author has created some for two-way data binding.  The best way to get a feel for the markup style and API is to check out the [MaskJS examples](http://libjs.it/#/mask/examples).
