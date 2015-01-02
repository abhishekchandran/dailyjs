---
layout: post
title: "Node Roundup: nchat, hulken, cult"
author: Alex Young
categories:
- node
- modules
- libraries
- command-line
- gulp
- build-tools
- chat
- websocket
---

###nchat

nchat (GitHub: [irrationalistic/nchat](https://github.com/irrationalistic/nchat), npm: [nchat](https://www.npmjs.com/package/nchat)) by Chris Rolfs is a terminal-based chat application that uses WebSocket, which means it's easier to use on networks where IRC might be blocked.

Notifications are supported on Mac OS X, and the client can run as the server so you only need to install nchat itself.  It supports a few IRC-style commands, like `/users`, and you can deploy it to hosting providers like Heroku.

###hulken

[Hulken](http://hellgrenj.github.io/hulken/) (GitHub: [hulken](https://github.com/hellgrenj/hulken), License: _MIT_, npm: [hulken](https://www.npmjs.com/package/hulken)) by Johan Hellgren is a stress testing tool for HTTP services.  It can make GET and POST requests, and can be configured to send dynamic payloads.

You can use hulken as a command-line tool, or a Node module.  The documentation includes all of the supported options, and you'll need to write an `options.json` file to use it on the command-line.

###cult

Cult (GitHub: [typicode/cult](https://github.com/typicode/cult), License: _MIT_, npm: [cult](https://www.npmjs.com/package/cult)) is a tool that monitors changes to a gulpfile and then reloads Gulp.  You can run it on the command-line, and it uses the [chalk](https://www.npmjs.com/package/chalk) library for pretty output.  The readme has an example for supporting gulpfiles that are split across multiple files.
