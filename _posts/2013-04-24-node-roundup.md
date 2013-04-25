---
layout: post
title: "Node Roundup: 0.10.5, Node Task, cap"
author: "Alex Young"
categories: 
- node
- modules
- grunt
- network
- security
- streams
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.5

[Node 0.10.5](http://blog.nodejs.org/2013/04/23/node-v0-10-5-stable/) is out.  Apparently it now builds under Visual Studio 2012.

One small change I noticed was added by Ryan Doenges, where the assert module now puts information into the `message` property:

> 4716dc6 made `assert.equal()` and related functions work better by generating a better `toString()` from the expected, actual, and operator values passed to `fail()`. Unfortunately, this was accomplished by putting the generated message into the error's name property. When you passed in a custom error message, the error would put the custom error into name and message, resulting in helpful string representations like `"AssertionError: Oh no: Oh no"`.

The [pull request for this](https://github.com/joyent/node/pull/5293) is nice to read (apparently Ryan is only 17, so he got his dad to sign the _Contributor License Agreement_ document).

###Node Task

[Node Task](https://github.com/node-task/spec/wiki), sent in by Khalid Khan, is a specification for a promise-based API that wraps around JavaScript tasks.  The idea is that tasks used with projects like Grunt should be compatible, and able to be processed through an arbitrary pipeline:

> Eventually, it is hoped that popular JS libraries will maintain their own node-task modules (think jshint, stylus, handlebars, etc). If/when this happens, it will be trivial to pass files through an arbitrary pipeline of interactions and transformations utilizing libraries across the entire npm ecosystem.

After reading through each specification, it seems like an interesting attempt to standardise Grunt-like tasks.  The API seems streams-inspired, as it's based around EventEmitter2 with various additional methods that are left for implementors to fill in.

###cap

Brian White sent in his cross-platform packet capturing library, "cap" (GitHub: [mscdex / cap](https://github.com/mscdex/cap), License: _MIT_, npm: [cap](https://npmjs.org/package/cap)).  It's built using WinPcap for Windows and libpcap and libpcap-dev for Unix-like operating systems.

It's time to write your vulnerability scanning tools with Node!

Brian also sent in "dicer" (GitHub: [mscdex / dicer](https://github.com/mscdex/dicer), License: _MIT_, npm: [dicer](https://npmjs.org/package/dicer)), which is a streaming multipart parser.  It uses the streams2 base classes and [readable-stream](https://npmjs.org/package/readable-stream) for Node 0.8 support.

