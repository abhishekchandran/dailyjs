---
layout: post
title: "Node Roundup: npm and Heartbleed, sipster"
author: "Alex Young"
categories:
- node
- modules
- npm
- audio
- telephony
- voip
---

###npm and Heartbleed

The npm blog has an article about [npm and Heartbleed](http://blog.npmjs.org/post/82107114489/npm-and-heartbleed):

> We started patching machines within 30 minutes of the revelation of the bug, and our last vulnerable machine was patched at 7.30am Pacific today.

> There has been no evidence so far that our keys were compromised during this period, but nevertheless we are regenerating all our SSL keys anyway and will be rolling them out over the next couple of days (we are very cautious about testing and rolling out new certs since an earlier incident in which we broke a lot of older npm clients while doing so).

###sipster

Brian White sent in sipster (GitHub: [mscdex / sipster](https://github.com/mscdex/sipster), License: _MIT_, npm: [sipster](https://www.npmjs.org/package/sipster)), a pjsip binding for Node.  This is the basis for the SIP driver used by Asterisk 12+.  He hasn't yet been able to get a working build environment set up for Windows, but it should work for Unix systems.

Here's a list of what Brian says it can do so far:

* Make and receive calls
* Play either individual or a playlist of wav files (ulaw, alaw, or pcm)
* Record audio to wav file (ulaw, alaw, or pcm)
* Hook up audio streams from different calls (e.g. create your own conference or record a mix of streams to wav)
* Adjust volume levels of audio streams
* Detect/Send DTMF digits
* Hold/un-hold
* Call transfer

The API is event based -- for example: `call.on('dtmf', cb)`, and I think the C++ binding is a cool example of a Node native module: [src/binding.cc](https://github.com/mscdex/sipster/blob/master/src/binding.cc).
