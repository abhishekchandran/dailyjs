---
layout: post
title: "Should You Share Client-Side Projects on npm?"
author: Alex Young
categories:
- npm
- node
- browser
---

Should you share your client-side projects with npm?  Or, as a client-side developer, should you be using npm and a `package.json` to organise your project's dependencies?

People are already using npm for distributing client-side code for many types of projects:

1. Generic JavaScript that is sometimes used on the server but often used in the client (Underscore.js, Backbone.js)
2. Client-side libraries that are so popular they've ended up npm out of convenience (jQuery)
3. Client-side plugins for Backbone.js, AngularJS, jQuery (check out [peer dependencies](http://blog.nodejs.org/2013/02/07/peer-dependencies/) if you want to do this in a clean way)

If you decide to share a module using npm, you don't necessarily need to wrap it in Node's module system, but I would argue that you should, and you should also supply tests that can be run with Node.  In an ideal world all modules on npm would include tests, and I believe this extends to client-side projects.

A recent client-side workflow pattern that has emerged, perhaps most notably from Substack, is to use Node in the browser, using something like [Browserify](http://browserify.org/).  This means you can use `require`, so you can organise client-side code with Node's module system.  What I think is amazing about this is you can use Node's core modules, so if you're used to using `EventEmitter` and streams then you can bring these patterns over to the browser.

However, as Substack notes in [this post on reddit](http://www.reddit.com/r/node/comments/1p3evg/require_in_node/cd1m6mm), `require` is incompatible with RequireJS.  It might seem surprising if you're a Node developer, but the naming of `require` and RequireJS causes serious confusion to client-side developers who are just discovering module systems.

###The Question

So, the question is, should you use npm for sharing client-side projects, or something like Bower?  Do you prefer using Browserify or similar pre-processors, or is using AMD good enough?

