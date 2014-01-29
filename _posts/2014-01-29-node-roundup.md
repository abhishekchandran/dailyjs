---
layout: post
title: "Node Roundup: Node 0.11.11, Nightwatch.js, Hackify"
author: Alex Young
categories:
- node
- modules
---

###Node 0.11.11

[Node 0.11.11](http://blog.nodejs.org/2014/01/28/node-v0-11-11-unstable/) was released today, and it's quite a big update so I think they're catching up after the holiday slowdown.  The main binary dependencies have been updated (v8, HTTP parser, openssl, uv).  There's a huge amount of fixes for the core modules, including crypto, http, tls, and util.

###Nightwatch.js

![Nightwatch.js](/images/posts/nightwatch-logo.png)

[Nightwatch.js](http://nightwatchjs.org/) (GitHub: [beatfactor / nightwatch](https://github.com/beatfactor/nightwatch), License: _MIT_, npm: [nightwatch](https://npmjs.org/package/nightwatch)) is a test framework that uses [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/).  Tests are written as modules, so the exported functions are run as test cases.  The first parameter is a `client` object, that has a chainable API for scripting access to webpages.

It includes JUnit XML support, so you can use it with a CI server like TeamCity.  Both CSS selectors and XPath can be used.

If you've never used Selenium before, then take a look at the [Nightwatch guide](http://nightwatchjs.org/guide).  It explains how it manages the Selenium server and browser instances.

###Hackify

[Hackify](http://www.hackify.org/) (GitHub: [hackify](https://github.com/hackify), License: _MIT_, npm: [hackify](https://npmjs.org/package/hackify)), by Michael Dausmann, is a collaborative code editor that features a permission system, and chat.  It feels like Google Drive for programming.

The server uses Express, Socket.IO, and Redis.  It's written like a fairly typical Express application, with route separation and ejs templates.
