---
layout: post
title: "Node Roundup: Browser tests"
author: "Alex Young"
categories: 
- node
- modules
- npm
- testing
---

I wanted to write about Substack's [Testling](https://github.com/substack/testling) project, but then coincidentally Chris Scribner sent in his [Browser Harness](https://github.com/scriby/browser-harness) project.  Let's look at both to see how they shape up.

###Testling

Testling (GitHub: [substack / testling](https://github.com/substack/testling), License: _MIT_, npm: [testling](https://npmjs.org/package/testling)) is a tool for running tests in local instances of browsers.  It works by using [browserify](http://browserify.org/) -- this allows Node modules to be used in browsers.

![Browserify](/images/posts/browserify2.png)

But what's _really_ going on?  Follow Testling's source into [browser/prelude.js](https://github.com/substack/testling/blob/master/browser/prelude.js) and you'll find [xhr-write-stream](https://npmjs.org/package/xhr-write-stream).  Also, Testling uses [browser-launcher](https://github.com/substack/browser-launcher) which allows browsers to be launched headlessly through Xvfb or PhantomJS.

I installed `browserify` and `testling` then ran `browserify test.js | testling` and it opened Chrome and ran my tests.  I wasn't sure how to make Testling run it headlessly, or run it in a different browser, but apparently if you define a `"testling"` field in your `package.json` it should pick up your desired browser settings from there.  Read more in [testling field documentation](https://github.com/substack/testling/blob/master/doc/testling_field.markdown).

### Browser Harness

Browser Harness (GitHub: [scriby / browser-harness](https://github.com/scriby/browser-harness), License: _MIT_, npm: [browser-harness](https://npmjs.org/package/browser-harness)) takes a different approach.  It uses client-side code to listen for commands to run tests.  It currently uses [NowJS](https://github.com/Flotype/now) for communication, but the author wants to replace it with Socket.IO.

It requires a file to be served from the domain of the site being tested, and has a few other limitations which are documented in the readme file.

The harness has built-in support for fibers, so if you install [asyncblock](https://npmjs.org/package/asyncblock) you can write tests in a blocking style.

The example in the documentation uses Mocha, but the author notes that other test frameworks should work as well.

