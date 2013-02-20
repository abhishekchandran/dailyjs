---
layout: post
title: "Node Roundup: 0.8.20, 0.9.10, continuation.js, selenium-node-webdriver"
author: "Alex Young"
categories: 
- node
- modules
- testing
- functional
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.8.20, 0.9.10

[Node 0.8.20](http://blog.nodejs.org/2013/02/15/node-v0-8-20-stable/) was released last week.  The most significant updates in this version are fixes for the HTTP core module, so if you're on 0.8.19 then I can't see any reason not to upgrade.

[Node 0.9.10](http://blog.nodejs.org/2013/02/19/node-v0-9-10-unstable/) meanwhile has several stream-related updates.  The default options for `WriteStream` have been updated to improve performance, and empty strings and buffers no longer signal EOF.

###continuation.js

continuation.js (GitHub: [dai-shi / continuation.js](https://github.com/dai-shi/continuation.js), License: _BSD_, npm: [continuation.js](https://npmjs.org/package/continuation.js)) by Daishi Kato automatically adds tail call optimisation to modules loaded with `require`.  It's written using [esprima](https://npmjs.org/package/esprima) and [escodegen](https://npmjs.org/package/escodegen) to parse and generate a new version of existing code.  It does this by using trampolined functions, which is also how tail recursive functions are implemented in functional languages like Lisp.

The author has included benchmarks that show where the module improves performance.  There are cases where it won't be faster due to how trampolining is handled -- there are also some interesting posts by Guillaume Lathoud about [implementing tail call optimisation without trampolining](http://glat.info/pub/tailopt-js/).

###selenium-node-webdriver

selenium-node-webdriver (GitHub: [WaterfallEngineering / selenium-node-webdriver](https://github.com/WaterfallEngineering/selenium-node-webdriver), License: _Apache 2_, npm: [selenium-node-webdriver](https://npmjs.org/package/selenium-node-webdriver)) by Lon Ingram packages a prebuilt WebDriver client so it's easier to get started writing tests that use WebDriver.  Lon notes that it was designed to work with PhantomJS, but it could be used with any WebDriver server.

