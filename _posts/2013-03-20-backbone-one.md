---
layout: post
title: "Backbone 1.0"
author: "Alex Young"
categories: 
- backbone.js
- mvc
- libraries
- frameworks
---

Today Jeremy Ashkenas announced that [Backbone.js 1.0 has been released](http://ashkenas.com/backbonejs-1.0/), after a [whole year](https://github.com/documentcloud/backbone/commit/5ce976bf6a6c795e295190bcc48c39e52f9afe6f) on the 0.9 branch.  This release adds support for HTTP `PATCH` requests, where partial updates are sent to the server.  It also provides some sugar for data filtering methods like [where](http://backbonejs.org/#Collection-where) and [omit](http://underscorejs.org/#omit) (from Underscore.js).  Jeremy also notes that the [annotated source](http://backbonejs.org/docs/backbone.html) has been improved.

Although Backbone 1.0 includes internal refactoring, the API should be largely backwards compatible -- at least from the tests I've been doing with my own Backbone projects against the releases on GitHub.  There may be quirks that I've missed, however, so as always make sure you've carefully tested your code before releasing it.

Jeremy also intimates that he's looking for new major features, but doesn't specifically promise anything in the roadmap:

> In an ecosystem where overarching, decides-everything-for-you frameworks are commonplace, and many libraries require your site to be restructured to suit their look, feel, and default behavior - Backbone should continue to be a tool that gives you the freedom to design the full experience of your web application.

I feel like Backbone has earned its 1.0 status, and I'll be watching Backbone's GitHub repository very carefully over the next few months.
