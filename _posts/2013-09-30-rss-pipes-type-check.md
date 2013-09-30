---
layout: post
title: "RSS Pipes, type-check"
author: "Alex Young"
categories: 
- rss
- node
- apps
- haskell
- functional
---

###RSS Pipes

[RSS Pipes](http://dai-shi.github.io/rss-pipes/) (GitHub: [dai-shi / rss-pipes](https://github.com/dai-shi/rss-pipes), License: _BSD_) by Daishi Kato is an Express app for aggregating RSS feeds.  It has a lightweight database wrapper for PostgreSQL and SQLite using the [jugglingdb](https://npmjs.org/package/jugglingdb), which seems like a cleaner ORM that some of the Node database ORMs I've used, and it keeps the route handlers lightweight which is good practice in Express applications.

One of the useful features it has is filtering feeds.  For example, you can filter for keywords or truncate the result set.  In this respect it's like a simple version of Yahoo! Pipes.  The client-side portion of the project uses Bootstrap, so you could probably customise it if you wanted.

###type-check

Haskell makes an appearance in [type-check](http://gkz.github.io/type-check/) (GitHub: [gkz / type-check](https://github.com/gkz/type-check), License: _MIT_, npm: [type-check](https://npmjs.org/package/type-check)) by George Zahariev.  It performs runtime type checking using a Haskell inspired syntax:

{% highlight javascript %}
var typeCheck = require('type-check').typeCheck;
typeCheck('Number', 1);               // true
typeCheck('Number', 'str');           // false

typeCheck('Number | String', 2);      // true
typeCheck('Number | String', 'str');  // true

typeCheck('{x: Number, y: Boolean, ...}', {x: 2, y: false, z: 3});  // true
{% endhighlight %}

It works in browsers and Node, and apparently has 100% statement, branch, and line test coverage.  It seems like something that might add an extra level of readability to test code, but could also be useful for validating user input.
