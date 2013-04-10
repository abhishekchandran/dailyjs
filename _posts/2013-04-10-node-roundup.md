---
layout: post
title: "Node Roundup: 0.8.23, indev, compressjs"
author: "Alex Young"
categories: 
- node
- modules
- build
- compression
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.8.23

In case you haven't switched to 0.10 yet, [Node 0.8.23 was released yesterday](http://blog.nodejs.org/2013/04/08/node-v0-8-23-stable/).  This version adds bug fixes for the http, tls, child_process, and crypto modules.

###indev

indev (GitHub: [azer / indev](https://github.com/azer/indev), License: _BSD_, npm: [indev](https://npmjs.org/package/indev)) by Azer Koçulu is a lightweight alternative to Makfiles.  It supports "Devfiles" which can be written in either CoffeeScript or JavaScript, and includes shortcuts for lots of shell commands through [ShellJS](https://github.com/arturadib/shelljs).

The inclusion of ShellJS makes it feel closer to make than Grunt, so if Grunt isn't quite what you want then indev might be what you're looking for.

###compressjs

compressjs (GitHub: [cscott / compressjs](https://github.com/cscott/compressjs), License: _GPLv2_, npm: [compressjs](https://npmjs.org/package/compressjs)) by C. Scott Ananian features several compression algorithms, implemented in pure JavaScript.  It can run in browsers, and includes bzip2, LZP3, a modified LZJB, PPM-D, and an implementation of [Dynamic Markov Compression](http://en.wikipedia.org/wiki/Dynamic_Markov_Compression).

The readme includes benchmarks for each algorithm, and a script is included so you can use it to compress things on the command-line.

