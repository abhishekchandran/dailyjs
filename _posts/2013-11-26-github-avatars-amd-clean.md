---
layout: post
title: "GitHub Avatar Chrome Extension, AMDClean"
author: Alex Young
categories:
- jquery
- chrome
- amd
- build
---

###GitHub Avatar Chrome Extension

![GitHub Avatar Chrome Extension](/images/posts/avatarsforgithub.png)

Writing Firefox add-ons or Chrome extensions can be off-putting for those of us who are good at JavaScript but not so great at browser plugin APIs.  Anas Nakawa sent in [chrome-github-avatars](https://chrome.google.com/webstore/detail/avatars-for-github/pgjmdbklnfklcjfbonjfkdhaonlfogbb) (GitHub: [anasnakawa / chrome-github-avatars](https://github.com/anasnakawa/chrome-github-avatars), License: _MIT_) which is a Chrome extension for displaying GitHub avatars on the news feed page.

It might seem like a modest extension, but the reason I liked it was he used a [Yeoman generator](https://github.com/yeoman/generator-chrome-extension).  Anas' project includes all the stuff I'm familiar with, like Bower and jQuery, but also things that I'm not too familiar with, like Chrome's `manifest.json`.  It seems cool that you can use tools popular in the JavaScript community to create browser plugins.

###AMDClean

[AMDClean](http://gregfranko.com/amdclean/) (GitHub: [gfranko / amdclean](https://github.com/gfranko/amdclean), License: _MIT_) by Greg Franko is a build tool for converting AMD code into standard JavaScript that works with RequireJS's optimiser.

> By incorporating amdclean.js into the build process, there is no need for Require or Almond.

> Since AMDclean rewrites your source code into standard JavaScript, it is a great fit for JavaScript library authors who want a tiny download in one file after using the RequireJS Optimizer.

> So, you get great code cleanliness with AMD, reduced file sizes, improved code readability, and easy integration with other developers who may not use AMD.


Greg notes that it also supports Grunt, so it should be easy to drop into your existing projects.
