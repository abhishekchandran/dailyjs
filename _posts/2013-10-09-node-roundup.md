---
layout: post
title: "Node Roundup: Great British Node Conference Edition"
author: "Alex Young"
categories: 
- node
- modules
- npm
- events
- gbnc
---

Yesterday was the [Great British Node Conference](http://greatbritishnodeconf.co.uk/), which took place in London at the [Shoreditch Works Village Hall](http://greatbritishnodeconf.co.uk/).  Speakers included [Julian Gruber](https://twitter.com/juliangruber), [Darach Ennis](https://twitter.com/darachennis), [Anton Whalley](https://twitter.com/antonwhalley), and [Tim Ruffles](https://twitter.com/timruffles).

I did a talk about Node's internals that went from the JavaScript core modules down to some libuv basics, with the aim of encouraging the audience to look at Node's source for themselves.  I want to break this talk down into a deeper analysis of uv and V8 while still remaining relevant to JavaScript developers.

![Substack](/images/posts/gbnc2.png)

Substack did a short talk about abstract syntax trees, Browserify, and a project he's working on to remove unreachable code.  He mentioned [testling](https://github.com/substack/testling), which I haven't seen before -- it's another way to run headless browser tests.  I was recently trying to rethink the way I do this, so I'm going to give it a try.

[Milo Mordaunt](https://twitter.com/bananaoomarang) and [Harry Dalton](https://twitter.com/hooleanplusplus) did an interesting talk about some games they created based on British government data.  One of the games used Max Ogden's [voxel-engine](https://github.com/maxogden/voxel-engine) project.

In the audience I talked to [Sven Lito](https://twitter.com/svenlito) who is one of the creators of [Hoodie](http://hood.ie/).  Hoodie is a [noBackend](http://nobackend.org/) project that aims to make web applications easier to build.  It reminded me of Meteor, but my initial impression was that it's more closely reliant and influenced by the Node community, so I'd like to spend more time looking at it.

Over the next week or so I'll write a little bit more about the projects and technologies I learned about at the conference.
