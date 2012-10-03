---
layout: post
title: "Node Roundup: otr, matches.js, mariasql"
author: "Alex Young"
categories:
- node
- modules
- security
- cryptography
- mysql
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Off-the Record Messaging Protocol

[otr](https://github.com/arlolra/otr) (License: _LGPL_, npm: [otr](https://npmjs.org/package/otr)) by Arlo Breault is an implementation of an [Off-the Record Messaging Protocol](http://en.wikipedia.org/wiki/Off-the-Record_Messaging):

> Off-the-Record Messaging, commonly referred to as OTR, is a cryptographic protocol that provides strong encryption for instant messaging conversations. OTR uses a combination of the AES symmetric-key algorithm, the Diffie–Hellman key exchange, and the SHA-1 hash function. In addition to authentication and encryption, OTR provides perfect forward secrecy and malleable encryption.

It's designed to be used in browsers, but can also be used with Node.  The readme has details on how to get started with otr, and the author notes that the project has been used by [Cryptocat](https://github.com/kaepora/cryptocat).

###matches.js

[matches.js](https://github.com/natefaubion/matches.js) (License: _MIT_, npm: [matches](https://npmjs.org/package/matches)) by Nathan Faubion is a pattern matching shorthand library that can create new objects with a convenient wrapper:

{% highlight javascript %}
var myfn = pattern({
  // Null
  'null' : function () {...},

  // Undefined
  'undefined' : function () {...},

  // Numbers
  '42'    : function () { ... },
  '12.6'  : function () { ... },
  '1e+42' : function () { ... },

  // Strings
  '"foo"' : function () { ... },

  // Escape sequences must be double escaped.
  '"This string \\n matches \\n newlines."' : function () { ... }
});
{% endhighlight %}

The author has used this library to create [adt.js](https://github.com/natefaubion/adt.js), which is a library for making pseudo-algebraic types and immutable structures:

> ... I say pseudo because it just generates classes with boilerplate that make them look and work like types in functional languages like Haskell or Scala.  It works in the browser or on the server.

###mariasql

[mariasql](https://github.com/mscdex/node-mariasql) (License: _MIT_, npm: [mariasql](https://npmjs.org/package/mariasql)) by Brian White is a high performance, single-threaded, asynchronous, cross-platform MySQL driver.  It's based on libmariadbclient, and the author notes that it works more like a typical Node module:

> This module strives to keep with the "node way" by never buffering incoming rows. Also, to keep things simple, all column values are returned as strings (except MySQL NULLs are casted to JavaScript nulls).

Brian has posted benchmarks that compare various SQL operations across several client libraries, including C and PHP-based samples: [MySQL client library benchmarks](http://mscdex.github.com/node-mysql-benchmarks/).
