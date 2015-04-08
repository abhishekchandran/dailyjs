---
layout: post
title: "Node Roundup: io.js 1.6.4, npm Semver Calculator, mongots, Join-io"
author: Alex Young
image: "/images/posts/semvernpm.png"
categories:
- node
- libraries
- modules
- web
- express
- middleware
---

###io.js 1.6.4, npm Semver Calculator

io.js 1.6.4 is out, as always check the [io.js changelog for more details](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md).  According to the changelog, the notable changes in this version are fixes for openssl, timers, and [some changes](https://github.com/iojs/io.js/pull/1307) to make it build for Android devices.

![Understanding semantic versions](/images/posts/semvernpm.png)

In [npm Weekly, #11](http://blog.npmjs.org/post/115777167035/npm-weekly-11), a really cool [semantic versioning calculator](http://semver.npmjs.com) is mentioned.  If you've been writing versions like `~1.1.0` but don't completely understand what this means, the calculator will show you which versions the string refers to.  The source is available here: [GitHub: npm/semver.npmjs.com](https://github.com/npm/semver.npmjs.com), and works using Browserify, Angular, and npm build scripts.

It uses [npm-registry-cors-proxy.herokuapp.com](http://npm-registry-cors-proxy.herokuapp.com/express) to fetch package metadata rather than directly hitting npm.  Presumably that's because npm's web API doesn't have JSONP or CORS (yet?).

###mongots

If you're interested in MongoDB and TypeScript, then take a look at Prabhu Subramanian's mongots (GitHub: [prabhu/mongots](https://github.com/prabhu/mongots), License: _MIT_).  The author says it supports everything MongoJS does and passes the same tests.  It's not yet available on npm -- he's working on a stable version before releasing it.

###Join-io

Most of us concatenate scripts to reduce request counts, but what about piping them?  Join-io (GitHub: [coderaiser/join-io](https://github.com/coderaiser/join-io), License: _MIT_, npm: [join-io](https://www.npmjs.com/package/join-io)) is a middleware component that allows you to specify `script` or `link` paths like this: `/join:/lib/client.js:/lib/util.js:/lib/jquery.js`.  When this hits your Express server, join-io will stream each file to the browser.

The author has built this module on top of [files-io](https://github.com/coderaiser/files-io), which is a more generalised API for piping collections of files.  And, naturally, files-io is written with [pipe-io](https://github.com/coderaiser/pipe-io)!
