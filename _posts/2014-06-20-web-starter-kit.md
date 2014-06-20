---
layout: post
title: "Google's Web Starter Kit"
author: "Alex Young"
categories:
- node
- gulp
- sass
- boilerplate
---

<div class="image">
  <img src="/images/posts/webstarterkit.png"/>
  <small>Web Starter Kit</small>
</div>

[Web Starter Kit](https://developers.google.com/web/starter-kit/) (GitHub: [google / web-starter-kit](https://github.com/google/web-starter-kit), License: _Apache 2.0_) from Google is a boilerplate for developing responsive websites.  It supports multiple devices, has a [gulp.js](http://gulpjs.com/) build script, and has support for synchronising pages across devices during testing.

If you're a Node developer, then you might like the gulp.js-based environment.  Typing `gulp` will build and optimise the current project, and `gulp serve` will run a server.  There's also `gulp pagespeed` that uses Google's [PageSpeed insights](https://developers.google.com/speed/pagespeed/insights/).

The sync feature for testing is powered by [BrowserSync](http://browsersync.io/).  BrowserSync is a Socket.IO-based Node application that automatically sends changes to pages as you edit files.  It also has a [gulp.js module](https://github.com/shakyShane/gulp-browser-sync) that you can use with your own projects.

If you're wondering why a Node/Ruby project has come out of Google, then [take a look at the Web Starter Kit contributors](https://github.com/google/web-starter-kit/graphs/contributors): it seems like it's another project by Addy Osmani and Sindre Sorhus, just like [Yeoman](http://yeoman.io/).

Although this is a boilerplate project, the style guide makes it look more like something like Bootstrap.  If you find Bootstrap too heavy for your projects and would prefer something lighter with workflow tools, then give Web Starter Kit a try.
