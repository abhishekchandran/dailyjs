---
layout: post
title: "Node Roundup: 0.10.23, 2013, Bull"
author: Alex Young
categories:
- node
- modules
- queue
- redis
---

###Node 0.10.23 Released

[Node v0.10.23](http://blog.nodejs.org/2013/12/11/node-v0-10-23-stable/) is out.  This release upgrades uv, npm, and has patches for several core modules.  I particularly liked "events: avoid calling once functions twice".  This would happen when [emitting an event from inside the event hander](https://github.com/joyent/node/commit/c9d93f34311ce0a9b59ed9f4511a2e3ba69e0f25).  The fix involves using a boolean to track if the event has fired, so it's not too drastic.

###Node in 2013

If I think back over 2013, all I can remember is being punched in the face a lot by my son.  He's a year old, so I'm hoping this sort of thing stops before he gets much bigger.  For those of you who still have brain cells, Gergely Nemeth sent in [a timeline of Node in 2013](http://gergelyke.github.io/node2013/).  This includes news like Ghost getting funded, Nodeschool.io's release, and the ScaleNPM funding drive.

###Bull Job Manager

Manuel Astudillo sent in [Bull Job Manager](https://github.com/OptimalBits/bull) (npm: [bull](https://npmjs.org/package/bull), License: _BSD_).  It's a job queue manager that uses Redis and has an API inspired by LearnBoost's [Kue](https://npmjs.org/package/kue).

Manuel says it's designed with atomicity in mind.  Looking at the source, it uses atomic increments and blocking operations (`BRPOPLPUSH`), so it should be as atomic as Redis is.
