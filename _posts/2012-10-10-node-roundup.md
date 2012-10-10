---
layout: post
title: "Node Roundup: MongloDB, parseq.js, node-netpbm"
author: "Alex Young"
categories: 
- node
- modules
- databases
- mongo
- markdown
- documentation
- async
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###MongloDB

![MongloDB Logo](/images/posts/monglodb.png)

[MongloDB](http://monglodb.com/) (GitHub: [onglo / MongloDB](https://github.com/Monglo/MongloDB), License: _MIT_) by Christian Sullivan is a database written with JavaScript that's compatible with MongoDB's queries.  It has a plugin system for persistence, and a datastore for Titanium Mobile -- this effectively allows a form of MongoDB to be used within iOS and Android applications.

Monglo has a `DataStore` API that can be used to persist data locally or remotely.  It's based around an object that implements each CRUD operation:

{% highlight javascript %}
var monglo = require('./index').Monglo
  , db = monglo('DemoDB')
  ;

function DemoStore(){
  return {
     insert: function() {}
   , update: function() {}
   , open: function() {}
   , remove: function() {}
   , all: function() {}
  };
}

db.use('store', new DemoStore());
{% endhighlight %}

###parseq.js

[parseq.js](http://parseqjs.com/) (GitHub: [sutoiku / parseq](https://github.com/sutoiku/parseq), License: _MIT_, npm: [parseq](https://npmjs.org/package/parseq)) from Sutoiku, Inc. is a flow control library for organising parallel and sequential operations.  To manage asynchronous operations, `this` can be passed.  If several calls are made, then `this()` can be passed, and the next function will receive an array that contains the results in the order they were called.

The same author also recently released [jsdox](http://jsdox.org/), which is another JSDoc to Markdown generator.

###netpbm

[netpbm](https://npmjs.org/package/netpbm) (GitHub: [punkave / node-netpbm](https://github.com/punkave/node-netpbm), License: _MIT_, npm: [netpbm](https://npmjs.org/package/netpbm)) by Tom Boutell scales and converts images using the [netpbm](http://netpbm.sourceforge.net/) toolkit, which is a venerable set of graphics programs found on many Unix systems.

This library is a wrapper around the netpbm binaries, and takes advantage of the fact that most netpbm programs only read one row of pixels at a time into memory to keep memory usage low.
