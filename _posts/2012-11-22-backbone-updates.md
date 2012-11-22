---
layout: post
title: "The State of Backbone.js"
author: Alex Young
categories: 
- backbone.js
- mvc
---

![Backbone.js](/images/posts/backbone-banner.png)

Looking at [backbonejs.org](http://backbonejs.org/) you'd be forgiven for thinking the project has stagnated somewhat.  It's currently at version 0.9.2, released back in March, 2012.  So what's going on?  It turns out _a huge amount of work_!  The developers have committed a slew of changes since then.  The latest version and commit history is readily available in the [master Backbone.js branch on GitHub](https://github.com/documentcloud/backbone/).  Since March there has been consistent activity on the master branch, including community contributions. The core [developers are working hard on releasing 1.0](https://github.com/documentcloud/backbone/issues/1594).

If you've been sticking with the version from the Backbone.js website (0.9.2), you're probably wondering what's changed between that version and the current code in the master branch.  Here's a summary of the new features and tweaks:

* Backbone can run without `$` being defined
* `Backbone.View` how has a `dispose` method for preventing memory leaks: [#1461](https://github.com/documentcloud/backbone/pull/1461)
* In `Backbone.View` objects, `id` and `className` can be functions: [#1520](https://github.com/documentcloud/backbone/pull/1520)
* Collections can be unsorted: [#1342](https://github.com/documentcloud/backbone/pull/1342)
* `Backbone.Collection.add` has an optional `merge` flag for merging models with identical IDs: [#1220](https://github.com/documentcloud/backbone/pull/1220)
* [Collections can now be cloned](https://github.com/documentcloud/backbone/pull/1239)
* Success callbacks now receive the original `options` object: [#1355](https://github.com/documentcloud/backbone/pull/1355)
* ['off' is chainable when there are no events](https://github.com/documentcloud/backbone/commit/af30bcf3ca60c4234df099762344ff4b479260e7)

In addition to these changes, there are a lot of fixes, refactored internals, and documentation improvements.

If you're interested in testing this against your Backbone-powered apps, then download the [Backbone.js edge version](https://raw.github.com/documentcloud/backbone/master/backbone.js) to try it out.  I'm not sure when the next major version will be released, but I'll be watching both the [Backbone.js Google Group](https://groups.google.com/group/backbonejs/topics) and GitHub repository for news.
