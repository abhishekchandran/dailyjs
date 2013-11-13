---
layout: post
title: "Node Roundup: 0.10.22, genome.js, Bellhop"
author: "Alex Young"
categories: 
- node
- modules
- biology
- streams
---

###Node 0.10.22

[Node 0.10.22](http://blog.nodejs.org/2013/11/12/node-v0-10-22-stable/) was released this week.  This version has fixes for `process`, the debugger and the repl, and a memory leak on closed handles.

There's also a fix for Mac OS 10.9: apparently "Not Responding" was displayed in Activity Monitor for Node processes.

###genome.js

![DNA card](/images/posts/genomejs.png)

[genome.js](http://genomejs.com/) is an interesting project that proclaims "Welcome to the OpenDNA movement":

> genome.js is a fully open source platform built on Node.js that utilizes streams for high-performance analysis of DNA SNPs

There are currently several related repositories for the overall project on GitHub:

* [genomejs / dna2json](https://github.com/genomejs/dna2json): Formats your DNA file as JSON
* [genomejs / gql](https://github.com/genomejs/gql): Query language for interpreting genome SNPs
* [genomejs / genoset-male](https://github.com/genomejs/genoset-male): Determines if a genome is male (GS144)

Why is this useful?  Perhaps you've had your genome sequenced by a site like 23andMe, and want to do something with the data.  Apparently the cutting edge in [web-based DNA browsing](http://genome.ucsc.edu/cgi-bin/hgTracks?position=chr10:69713986-69714099&hgsid=352821589&mrna=pack) isn't particularly great, so there may be room for innovation.

###Bellhop

Bellhop (GitHub: [mscdex / bellhop](https://github.com/mscdex/bellhop), License: _MIT_, npm: [bellhop](https://npmjs.org/package/bellhop)) by Brian White is a stream for Pub/Sub and RPC.  It can serialize data types that aren't supported by JSON.  Bellhop streams should work over any transport, from HTTP to TCP sockets.

The project has tests, and the readme includes API examples.
