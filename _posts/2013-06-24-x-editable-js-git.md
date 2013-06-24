---
layout: post
title: "JS-Git Update, X-editable"
author: "Alex Young"
categories: 
- bootstrap
- ui
- widgets
- git
---

###JS-Git

![JS-Git logo](/images/posts/jsgit.png)

Tim Caswell's JS-Git project has gone through the proof-of-concept stage, and he's now reached an impasse where he's looking for more funding.  There's a [JS-Git](https://github.com/creationix/js-git) repository that has specifications for the core parts of the project.  This includes interfaces for how backends can be written, including details on using HTML5 APIs or a real file system with Node.

The [Git Database](https://github.com/creationix/js-git/blob/master/specs/git-db.md) specification defines how objects and refs should be stored, based on ECMAScript syntax.  The beginnings of a reference implementation can be found in [fs-db.js](https://github.com/creationix/git-repo/blob/master/fs-db.js), which uses Node's `fs` module.

The new fundraising campaign, run on [BountySource](https://www.bountysource.com/#fundraisers/325-js-git), aims to raise $30,000 to enable Tim to work on the project full time to move the project closer to his main goals.  This includes cloning remote repositories to local storage over http, git, or ssh, making and committing local changes offline, and pushing changes back to remote repositories.  The target platforms are ChromeOS, Firefox OS, Windows RT WinJS, and HTML5 web apps.

It's an ambitious project, but Tim admits in the BountySource posting that he won't reach 100% completion.  The effort reminds me of a JavaScript-centric version of [libgit2](http://libgit2.github.com/), and has particular relevance for anyone interested in bringing native development tools to new web-based platforms like ChromeOS.

###X-editable

![X-editable](/images/posts/x-editable.png)

[X-editable](http://vitalets.github.io/x-editable/) (GitHub: [vitalets / x-editable](https://github.com/vitalets/x-editable), License: _MIT_, bower: _x-editable_) by Vitaliy Potapov is an in-place editing library that works with Bootstrap, jQuery UI, and jQuery.  It can display a popup for a simple text field, or richer input widgets like date selectors.

I like to use it with data attributes, so I have simple markup that drives the keys and values for various UI elements, and then a generic RESTful API that the data is persisted to.  I've been using it for Bootstrap CMS-style interfaces, with a Grunt/bower build environment, and it's been solid so far.  The author has included tests and [documentation](http://vitalets.github.io/x-editable/docs.html).
