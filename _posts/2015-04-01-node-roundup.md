---
layout: post
title: "Node Roundup: Node 0.12.2, io.js 1.6.3, JXcore, Osmosis"
author: Alex Young
categories:
- node
- libraries
- modules
- iojs
- npm
- build
---

###Node 0.12.2

Is Node ramping up to regular iterative releases again?  This week [Node 0.12.2](http://blog.nodejs.org/2015/03/31/node-v0-12-2-stable/) was released, which upgrades the core binary dependencies, fixes a V8 issue, and has bug fixes for the core modules.  Some of these commits go back to things we saw in February in io.js that I believe came from commits to Node that io.js picked up.  For example, the commit for [allow Object.prototype fields as labels](https://github.com/joyent/node/commit/c8239c08d7ad7d375683fd85745b30da789bb591) goes back to a backport of [an earlier commit](https://github.com/joyent/node/commit/6c3647c38d73f729ce85633a0440cd939d93dea2).

Comparing the commits in 0.12.2 to [io.js's changelog](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) shows that most of them have already been released -- the newest commit currently in Node's stable branch was in io.js 1.5.

Speaking of io.js, yesterday io.js 1.6.3 was released.  There's a bug fix for `fs` that stood out to me:

* [[`c9207f7fc2`](https://github.com/iojs/io.js/commit/c9207f7fc2)] - **fs**: fix corruption in writeFile and writeFileSync (Olov Lassus) [#1063](https://github.com/iojs/io.js/pull/1063)

And there are several commits that improve code quality.  This release seems pretty big, so keep an eye on [their weekly review post on Medium](https://medium.com/@iojs) for an overview.

###JXcore

There are more Node forks out there! [JXcore](http://jxcore.com/) (GitHub: [jxcore/jxcore](https://github.com/jxcore/jxcore)) is a Node-compatible platform that aims to support mobile devices.  It's embeddable, supports multiple JavaScript engines (V8 and SpiderMonkey), and also supports ES6.

One of the core developers, Ugur Kadakal, sent me an email about the project, and claimed it allows applications to run on iOS.  I found [a blog post](http://jxcore.com/new-open-source-version-of-jxcore-will-support-ios/) with more details.  There's also documentation for [compiling native apps with jx](http://jxcore.com/document/compiling-2/).  I haven't tried this myself, but it sounds like they've done an impressive amount of work on it so far.

###Osmosis

Here's a new web scraper for Node: Osmosis (GitHub: [rc0x03/node-osmosis](https://github.com/rc0x03/node-osmosis), npm: [osmosis](https://www.npmjs.com/package/osmosis)).  It doesn't have any HTML parsing dependencies because it uses libxml C bindings instead.  It supports both CSS and XPath selectors.

The API includes HTTP and is chainable, so you can do `osmosis.get(url).find(selector).data(callback)` to pull out elements for a selector.  You can also open new URLs based on selectors using `follow`, and transform data using `set()`.

The underlying HTTP layer is provided by [needle](https://github.com/tomas/needle).  Needle itself is an amazing HTTP client, supporting streaming decompression, multipart forms (uploads), character encoding support with iconv-liteiconv-lite, and proxies.

If you're doing lots of scraping, then Osmosis looks like a solid library to try out.  The other one that I've recently been impressed by is [X-Ray](https://github.com/lapwinglabs/x-ray).
