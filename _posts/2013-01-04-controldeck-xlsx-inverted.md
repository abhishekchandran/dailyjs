---
layout: post
title: "Inverted, controldeck.js, xlsx"
author: Alex Young
categories:
- libraries
- excel
- spreadsheets
- presentations
- oo
---

###Inverted

[Inverted](http://philmander.github.com/inverted/) (GitHub: [philmander / inverted](https://github.com/philmander/inverted), License: _MIT_, npm: [inverted](https://npmjs.org/package/inverted)) by Phil Mander is an [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control) container.  Used in conjunction with AMD, Inverted uses a separate configuration file to express how classes are instantiated and how they interact.  Once these defaults and relationships have been defined, an application context can be created, and instances of the classes can be used.

Phil has provided several examples on the Inverted site that use AMD, but he's also included a CommonJS example that could be used with Node.  The API is mostly based around callbacks.  For example, fetching an instance is performed with `appContext.getProto('name', fn)`, where `fn` receives the instance as the first argument.

> JavaScript module loading systems such as the CommonJS and AMD manage the loading of your application's dependencies, but they don't actually inject dependencies and wire your code together. Inverted uses a separate application configuration file to define how your Javascript 'classes' interact without needing to add any library specific code within your modules.

###controldeck.js

<div class="image">
  <img src="/images/posts/controljs.png" alt="" />
  <small>One of the controldeck.js demos.</small>
</div>

[controldeck.js](http://dfcb.github.com/controldeck.js/) (GitHub: [dfcb / controldeck.js](https://github.com/dfcb/controldeck.js/), License: _MIT_) from Draftfcb in Chicago is a small Node web application that provides a remote control for HTML presentations.  This offers a simple way of using a mobile phone to control a slideshow.

[Socket.IO](http://socket.io/) is used to communicate between the controller and the slides, and the authors have demos running on [AppFog](http://www.appfog.com/).

###xlsx

[xlsx](http://niggler.github.com/js-xlsx/) (GitHub: [Niggler / js-xlsx](https://github.com/Niggler/js-xlsx), License: _MIT_, npm: [xlsx](https://npmjs.org/package/xlsx)) by Niggler is an implementation of the ISO 29500 Office Open XML specification.  The author states that it has been tested with some simple Excel 2011 files, but is still a nascent attempt at supporting the format.

It's designed to work with Node and browsers, and the project's homepage has a browser-based demo.  This project was created in response to Stephen Hardy's [xlsx.js](https://github.com/stephen-hardy/xlsx.js) project -- there was a lengthy discussion on the license of the project which some felt is ambiguous: [stephen-hardy / xlsx.js, issue #8: Use a more permissive license](https://github.com/stephen-hardy/xlsx.js/issues/8).

