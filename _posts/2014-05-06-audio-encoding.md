---
layout: post
title: "Browser Audio Encoding, Atom Open Source"
author: Alex Young
categories:
- audio
- encoding
- mp3
- ogg
- editors
- atom
---

###Vorbis.js

Joe Sullivan sent in vorbis.js (GitHub: [itsjoesullivan/libvorbis.js](https://github.com/itsjoesullivan/libvorbis.js), License: _MIT_), a project based on several others that produces Ogg Vorbis from PCM data.  It uses Emscripten, and has an event-based API.  There's a full example in the readme, which demonstrates how to configure the necessary memory buffers and encoding options.

Joe has also made a project called [iago](https://github.com/itsjoesullivan/iago) that can stream Ogg using web workers.

If licensing issues don't put you off, take a look at [libmp3lame.js](https://github.com/akrennmair/libmp3lame-js) by Andreas Krennmair.  Again, this project makes use of Emscripten to port parts of [lame](http://lame.sourceforge.net/) to JavaScript.

###Atom is Open Source

[Atom is now free and open source](https://github.com/blog/1831-atom-free-and-open-source-for-everyone).  The announcement includes the minor revelation that there are now over 800 [Atom packages](https://atom.io/packages).

I've seen people on Twitter running the Linux version, but people are still dubious about Atom's performance and the 2 MB file limit.  Making it open source seems like a solid first step to creating sustained interest, but it has a Google Wave feel about it.
