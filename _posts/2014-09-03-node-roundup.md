---
layout: post
title: "Node Roundup: DataCollection.js, supererror, Readability"
author: "alex young"
categories:
- modules
- node
- libraries
---

###DataCollection.js

[DataCollection.js](http://thestorefront.github.io/DataCollection.js/) (GitHub: [thestorefront / DataCollection.js](https://github.com/thestorefront/DataCollection.js), License: _MIT_, npm: [data-collection](https://www.npmjs.org/package/data-collection)) from Storefront is a library for querying data.  You can use it in browsers or Node.  The example in the documentation uses an array of objects, then filters them based on key/values, and some sql-like operators including `max` and `distinct`.

The authors claim it's fast, and although I can't confirm this it does include a feature for defining indexes for specific keys.  It's well documented and has 95.5% test coverage.

###supererror

If you've got a project where you're logging errors with `console.error`, but want to get more data like line numbers without modifying code, then you could try supererror (GitHub: [nebulade/supererror](https://github.com/nebulade/supererror), License: _MIT_, npm: [supererror](https://www.npmjs.org/package/supererror)) by Johannes Zellner.

It changes `console.error` to include colours, line number, and stacks for `Error` objects.

###Readability

Readability (GitHub: [luin / node-readability](https://github.com/luin/node-readability), License: _Apache 2.0_, npm: [node-readability](https://www.npmjs.org/package/node-readability)) by Zihua Li turns pages into simplified Arc90-style HTML.  It uses jsdom, supports more character encodings like GB2312, and converts relative URLs so images still work.

I seem to remember having issues with encodings and relative images with other Readability-derived projects, so this seems ideal.
