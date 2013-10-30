---
layout: post
title: "HiDPI Canvas Polyfill, formatter.js"
author: "Alex Young"
categories: 
- browser
- canvas
- polyfills
---

###HiDPI Canvas Polyfill

Don't you just hate it when a cool canvas animation suddenly goes blurry?  [HiDPI Canvas Polyfill](https://github.com/jondavidjohn/hidpi-canvas-polyfill) by Jonathan Johnson scales the canvas so the PPI is right, avoiding unsightly blurring.  Jonathan notes that Safari is currently the only browser that does this properly.

I don't know if the author was inspired by [How do I fix blurry text in my HTML5 canvas?](http://stackoverflow.com/questions/15661339/how-do-i-fix-blurry-text-in-my-html5-canvas) on Stack Overflow, but the solution looks similar to MyNameIsKo's answer.

Jonathan has gone further by including tests, and he's included a Grunt build script as well.

Jonathan also sent in [BubbleChart](http://jondavidjohn.github.io/bubblechart/) (GitHub: [jondavidjohn / bubblechart](https://github.com/jondavidjohn/bubblechart), License: _Apache 2.0_, npm: [bubblechart](https://npmjs.org/package/bubblechart)) which is an interactive visualisation for two dimensional data.

###formatter.js

[formatter.js](http://firstopinion.github.io/formatter.js/index.html) (GitHub: [firstopinion / formatter.js](https://github.com/firstopinion/formatter.js), License: _MIT_) by Jarid Margolin helps you to define custom form fields.  The examples given are a credit card form and a telephone number entry.  The script can insert text as the user types, so the credit card form inserts hypens, and the telephone number uses the US-style format with brackets and a single hyphen.

The API looks like this, but there's a jQuery wrapper as well:

{% highlight javascript %}
new Formatter(document.getElementById('credit-input'), {
  pattern: '{{9999}}-{{9999}}-{{9999}}-{{9999}}'
});
{% endhighlight %}

The project includes tests that can be run with npm, and there are examples here: [formatter.js demos](http://firstopinion.github.io/formatter.js/demos.html).
