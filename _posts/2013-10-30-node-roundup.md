---
layout: post
title: "Node Roundup: 0.11.8, tabby, Nixt"
author: "Alex Young"
categories: 
- node
- modules
- substack
- node-web
- testing
- command-line
---

###Node 0.11.8

The core developers are cranking the handle again and firing out releases.  Today [Node 0.11.8](http://blog.nodejs.org/2013/10/30/node-v0-11-8-unstable/) was released, which upgrades uv and V8.  There's a new `buf.toArrayBuffer` API, debugger improvements, and core module fixes.

I saw 0.11.8 announced on Twitter, and the author hinted at more frequent unstable releases.

<blockquote class="twitter-tweet"><p>Node v0.11.8 (Unstable) <a href="http://t.co/RMiRz0dyhV">http://t.co/RMiRz0dyhV</a> It&#39;s been too long since the last release, weekly cadence going forward!</p>&mdash; node js (@nodejs) <a href="https://twitter.com/nodejs/statuses/395583936077647872">October 30, 2013</a></blockquote>

###tabby

If it's not TJ Holowaychuk it's Substack.  I don't believe it's possible to write a weekly column about Node without mentioning one of them at least once.  Substack just released a client-side project called tabby (GitHub: [substack / tabby](https://github.com/substack/tabby), License: _MIT_, npm: [tabby](https://npmjs.org/package/tabby)), a module for creating web applications with tabs using progressive enhancement techniques.

Why is this notable?  Well, [Substack has been ranting](http://www.reddit.com/r/node/comments/1p3evg/require_in_node/cd1m6mm) about Node's module system and client-side code.  He wants you to stop mucking about and `require()`.  Tabby blends the browser and Node by using WebSockets, and makes judicious use of Node's core modules and streams.

For something focused on client-side code, it uses an interesting cocktail of modules.  The [inherits](https://npmjs.org/package/inherits) module provides browser-friendly inheritance, whilst still being compatible with `util.inherits`.  And [trumpet](https://npmjs.org/package/trumpet) is used for parsing and transforming streaming HTML using CSS selectors.  In the documentation, Substack recommends using [hyperspace](https://npmjs.org/package/hyperspace) for rendering.

Looking through the examples, it definitely feels like idiomatic Node.  I can imagine this style scaling up well to a larger web application.

###Nixt

![Nixt](/images/posts/nixt.jpg)

Test code readability can bring huge gains when maintaining projects.  Tests should communicate intent, and the longer they don't need heavy modification the happier everyone will be.  I generally find myself writing DSL-like methods for tests that reduce code duplication, particularly in the set-up phase.

With that in mind, it's interesting to see Nixt (GitHub: [vesln / nixt](https://github.com/vesln/nixt), License: _MIT_, npm: [nixt](https://npmjs.org/package/nixt)) by Veselin Todorov.  This is a module for testing command-line applications.  It's based around expectations, which reminds me of good old [Expect](http://en.wikipedia.org/wiki/Expect).

Nixt works well asynchronously because it supports middleware for ordering execution.  It can be used with a test harness like Mocha, and allows you to define custom expectations, which is where your application-specific DSL-like test helpers come in.

Although I'm probably guilty of using Node for command-line scripts that could be done with a shell script (I write my share of shell script too though), Nixt seems like a great way to test them, particularly as people often forget to test such scripts.
