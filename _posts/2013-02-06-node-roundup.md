---
layout: post
title: "Node Roundup: GNOME, fs, procjs"
author: "Alex Young"
categories: 
- node
- modules
- gnome
- desktop
- bindings
- browser
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###JavaScript and GNOME

[GNOME now recommends JavaScript for authoring GNOME applications](http://treitter.livejournal.com/14871.html).  For information on what this means for the near future of GNOME desktop development, see [JavaScript in GNOME](https://live.gnome.org/JavaScript).  Although it looks like they're using SpiderMonkey rather than Node, Jérémy Lal sent in an email detailing his positive experiences with node-gir (GitHub: [creationix / node-gir](https://github.com/creationix/node-gir), npm: [gir](https://npmjs.org/package/gir)) by Tim Caswell which provides bindings for [GObject Introspection](https://live.gnome.org/Gjs).

These bindings can be used to make dynamic calls to any library that has GI annotations installed -- Jérémy said he was using it to generate PDFs from HTML.

###Component: fs

fs (GitHub: [matthewp / fs](https://github.com/matthewp/fs), License: _MIT_, component: _matthewp/fs_) by Matthew Phillips is a component that brings Node's `fs` module to the browser.  It's designed to be cross-browser, with the FileSystem API for Chrome and IndexedDB for Firefox and Internet Explorer.

###procjs

procjs (GitHub: [vzaccaria / procjs](https://github.com/vzaccaria/procjs), License: _MIT_, npm: [procjs](https://npmjs.org/package/procjs)) by Vittorio Zaccaria is a set of command-line utilities for getting JSON representations from the output of `ps`.  It also comes with a REST server that provides a JSON API for the same data.

The project is built with LiveScript, and can be invoked with `jsps` along with several arguments.

