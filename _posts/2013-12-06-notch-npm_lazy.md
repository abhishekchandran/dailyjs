---
layout: post
title: "Notch and WebGL, npm_lazy"
author: "Alex Young"
categories: 
- webgl
- npm
- games
- node
---

###Notch, WebGL, Dart

Brandon Jones wrote a summary of Notch's WebGL and-Dart related activity: [Notch, WebGL, Dart, and ramping up quickly](http://blog.tojicode.com/2013/12/notch-webgl-dart-and-ramping-up-quickly.html):

> I can't tell you how many time I see hobby developers saying "I'm building a game!" and what they actually have to show for it is a really complicated system for loading meshes and shaders. It's all well and good to think about long term goals and engine structure and such, but if you're going to build a game then please build a freaking game! Don't build an engine that you will someday build a game on top of, because you will never get past step one.

Dart seems to appeal to Notch, maybe because of his Java background.  It's cool seeing his work come together on Twitter, from the initial ideas to working code with screenshots.

###npm_lazy

Sometimes npm goes down (which is why you should [donate to npm](https://scalenpm.org/)).  But there's a solution: mirror it!  If you're too lazy to mirror the whole thing, how about just caching the modules you need to deploy your projects?  That's where [npm_lazy](http://mixu.net/npm_lazy/) by Mikito Takada comes in.

This is a local cache for npm.  It has a configuration file that allows you to tailor it to your needs -- you can set the cache lifespan, HTTP timeout, and so on.  Once you've set that up, you can run it as a server.  Then you just use `npm --registry` to set the server as your npm registry.

It has some caching logic -- anything that isn't local will be fetched, and metadata is updated when a module is requested the first time after a restart.
