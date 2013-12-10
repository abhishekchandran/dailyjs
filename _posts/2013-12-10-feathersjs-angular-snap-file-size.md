---
layout: post
title: "Feathers, Angular Snap.js, File-size.js"
author: "Alex Young"
categories: 
- frameworks
- libraries
- modules
- node
- angularjs
---

###Feathers

[Feathers](http://feathersjs.com/) (GitHub: [feathersjs / feathers](https://github.com/feathersjs/feathers), License: _MIT_, npm: [feathers](https://npmjs.org/package/feathers)), sent in by Matthew Phillips, is an Express-based web framework for creating RESTful services that use Socket.IO.

Because it's based on Express, you can use existing Connect middleware.  That means you could drop in an authentication module like [everyauth](https://npmjs.org/package/everyauth), and your preferred client-side framework (like Backbone.js or AngularJS), and then use the Feathers conventions for CRUD-style server-side code and Socket.IO events.

Matthew wrote a glowing email about it -- he's been using it for client project.  I had a look at the source, and it's actually pretty lightweight: it's basically based around events that bridge between Express routes and Socket.IO.

The main author, David Luecke, has built it with [Rubberduck](https://npmjs.org/package/rubberduck) and [Uberproto](https://npmjs.org/package/uberproto), two of his other modules.  Uberproto is basically inheritance sugar, and Rubberduck allows methods to be wrapped with events.

###Angular Snap.js

[Angular Snap.js](http://jtrussell.github.io/angular-snap.js/) (GitHub: [jtrussell / angular-snap.js](https://github.com/jtrussell/angular-snap.js), License: _MIT_) by Justin Russell is a [Snap.js](https://github.com/jakiestfu/Snap.js) directive for AngularJS.  Snap.js makes mobile-style "shelf" layouts a lot easier, and is intuitive to use -- touch gestures work as expected, and click-dragging the mouse opens the drawer as well.

The directive can be used as an attribute, or event an element:

{% highlight html %}
<div snap-drawer>
  <p>I'm a drawer! I maybe I've got some sweet navigation links.</p>
</div>

<snap-drawer>
  <p>I'm a drawer! I maybe I've got some sweet navigation links.</p>
</snap-drawer>
{% endhighlight %}

###File-size.js

File-size.js (GitHub: [Nijikokun / file-size](https://github.com/Nijikokun/file-size), License: _MIT_, npm: [file-size](https://npmjs.org/package/file-size)) by Nijiko Yonskai is a module for generating human-readable file sizes.  For example, `filesize(186457865).to('MB')` returns `177.82`.

It supports various specifications, including JEDEC and IEC, and it works in browsers and Node.
