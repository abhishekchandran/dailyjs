---
layout: post
title: "Node Roundup: npm 3, io.js 1.4.3, NoDent"
author: Alex Young
categories:
- node
- modules
- libraries
- iojs
- npm
- async
---

###npm: Roadmap for 3, Using jQuery Modules

The [npm roadmap](https://github.com/npm/npm/wiki/Roadmap) has been updated with details on npm.  This includes multi-stage installation, improvements to shrinkwrap, and progress bars.  There's an entry that aims to solve the front-end tooling problem, and I noticed shipping HTML and CSS is mentioned.  I prefer a Browserify/npm-based workflow, but I've always found this stage less than elegant, so it'll be interesting to see what happens there.

To read more, visit the [npm blog](http://blog.npmjs.org/post/112610795275/npm-weekly-7).  There's also another interesting post about jQuery, which [describes how to use jQuery plugins through npm](http://blog.npmjs.org/post/112064849860/using-jquery-plugins-with-npm).  The previous post on jQuery was about publishing modules, but this one shows how to consume plugins even if they don't use npm.

###io.js 1.4.3

There was a new io.js release (1.4.3) on Monday, which has quite a big fix for streams on Windows and the beginnings of ARM support.  The 1.4.x branch was released at 1.4.1 due to a libuv bug in 1.4.0.  This branch adds newer versions of V8, npm, and libuv, but also has improvements for process, stream, and http.

For more details on io.js and npm changes, you can look at the changelogs on GitHub:

* [npm/CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md)
* [io.js/CHANGELOG.md](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md)

They're both nicely annotated with links to commits, and summarise major changes.

###NoDent

In my DailyJS email backlog I found NoDent (GitHub: [MatAtBread/nodent](https://github.com/MatAtBread/nodent), License: _BSD-2-Clause_, npm: [nodent](https://www.npmjs.com/package/nodent)).  It's a small module that adds support for the proposed `aysnc` and `await` keywords.  They're not too hard to learn, and once you get used to them they can make asynchronous code more readable.

The basic idea is to mark asynchronous functions with the `async` keyword, and then use the `await` keyword before they're called.

{% highlight javascript %}
async function tellYouLater(sayWhat) {
  // Do something asynchronous and terminal, such as DB access, web access, etc.
  return result;
}

var result = await tellYouLater('Hi there');

{% endhighlight %}

This will cause execution to wait until `tellYouLater` returns.  I've used `async/await` in C#, and it works well for methods that return a single value (rather than an observable with a sequence of values).

The author's readme has lots of examples of uses and abuses, so it's worth reading if you seriously want `async/await` now.
