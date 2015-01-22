---
layout: post
title: "Terminal.js: A Terminal Emulator Library"
author: Alex Young
categories:
- client-side
- node
- libraries
- modules
---

![Terminal.js](/images/posts/terminaljs.gif)

These days the terms _VT100_ and _terminal_ are synonymous with either text-based interfaces or a shell.  But there was a time when terminal referred to "computer terminal" -- a machine that allows you to input commands into a computing system and view the results.  This includes CRTs and teletype printers.  The VT100 terminal was based on an Intel 8080, and if I remember my computer history correctly represents a transitory stage between the era of remote mainframes and local minicomputer systems.

The thing that's interesting about the VT100 is it implemented some of the ANSI escape code sequences that we still use to annoy people on IRC and make quirky command-line tools.  So when you see a terminal emulator set to VT100, it means it supports the features the VT100 had for cursor movement, clearing the display, and so on.

[Terminal.js](http://gottox.de/terminal.js/) (GitHub: [Gottox/terminal.js](https://github.com/Gottox/terminal.js), License: _MIT/X Consortium License_, npm: [terminal.js](https://www.npmjs.com/package/terminal.js)) by Enno Boland is a VT100 emulator that works in browsers and Node.  Enno has also published [node-webterm](https://github.com/Gottox/node-webterm), which you can use to try out the project in a browser.

The API allows you to create a terminal object, write data to it, and get data back out.  This demo uses the [colors](https://www.npmjs.com/package/colors) module:

{% highlight javascript %}
var colors = require('colors');
var Terminal = require('terminal.js');
var terminal = new Terminal({ columns: 20, rows: 2 });

terminal.write('Terminal.js in rainbows'.rainbow);
console.log(terminal.toString('ansi'));
{% endhighlight %}

Internally, the source is split into handler, input, and output modules.  The handlers are basically JSON maps between characters and internal state.  For example, [handler/esc.js](https://github.com/Gottox/terminal.js/blob/master/lib/handler/esc.js) has the escape code handlers for things like moving the cursor down a column (`ESC D`).

You could use this module to provide a command-line interface to web-based developer tools, or maybe even make your own Chrome OS/iOS-friendly IDE.  The node-webterm example demonstrates how to connect the terminal up with WebSockets, so it actually feels pretty low latency.  Check out [node-webterm/index.html](https://github.com/Gottox/node-webterm/blob/acb81a8340a34b0864ade932ff51155bc5e720a1/index.html) to see how that can be implemented!
