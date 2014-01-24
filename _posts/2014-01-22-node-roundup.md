---
layout: post
title: "Node Roundup: Nodemon 1.0, Prana, termcoin, node-bitwise-xor"
author: Alex Young
categories:
- node
- modules
- bitcoin
- mongodb
---

###Nodemon 1.0

![Nodemon](/images/posts/nodemon-logo.png)

I noticed [Nodemon 1.0](http://remysharp.com/2014/01/20/nodemon-1-0/) was released this week (GitHub: [remy / nodemon](https://github.com/remy/nodemon), License: _MIT_, npm: [nodemon](https://npmjs.org/package/nodemon)).  This update includes local and global configuration files, `execMap` for mapping file extensions to programs, and some changes to the overall architecture of the project.  You can now `require` Nodemon, and tests have been added.

###Prana

[Prana](http://pranajs.com/) (GitHub: [recidive / prana](https://github.com/recidive/prana), License: _MIT_, npm: [prana](https://npmjs.org/package/prana)) by Henrique Recidive is a small framework for Node applications.  Prana application objects are EventEmitters, and Prana "types" emit events as well.

It combines an ODM system with a plugin system, and currently persists data to memory or MongoDB.  The author has included some examples which you can find in [prana/examples](https://github.com/recidive/prana/tree/master/examples), and one of them uses Express.  The module's code itself has detailed comments, and the readme is solid too.

###termcoin

termcoin (GitHub: [chjj / termcoin](https://github.com/chjj/termcoin), License: _MIT_, npm: [termcoin](https://npmjs.org/package/termcoin)) by Christopher Jeffrey is a terminal Bitcoin client with a curses interface.  It requires bitcoind to work, and looks really cool in the screenshots.

###node-bitwise-xor

Stanislas Marion sent in node-bitwise-xor (GitHub: [czzarr / node-bitwise-xor](https://github.com/czzarr/node-bitwise-xor), License: _MIT_, npm: [bitwise-xor](https://npmjs.org/package/bitwise-xor)), a module for performing a bitwise XOR on two buffers or strings.  It iterates over each element with `^`, taking into account the length to ensure each item is changed.

