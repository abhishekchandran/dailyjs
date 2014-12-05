---
layout: post
title: "Node Advisory Updates and Node Forks"
author: "Alex Young"
image: "/images/posts/node-advisory-board.png"
categories: 
- community
- node
---

As someone who works professionally with Node and writes about it regularly, I've naturally been following the discussions about Node forks and the Node advisory board.  I've been collecting articles in Instapaper and highlighting things like crazy to figure out what's going on.

On Wednesday TJ Fontaine posted an [advisory board update](http://blog.nodejs.org/2014/12/03/advisory-board-update/) on the official Node blog.  The board has had three meetings so far which you can follow on GitHub: [nodejs-advisory-board/meetings](https://github.com/joyent/nodejs-advisory-board/tree/master/meetings).

The most recent minutes mention the ongoing discussions about the Node trademark:

> The group will utilize Mongo, Eclipse, and Docker as examples projects to draw from. Agreed that there is no certification products and since there is no process to do that, there will be no certification for training or product compatibility. Project teams should be publishing the acceptance testing and organizations that want to test against the test suite and should be posting the results to the node.js repo

The advisory board have decided that the Node project should be run based on a consensus, rather than a dictatorship:

> One thing that we all agree on, is that we're not going to be using the Benevolent Dictator model. In fact, recently the project hasn't been operating that way. We can be more clear about that in our documentation. We all agree we want a healthy and vibrant team, a team focused on making progress for Node.js, not for progress's sake, but for the betterment of the software project and the community we serve.
>
> The goal of the team, especially that of the project lead, is to drive consensus and ensure accountability.

This is followed by a list that indicates how API changes will be handled in the future.  Also, there is news about Node 0.12:

> Finally, we are very close to releasing v0.12, there's only one major patch we're waiting to land. Once that's done we'll be releasing v0.11.15 as a release candidate.

StrongLoop's blog has a related post about [their position on a major Node fork](http://strongloop.com/strongblog/position-on-io-js/) called [io.js](http://iojs.org/):

> As it has been widely reported, last week a fork of Node went live called io.js. Io.js represents a technical exploration by key developers in the Node core community with the intent to accelerate the release of recent technical innovations, many of which were developed by StrongLoop developers.
> 
> At StrongLoop, we've always participated in leadership, advisory and technical efforts in the Node ecosystem when appropriate and will continue to do so. We actively play a role in the Node Advisory Board established by Joyent in October 2014.

Although this sounds like StrongLoop is endorsing Node for now, the author indicates that StrongLoop remains open to changes in the future:

>  We will continue to recommend the version that currently has the best community support, is most compatible with the tools and frameworks we develop and that we can support for our customers. Of course, our preference over time is to support a version that satisfies these requirements and adheres to an open governance model.

There's [an article on Wired](http://www.wired.com/2014/12/io-js/) that quotes Mikeal Rogers citing Joyent's control as a reason for the fork:

> "We don't want to have just one person who's appointed by a company making decisions," says Mikeal Rogers, a Node community organizer involved in the fork. "We want contributors to have more control, to seek consensus."

Of course other contributing factors must be the perceived slow progress of the 0.12 release.  It's possible that io.js will exist as a novel fork that influences mainstream Node, or it could be like Chrome vs. previous less popular WebKit browsers.  My advice is to follow both and avoid judging either too soon.
