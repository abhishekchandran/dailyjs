---
layout: post
title: "Dependent Types for JavaScript, radioactive.js, Minimail"
author: "Alex Young"
categories:
- computer-science
- education
- email
- apps
---

###Dependent Types for JavaScript

[Dependent Types for JavaScript](http://lambda-the-ultimate.org/node/4700) published on Lambda the Ultimate is about Dependent JavaScript (DJS), a [statically-typed dialect of JavaScript by Ravi Chugh, David Herman, and Ranjit Jhala](http://cseweb.ucsd.edu/~rchugh/research/nested/djs.pdf) (pdf):

> DJS supports the particularly challenging features such as run-time type-tests, higher-order functions, extensible objects, prototype inheritance, and arrays through a combination of nested reﬁnement types, strong updates to the heap, and heap unrolling to precisely track prototype hierarchies

The paper has a summary of related work that will be interesting to those of you who are experimenting with dialects of JavaScript with different type models.

###radioactive.js

[radioactive.js](http://rein.pk/radioactive-js/) (GitHub: [reinpk / radioactive](https://github.com/reinpk/radioactive), License: _MIT_) by Peter Reinhardt is a library for modelling nuclear physics.  Its intended use is for creating interactive demonstrations of radioactive decay:

> One of the biggest problems I've encountered in writing about nuclear reactors is that people don't understand radioactive decay. This is a huge problem because it means that 99% of the population is totally unqualified to decide anything about nuclear energy.

> Suppose I have 1 kg of Cesium-134, with a half-life of 30 years. And 1 kg of Uranium-238, with a half-life of 4.5 billion years. I'm going to give you one of the blocks, and you have to sleep with it tonight like a teddy bear.  Which one do you want?

> If you guessed Cesium-134, you're dead.

So, if you often find yourself presented with various radioactive isotopes and don't want to die, Peter's library may be of use to you.  Or else you're creating presentations or simulations using [D3.js](http://d3js.org/) that you want to have some level of accuracy.

###Minimail

[Minimail](https://minimail.herokuapp.com/app/) (GitHub: [emailbox / minimail_mobileapp](https://github.com/emailbox/minimail_mobileapp), License: _BSD3_) by Nicholas Reed is a mobile and server-side project to create a developer-friendly email client:

> It is at the alpha stage, which means it kinda, sorta runs on Android and iOS, and is usable as a replacement mobile client (with changes synced to your Gmail web interface). I made it because there currently are no mobile email clients that are built with common frontend web languages. I'd like to see anyone able to run their own custom email client that fits their workflow.

It's built using PhoneGap, and the server is Node with MongoDB.
