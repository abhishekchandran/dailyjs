---
layout: post
title: "Node Roundup: The Future of Node, takeapeek, subtitle"
author: "Alex Young"
categories: 
- node
- modules
- subtitles
- video
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###The Future of Node

[Yakulu](https://news.ycombinator.com/user?id=Yakulu) posted [The Future of Programming in Node.js](https://groups.google.com/d/msg/nodejs/9afurRCTlOc/JKVo0ThFZIsJ) to Hacker News, which is a long message by Isaac Schlueter on the [nodejs Google Group](https://groups.google.com/forum/#!forum/nodejs):

> Callbacks will remain the de facto way to implement asynchrony.  Generators and Promises are interesting and will remain a userland option.

> This is not a democracy.  However, there's plenty of room for everyone's opinion.  If you want to make exciting dramatic breaking changes to node-core, and you can't find satisfaction by writing userland npm modules, then please fork joyent/node, give it a new name and logo, and go as completely crazy as you want.

It sounds like the Node core developers are focusing on keeping Node maintainable, rather than jumping on whatever new language or API style is currently fashionable.  I like this approach, because after working with faddish web frameworks that resulted in unmaintainable projects after a surprisingly short amount of time, the idea of a stable and calm core library is definitely welcome.

There were cries of a lack of innovation in the comments, setting off an interesting discussion about the future of Node.  Eventually the comparison with Meteor was brought up, and Isaac talks about how it differs to Node, npm, and even how the Meteor community is managed.

It's required reading for those of us investing in Node for the next few years.

###takeapeek

takeapeek (GitHub: [giodamelio / takeapeek](https://github.com/giodamelio/takeapeek), License: _MIT_, npm: [takeapeek](https://npmjs.org/package/takeapeek)) by Gio d'Amelio is a command-line web server in the spirit of `python -m SimpleHTTPServer`.  It supports directory indexes, and allows settings to be saved in `.takeapeekrc`.  You can also use it as a module in Node.

It's built with [connect](https://npmjs.org/package/connect), and was inspired by [glance](https://github.com/jarofghosts/glance) by Jesse Keane.

###subtitler

subtitler (GitHub: [aetheon / node-opensubtitles-client](https://github.com/aetheon/node-opensubtitles-client), License: _BSD_, npm: [opensubtitles-client](https://npmjs.org/package/opensubtitles-client)) by Oscar Brito is an open subtitles API client.

It has a command-line tool for downloading subtitle files, and also has an event-based, asynchronous JavaScript API.
