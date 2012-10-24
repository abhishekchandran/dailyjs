---
layout: post
title: "Node Roundup: 0.8.12, Node CSV, Memoize"
author: "Alex Young"
categories: 
- node
- modules
- csv
- functional
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.12

[Node 0.8.12](http://blog.nodejs.org/2012/10/12/node-v0.8.12/) is out, which has some fixes for Windows, the Buffer and HTTP modules, and the REPL.  I upgraded as soon as this release came out, and it's running all of my stuff fine as far as I can tell.

###Node CSV

[Node CSV](http://www.adaltas.com/projects/node-csv/) (GitHub: [wdavidw / node-csv-parser](https://github.com/wdavidw/node-csv-parser), License: _New BSD_, npm: [csv](https://npmjs.org/package/csv)) by David Worms is a streaming CSV parser.  By implementing stream readers and writers, this module can parse CSV with less memory overheads when compared to reading the entire file into memory.

It can be used with `fs.createReadStream` like this:

{% highlight javascript %}
fs.createReadStream('./in')
  .pipe(csv())
  .pipe(fs.createWriteStream('./out'));
{% endhighlight %}

Alternatively, David has added a more convenient property-based API:

{% highlight javascript %}
csv()
  .from.path('./in')
  .to.string(function(data) { console.log(data); });
{% endhighlight %}

To set options, `from.options({ option: 'value' })` can be used.  This supports the usual CSV parser settings, like field delimiters and quoting.  The project has Mocha tests, and there's a growing list of contributors.

###Memoize

[Memoize](https://github.com/medikoo/memoize) (License: _MIT_, npm: [memoize](https://npmjs.org/package/memoize)) by Mariusz Nowak is a memoize module that implements pretty much everything related to memoization that I can think of.  It works in both Node and browsers, works with function arguments without serialising arguments, supports asynchronous functions, and has cache management features.

The "primitive mode" is interesting because it's optimised for large amounts of data.  In fact, it made me think back to `Map` and `WeakMap` from Monday's article on [ES6 for Node](http://dailyjs.com/2012/10/15/preparing-for-esnext/).  It seems like caching would get a boost from these ES6 features.
