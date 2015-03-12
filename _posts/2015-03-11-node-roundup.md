---
layout: post
title: "Node Roundup: io.js, npm and jQuery, error-system"
author: Alex Young
categories:
- node
- modules
- libraries
- error-handling
- iojs
- hardware
---

###io.js

Last Friday, io.js 1.5.0 was released, which is another major milestone for the project.  It introduces a new `Buffer.prototype.indexOf` method, which is like `Array.prototype.indexOf`.  This is implemented in `node_buffer.cc`, and works with strings and numbers.

Last week Rodd Vagg posted a comment about io.js on DailyJS to say that the ARMv8 support is separate to the earlier Node support for ARMv6 and 7, and it actually sounds quite significant.  According to last week's release notes, [Linaro](http://www.linaro.org) has contributed hardware to help io.js with ARMv8:

> this is an entirely new architecture from ARM that adds 64-bit support which they are heavily pursuing the server market with. io.js (Node) + ARMv8 on the server is an amazing opportunity and ARM have been lending their support to the io.js project to make this work.

64bit ARM means more RAM in Android phones and tablets, which is great. But what about servers -- are we going to be able to use low-powered clusters of powerful ARM machines?  [Linaro has details on its ARM servers](http://www.linaro.org/leg/servercluster/), and has an application form for people to request access to try them out.  Linaro says it's planning to use servers are based on Opteron A1100 Cortex-A57, and [X-Gene](https://www.apm.com/products/data-center/x-gene-family/x-gene/).

The best place to read more about the latest io.js release is the [io.js Week of March 6th](https://medium.com/node-js-javascript/io-js-week-of-march-6th-2f9344688277) post on Medium.  Which reminds me, there's an [@iojs Medium account](https://medium.com/@iojs) which is definitely worth following.

###npm and jQuery

The npm weekly update points to yet another [npm and jQuery plugin article](http://blog.npmjs.org/post/112712169830/making-your-jquery-plugin-work-better-with-npm).  This one talks about how to make your own jQuery plugins make better use of npm.  This includes referencing stylesheets in `package.json` and CommonJS compatibility.

###error-system

Something I like to do in my Node-based web apps is include an errors.js file that subclasses `Error` with constructors named after HTTP errors.  It makes it easier for me to pass the right error into `next` (in Express/Connect) so the error gets passed along to a centralised error handler.  The way I do it is basic old skool JavaScript, so I've been looking for ways to improve it

Fomichev Kirill noticed Rod Vagg created [node-errno](https://github.com/rvagg/node-errno).  Rodd's module includes errors for libuv and Node, so you can check error codes with expressions like `require('errno').code.ENOTEMPTY`.  You can also use it as a command-line tool for checking Node errors, and it has an API for making custom errors.  The custom errors include the call stack, and it allows error hierarchies to be created.

Inspired by this, Fomichev made error-system (GitHub: [fanatid/error-system](https://github.com/fanatid/error-system), License: _MIT_, npm: [error-system](https://www.npmjs.com/package/error-system)).  It's similar to Rodd's module, but is designed specifically for creating custom errors.  If you were making a web application, you could make a class for request errors like this:

{% highlight javascript %}
var errorSystem = require('error-system')
var RequestError = errorSystem.createError('RequestError', 'Code: {0} (url: {1})')
{% endhighlight %}

This is exactly what I wanted when I made my original errors.js file.  I particularly like the numbered arguments in Fomichev's module because it cuts down the amount of boilerplate when compared to my solution.
