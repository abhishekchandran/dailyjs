---
layout: post
title: "Luc, z.js, Tabler"
AUthor: Alex Young
categories:
- frameworks
- libraries
- browser
- node
- tables
---

###Luc

[Luc](http://pllee.github.io/luc/pages/docs/) (GitHub: [pllee / luc](https://github.com/pllee/luc), License: _MIT_, npm: [luc](https://npmjs.org/package/luc)) by Patrick Lorian Lee is a framework written in ECMAScript 5 designed to work with browsers and Node.  It includes classes for working with arrays, dates, functions, events, and some high-level architectural tools.

For example, this is the composition API, which allows functionality to be added to classes while respecting the inheritance chain:

{% highlight javascript %}
var C = Luc.define({
  $compositions: {
    defaults: Luc.compositionEnums.EventEmitter,
    methods: ['emit']
  }
});

var c = new C();

typeof c.emit
>"function"
typeof c.on
>"undefined"
{% endhighlight %}

Classes can be created with `Luc.define`:

{% highlight javascript %}
var C = Luc.define({
  init: function() {
    Luc.Array.each(this.items, this.logItems)
  },

  logItems: function(item) {
    console.log(item);
  }
});

var c = new C({items: [1,2,3]});
>1
>2
>3
var d = new C({items: 'A'});
>'A'
var e = new C();
{% endhighlight %}

The array functions can be found under `Luc.Array` -- it has the kinds of methods you might be familiar with from libraries like Underscore.  The method signatures are similar as far as I can tell: `Luc.Array.findFirst([1,2,3, {}], {});`.

Luc's source has JSDoc-style comments, a Grunt build script, and unit tests.  It has no dependencies and is currently around 650 lines of code.

###z.js

[z.js](http://kptl.co/z.js/) (Source: [z.js](http://kptl.co/z.js/z.js), License: _MIT_) is a tool for turning text into a binary code that uses [zero width non-breaking spaces](http://www.fileformat.info/info/unicode/char/feff/index.htm).  That means you can create invisible messages that work in most modern browsers (including IE8+).  It can even apply a password to the message so potential snoops must go through an extra level of misdirection.

There's even an ASCII mode where tabs and spaces are used instead of UTF8.

###Tabler

I really loathe making tables, yet almost every project seems to need them.  I inevitably end up creating or finding a table generator that can turn data into suitable HTML tables.  [Tabler](http://brandwatchltd.github.io/tabler/) (GitHub: [BrandwatchLtd / tabler](https://github.com/BrandwatchLtd/tabler), License: _MIT_) by Steve Mason is an AMD-friendly, Mocha-tested library for building dynamic tables.  It takes an array then generates tables based on a "spec" -- a definition of the headers and properties to include in the output.
Usage looks like this:

{% highlight javascript %}
var table = tabler.create([
    {field: 'name', name: 'Name'},
    {field: 'apples', name: '# Apples'},
    {field: 'bananas', name: '# Bananas'}
]);

table.load([
    {name: 'Steve', apples: 2, bananas: 4},
    {name: 'Graham', apples: 1, bananas: 6},
    {name: 'Dan', apples: 9, bananas: 2},
    {name: 'Jon', apples: 5, bananas: 6}
]);
table.render();
{% endhighlight %}
