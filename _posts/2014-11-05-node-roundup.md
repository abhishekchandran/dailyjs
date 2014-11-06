---
layout: post
title: "Node Roundup: npm and Front-end Packaging, npm Package Store"
author: "Alex Young"
image: "/images/posts/npmpackagestore.png"
categories:
- video
- node
- modules
- libraries
- frontend
- npm
---

###npm and Front-end Packaging

There's a post on the npm blog about [npm and front-end packaging](http://blog.npmjs.org/post/101775448305/npm-and-front-end-packaging).  It directly addresses something that lots of people are confused about: is it a good idea to use npm for front-end development, even if the project doesn't use CommonJS modules?

It's useful to see the npm team's thoughts on this, because it seems like some front-end developers use npm out of convenience, and others use it because their module works well in Node and browsers.  Writing code for browsers has different requirements to Node, but the major ones are highlighted in this post and then potential solutions are discussed.

One future feature that will help front-end developers is [ecosystems](http://blog.npmjs.org/post/94662089625/the-future-of-the-npm-website-lets-map-this-road#ecosystems), which is a way to create a subset of packages for a common base.  So in theory you could place React, jQuery, Gulp, and Grunt packages into separate sub-repositories.

Another recommendation suggested in the article is using additional metadata in the `package.json` file.  I've seen lots of packages do this so it seems increasingly popular at this point.

My preferred approach to front-end development is npm with npm scripts and Browserify, so it's encouraging to see that mentioned in the post:

> We also think browserify is amazing and under-utilized, and an end-to-end solution that worked with it automatically at install time is a really, really interesting idea (check out browserify’s sweet handbook for really great docs on how to use it effectively).

Building dependencies from `./node_modules` is a pain because every module seems to have a different entry point filename, so it would be really nice if more front-end developers used the `main` property in `package.json`.

If you're looking for an example of an npm-based React project, then I recently received this tutorial from yiminghe : [npm-based front-end development using browserify and browser loader library](https://github.com/yiminghe/learning-react/blob/master/tutorial/env/modulex-browserify-npm.md).

###npm Package Store

![npm Package Store](/images/posts/npmpackagestore.png)

Travis Horn sent in [npm Package Store](http://travishorn.com/npm-package-store/) (GitHub: [travishorn/npm-package-store](https://github.com/travishorn/npm-package-store), License: _MIT_, npm: [npm-package-store](https://www.npmjs.org/package/npm-package-store)).  This is a web application that shows updates for your globally installed npm packages.

It's an Express app that queries npm for JSON using `npm ls -g --json`, then fetches the latest info with `request` from <http://registry.npmjs.org>.
