---
layout: post
title: "WebGL Head Tracking, Clouseau, ColtJS"
author: Alex Young
categories: 
- webgl
- mvc
- testing
- node
---

###WebGL Head Tracking

![headtrackr](/images/posts/headtracker.png)

In [Move a Cube With Your Head or Head-Tracking With WebGL](http://learningthreejs.com/blog/2013/03/12/move-a-cube-with-your-head/), Jerome Etienne talks about 3D head tracking using Three.js and [WebRTC](http://www.webrtc.org/).  He's using a library for face and head tracking called [headtrackr](https://github.com/auduno/headtrackr) by Audun Mathias Øygard, which has been used to create some interesting demos and games (check out [Targets](http://auduno.github.com/headtrackr/examples/targets.html) and [FaceKat](http://www.shinydemos.com/facekat/)).

###Clouseau

Clouseau (GitHub: [hull / clouseau](https://github.com/hull/clouseau), License: _MIT_, npm: [clouseau-js](https://npmjs.org/package/clouseau-js)) by Xavier Cambar tracks applications using PhantomJS combined with [Q](http://github.com/kriskowal/q).  It basically provides a lightweight integration testing solution:

> Once you've defined invariants in your app, you provide Clouseau with functions to assert them. Then Clouseau will open in PhantomJS the URL at which your app resides and will applies these functions.

It can be used for testing, but the author also notes it works for monitoring long-running applications.

###ColtJS

[ColtJS](http://coltjs.com/) (GitHub: [Fluidbyte / ColtJS](https://github.com/Fluidbyte/ColtJS), License: _MIT_) is a framework for creating AMD-based applications.  It supports routing, templates, URL parsing, network calls, events, storage, and pub/sub:

> ColtJS is a simple framework allowing for easy deployment of JavaScript Application using asynchronous module definition. Its only dependency is RequireJS and it builds off simple principles of a centralized router loading modules only when requested to produce an efficient, easy-to-manage application structure.

