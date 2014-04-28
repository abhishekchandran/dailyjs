---
layout: post
title: "Managing Node.js Callback Hell, this Considered Harmful"
author: "Alex Young"
categories:
- node
- tutorials
---

Marc Harter, who is working with me on [Node.js in Practice](http://manning.com/young/), recently published [Managing Node.js Callback Hell](https://medium.com/p/1fe03ba8baf):

> Callback hell is subjective, as heavily nested code can be perfectly fine sometimes. Asynchronous code is hellish when it becomes overly complex to manage the flow. A good question to see how much "hell" you are in is: how much refactoring pain would I endure if `doAsync2` happened before `doAsync1`? The goal isn't about removing levels of indentation but rather writing modular (and testable!) code that is easy to reason about and resilient.

The example he uses is nested asynchronous file operations, with a counter to determine completion.  This is compared to a version that uses [async](https://www.npmjs.org/package/async), and another that uses promises with [q](https://www.npmjs.org/package/q).

The post was originally published on StrongLoop's blog, here: [Managing Node.js Callback Hell with Promises, Generators and Other Approaches](http://strongloop.com/strongblog/node-js-callback-hell-promises-generators/).  [StrongLoop's blog](http://strongloop.com/strongblog/) is worth subscribing to if you're a Node developer -- it has general tutorials and coverage of interesting npm modules.

Tom Boutell sent in a blog post about OO in JavaScript, called ["this" considered harmful (sometimes)](http://justjs.com/posts/this-considered-harmful):

> Most JavaScript implementations of "classes" do have certain features in common. They rely on the "this" keyword to refer to the current object; after all, it's built into the language. They provide a convenience function to implement subclassing, because it's tricky to get right, especially in older browsers. And they have a really tough time handling callbacks in methods, because "this" ceases to refer to the object you expect.

Tim Oxley posted some comments discussing how to use `Function.prototype.bind` as well.
