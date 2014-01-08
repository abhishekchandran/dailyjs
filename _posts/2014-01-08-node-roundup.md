
---
layout: post
title: "Node Roundup: Faucet, Node Compiler, Tumblr"
author: Alex Young
categories:
- node
- modules
- testing
- tap
---

###Faucet

Faucet (GitHub: [substack / faucet](https://github.com/substack/faucet), License: _MIT_, npm: [faucet](https://npmjs.org/package/faucet)) by Substack is a human-readable TAP summariser.  You can pipe TAP text into the `faucet` command-line script, and it'll generate prettier yet concise output.

If you type `faucet`, JavaScript files in `test/` will be executed using `tape` and then automatically piped through `faucet`.

Substack has created some nice animated gifs that show what the results look like under various conditions.  One of them even shows Mocha using tap through the `-R tap` command-line option.

###Node Compiler

![Node Compiler](/images/posts/nodecompiler.png)

Sonny Lazuardi sent in [Node Compiler](http://sonnylab.com/api/compiler) (GitHub: [sonnylazuardi / node-compiler](https://github.com/sonnylazuardi/node-compiler), License: _MIT_), a web-based tool for building C++.  It uses `g++` with [execSync](https://github.com/mgutz/execSync), wrapped up with an Express-based API.

The web interface uses the Ace editor, which supports traditional editor features like syntax highlighting.  I think it's quite an audacious idea, but it might be a little dangerous to leave on public servers.

###Tumblr

[node-tumblr](http://meritt.github.io/node-tumblr/) (GitHub: [meritt / node-tumblr](https://github.com/meritt/node-tumblr), npm: [tumblr](https://github.com/meritt/node-tumblr)) by Alexey Simonenko is a Tumblr API wrapper for Node.  It supports OAuth, and allows you to query posts, links, answers, and the other resources Tumblr provides.

