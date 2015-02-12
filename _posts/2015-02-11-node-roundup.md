---
layout: post
title: "Node Roundup: 0.12.0, vmd, NtSeq"
author: Alex Young
categories:
- node
- libraries
- modules
- bioinformatics
---

### Node 0.12.0

A new day, a new branch (a new fork?)! [Node 0.12.0 is out](http://blog.nodejs.org/2015/02/06/node-v0-12-0-stable/), and it includes some major changes:

* Streams 3
* Core module changes: HTTP, Cluster, TLS, Buffer, child_process, Crypto
* The sandboxing is now magical

I tried 0.12.0 with some of my production projects and found several dependencies didn't work, so you need to be careful before switching from 0.10.x.

Obviously the streams 3 API is interesting, and I seem to remember reading several discussions about it on the Node Google Group and IRC.  I kind of forgot about it, so now I'm scrambling to figure out what new stuff it'll let us do.  I'm also half-way through Wolf Hall so it may take a few weeks...

> The Streams implementation now works the way you thought it already should, without introducing any changes to the API. Basically this means no more getting stuck in "old mode", there are only streams that are flowing or not.

There's a good [StrongLoop post](http://strongloop.com/strongblog/whats-new-io-js-beta-streams3/) that explains how it relates to the two previous APIs:

> Streams 1 introduced push-streams to allow developers to consume data efficiently. Streams 2 added pull-streams in addition to push-streams to allow advanced use-cases, however, the two styles could not be used together. Streams 3 solves this issue in an elegant manner and allows the same stream to be used in both push and pull mode. Streams3 is available in Node v0.11/v0.12 and io.js.

Very soon after, [io.js 1.2.0](https://iojs.org/dist/v1.2.0/) was released.  Again the io.js release includes patches that aren't present in Node.  JavaScript programmers are increasingly switching to io.js because of these patches and the fact it very openly adopts ES6, so the pressure is definitely growing on the Node maintainers.

In the bizarre world of Node/io.js politics, you'll also find Joyent reiterating the importance [Node.js Foundation](https://www.joyent.com/blog/introducing-the-nodejs-foundation). This translates to "IBM, Microsoft, PayPal love us, and so should you".  And elsewhere [Nodejitsu joins GoDaddy](http://blog.nodejitsu.com/nodejitsu-joins-godaddy/), which is another corporate move I'm not impressed by:

> Nodejitsu products will continue to run for the next seven months, then shutdown.
> As an added bonus our Open Source contributions are going to get a serious boost through the added engineers and resources of a world-class organization like GoDaddy. OSS at GoDaddy has grown significantly in the last few years and we’re excited to be on board to help it continue to evolve.

I thought Nodejitsu had a reasonable PaaS service and was a viable alternative to Azure and Heroku.  I think Azure and Heroku are great, but it's we need other options. There are still some independent PaaS services out there, but will they all fall to acquihiring?

###vmd

vmd (GitHub: [yoshuawuyts/vmd](https://github.com/yoshuawuyts/vmd), License: _MIT_, npm: [vmd](https://www.npmjs.com/package/vmd)) by Yoshua Wuyts is a desktop Markdown preview tool.  Yes, another desktop app that you can install with npm!  It's made with [atom-shell](https://www.npmjs.com/package/atom-shell), so if you're interested in building desktop apps with Node then you should check out atom-shell and vmd to see how they work:

> Atom Shell is a javascript runtime that bundles Node.js and Chromium. You use it similar to the node command on the command line for executing javascript programs. This module helps you easily install the atom-shell command for use on the command line without having to compile anything.

###NtSeq

[NtSeq](http://keithwhor.github.io/NtSeq/) (GitHub: [keithwhor/NtSeq](https://github.com/keithwhor/NtSeq), License: _MIT_, npm: [ntseq](https://www.npmjs.com/package/ntseq)) by Keith William Horwood is a bioinformatics library that provides DNA sequence manipulation.  You can use it in Node and the browser, and it comes with some Node-friendly benchmarks so you can install and test it fairly painlessly.

> More specifically, it's a library for dealing with all kinds of nucleotide sequences, including degenerate nucleotides. It's built with the developer (and scientist) in mind with simple, readable methods that are part of the standard molecular biologist's vocabulary.

It's always good to see Node modules for science!
