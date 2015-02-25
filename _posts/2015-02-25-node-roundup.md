---
layout: post
title: "Node Roundup: npm jQuery, io.js 1.3.0, proginoskes"
image: "/images/posts/tests-result.png"
author: Alex Young
categories:
- sponsored-content
- recruitment
- apps
---

###npm and jQuery

It's finally happened: jQuery is recommending npm for distributing plugins.  My preferred client-side workflow is npm and Browserify, but I know many readers use Bower.  Hopefully this shift will encourage more people to use npm for client-side libraries.

Lin Clark mentioned this in this week's [npm Weekly](http://blog.npmjs.org/post/111968476155/npm-weekly-6), and also that npm has hit 1,000,000,000 downloads in a single month.  Very impressive!

###io.js 1.3.0

[io.js](https://iojs.org/) 1.3.0 is out.  As usual the details are in the [nicely marked up changelog](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md), which now contains links to commits.  That makes it easier to look up what the commits actually do, because the one line descriptions can't always communicate the subtleties of the pull requests.  You'll probably think I'm being sarcastic, but I was happy to see these changes:

* [[`f0296933f8`](https://github.com/iojs/io.js/commit/f0296933f8)] - **doc**: correct `it's` to `its` in process (Charmander) [#837](https://github.com/iojs/io.js/pull/837)
* [[`4ca7cca84a`](https://github.com/iojs/io.js/commit/4ca7cca84a)] - **doc**: grammar fix in smalloc (Debjeet Biswas) [joyent/node#9164](https://github.com/joyent/node/pull/9164)
* [[`ba40942ad2`](https://github.com/iojs/io.js/commit/ba40942ad2)] - **doc**: fix sentence grammar timers.markdown (Omer Wazir) [#815](https://github.com/iojs/io.js/pull/815)

It's all about attention to detail!  In general this release feels like it's focused on quality control -- there are lots of JavaScript code quality fixes and documentation tweaks.

The new changelog formatting also lets you easily see which commits come from Node:

* [[`4ca7cca84a`](https://github.com/iojs/io.js/commit/4ca7cca84a)] - **doc**: grammar fix in smalloc (Debjeet Biswas) [joyent/node#9164](https://github.com/joyent/node/pull/9164)
* [[`30dca66958`](https://github.com/iojs/io.js/commit/30dca66958)] - **doc**: fix code syntax (Dan Dascalescu) [joyent/node#9198](https://github.com/joyent/node/pull/9198)
* [[`6a2b204bbc`](https://github.com/iojs/io.js/commit/6a2b204bbc)] - **module**: replace NativeModule.require (Herbert Vojčík) [joyent/node#9201](https://github.com/joyent/node/pull/9201)
* [[`0cff0521c3`](https://github.com/iojs/io.js/commit/0cff0521c3)] - **net**: throw on invalid socket timeouts (cjihrig) [joyent/node#8884](https://github.com/joyent/node/pull/8884)
* [[`3b1b4de903`](https://github.com/iojs/io.js/commit/3b1b4de903)] - **test**: Timeout#unref() does not return instance (Jan Schär) [joyent/node#9171](https://github.com/joyent/node/pull/9171)

I think it's [@rvagg](https://twitter.com/rvagg) who writes this document, so thanks Rod for making it easier for us to see what's going on.

###proginoskes

Jason Gerfen sent in proginoskes (GitHub: [jas-/proginoskes](https://github.com/jas-/proginoskes), License: _MIT_, npm: [proginoskes](https://www.npmjs.com/package/proginoskes)), a module for monitoring logs from multiple sources by using SSH as the transport.  It gives you an object stream, so you can format the results however you want.  You can also easily see each source, because the objects have a `server` property.

This will work really well if you're used to writing `~/.ssh/config` with aliases for servers and keys.  The configuration options for proginoskes allow you to define the port, username, private key, and log file location.  You could easily pipe your server logs to multiple locations for archival purposes, stats, and error notifications.

This project is based on the [ssh2](https://www.npmjs.com/package/ssh2) module which is actually an SSH client by Brian White that's written in JavaScript.  The ssh2 module also exposes a stream-based API, but for the underlying SSH protocol.
