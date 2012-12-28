---
layout: post
title: "CampJS, euh.js, node-startup"
author: Alex Young
categories: 
- conferences
- events
- node
---

###CampJS

![CampJS](/images/posts/campjs.png)

[CampJS](http://campjs.com/) is a weekend-long JavaScript "hack retreat" taking place in Gold Coast Hinterland, Queensland, Australia, from February 15th to the 18th.  Early bird tickets are $270, and then prices go up to $470 by the 1st of February.

Some well-known developers will be there, including Dominic Tarr and James Halliday (substack).

The event is organised by Tim Oxley, Nigel Rausch, and Geoffrey Donaldson.  For more about the event, follow [@campjsnews](https://twitter.com/campjsnews).

###euh.js

[euh.js](https://github.com/CristianTincu/euh.js) (License: _MIT_, npm: [euh.js](https://npmjs.org/package/euh.js)) by Cristian Tincu is a `console` implementation that supports the usual `log`, `warn`, and `error` methods.

It's exposed as the `ø` object, and has a chainable API.  It can be installed with npm and ender (`ender build euh.js`).

###node-startup

[node-startup](https://github.com/chovy/node-startup) (License: _MIT_) by Anthony Ettinger is an init script for managing Node applications.  The script itself, [init.d/node-app](https://github.com/chovy/node-startup/blob/master/init.d/node-app), implements the usual `start`, `stop`, and `restart` commands, and will manage processes using PID files.

It's exactly the kind of thing you can't find when you need it, so it's probably worth starring on GitHub if you're the kind of developer that doesn't typically have to deal with sysadmin tasks.  I wrote about using [Upstart for managing Node apps](http://dailyjs.com/2011/03/07/node-deployment/) last year on DailyJS.
