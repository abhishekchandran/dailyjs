---
layout: post
title: "memdiff, numerizerJS, Obfuscate.js"
author: "Alex Young"
categories: 
- testing
- debugging
- memory
- node
- modules
- parsing
- text
---

###memdiff

memdiff (GitHub: [azer / memdiff](https://github.com/azer/memdiff), License: _WTFPL_, npm: [memdiff](https://npmjs.org/package/memdiff)) by Azer Koculu is a BDD-style memory leak tool based on [memwatch](https://npmjs.org/package/memwatch).  It can either be used by writing scripts with `describe` and `it`, and then running them with `memdiff`:

{% highlight javascript %}
function SimpleClass(){}
var leaks = [];

describe('SimpleClass', function() {
  it('is leaking', function() {
    leaks.push(new SimpleClass);
  });

  it('is not leaking', function() {
    new SimpleClass;
  });
});
{% endhighlight %}

Or by loading `memdiff` with `require` and passing a callback to `memdiff`.  The memwatch module itself has an event-based API, and includes a platform-independent native module -- so both of these projects are tied to Node and won't work in a browser.

###numerizerJS

numerizerJS (GitHub: [bolgovr / numerizerJS](https://github.com/bolgovr/numerizerJS), License: _MIT_, npm: [numerizer](https://npmjs.org/package/numerizer)) by Roman Bolgov is a library for parsing English language string representations of numbers:

{% highlight javascript %}
var numerizer = require('numerizer');
numerizer('forty two'); // '42'
{% endhighlight %}

It's currently very simple, and doesn't support browsers out of the box, but I like the fact the author has included Mocha tests.  It'd work well alongside other libraries like [Moment.js](http://momentjs.com/) for providing intuitive text-based interfaces.

###Obfuscate.js

Obfuscate.js (GitHub: [miohtama / obfuscate.js](https://github.com/miohtama/obfuscate.js), License: _MIT_) by Mikko Ohtamaa is a client-side script for replacing text on pages with nonsense that may be more desirable than private information.  Mikko suggests this might be useful for making screenshots, so post-processing isn't required to blur out personal information.  The `obfuscate` function takes an optional selector, so either the entire `body` of a document can be obfuscated, or just the contents of a given selector.

It walks through each child node looking for text nodes, so it's lightweight and doesn't have any dependencies.  It also tries to make the text look similar (at a glance) to the original text.

