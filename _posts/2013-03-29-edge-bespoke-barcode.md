---
layout: post
title: "Edge.js, Bespoke.js, Barcode39"
author: Alex Young
categories: 
- Canvas
- node
- Microsoft
- presentations
- libraries
---

###Edge.js

[Edge.js](http://tjanczuk.github.com/edge/) (GitHub: [tjanczuk / edge](https://github.com/tjanczuk/edge), License: _Apache 2_, npm: [edge](https://npmjs.org/package/edge)) by Tomasz Janczuk is an in-process interoperability layer between .NET and Node.  This allows things like CPU-bound operations to be processed by .NET, or Node to access the Win32 APIs through C#.

The .NET code can be executed asynchronously and may be passed as a multiline comment or a string.  A basic example looks like this:

{% highlight javascript %}
var edge = require('edge');

var helloWorld = edge.func('async (input) => { return ".NET Welcomes " + input.ToString(); }');

helloWorld('JavaScript', function(err, result) {
  if (err) throw err;
  console.log(result);
});
{% endhighlight %}

Running this example would display ".NET welcomes JavaScript".

Other CLR languages [can be supported](https://github.com/tjanczuk/edge/wiki/Add-support-for-a-CLR-language), should you be interested in playing with F# for example.

This project requires Windows, and needs Visual Studio 2012, Python 2.7, and npm-gyp to build.

###Bespoke.js

![Bespoke.js](/images/posts/bespokejs.png)

[Bespoke.js](http://markdalgleish.com/projects/bespoke.js/) (GitHub: [markdalgleish / bespoke.js](https://github.com/markdalgleish/bespoke.js), License: _MIT_, bower: _bespoke.js_) by Mark Dalgleish is a small but slick presentation library.  It works with keyboard and touch events, and is intended to be used with CSS transitions.

It's built using ECMAScript 5, so you'll want to run your presentations on a compatible browser.

Creating presentations involves wrapping HTML slide content in `<section>` containers.  Horizontal and vertical deck styles are supported, and Mark has documented the CSS classes in the project's readme so you can hook into the provided JavaScript and styles.

###Barcode39

Barcode39 (GitHub: [erik5388 / barcode-39.js](https://github.com/erik5388/barcode-39.js), License: _MIT_) by Erik Zettersten is a [Code 39](http://en.wikipedia.org/wiki/Code_39) implementation -- it basically generates barcodes that almost all barcode readers can cope with.  It can output data URIs and supports Canvas for drawing.

The JavaScript API is `new Barcode39(elementId, type, delimeter)`, but it will also look for an element with the default ID of `barcode` and read the element's content for the barcode's source text.
