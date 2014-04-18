---
layout: post
title: "Live Reloading Chrome Apps, Chrome Extensions with React, sendMessage Tutorial"
author: "Alex Young"
categories:
- chrome
- extensions
- browsers
---

###Live Reloading Chrome Apps

> The Chrome Store itself is a pile of rubbish apps with very few exceptions.

Working with Chrome extensions and apps is pleasant enough in some ways -- the JavaScript APIs are generally intuitive, and you can make native-feeling UIs without too much effort.  However, the development experience feels a little bit dated and painful in places.

Konstantin Raev sent in [Live Reloading Chrome Apps](https://medium.com/p/2a58d804c496), an article about using Gulp with Chrome apps.  It shows how live reloading isn't as easy as it could be, and how to fix it.  There's also a full example on GitHub: [bestander / clock-chrome-app-livereload-example](https://github.com/bestander/clock-chrome-app-livereload-example).

###Creating Chrome Extensions with React

Brandon Tilley sent in [Creating Chrome Extensions with React](http://brandontilley.com/2014/02/24/creating-chrome-extensions-with-react.html):

> If you're into client-side web development to any extent, you've probably heard of Facebook's React library.  I was working on a Chrome extension, and decided to see how well React fit in to the development I was doing.

He also uses Browserify as well, which I'm interested in because I tried using RequireJS for sharing code between Chrome extensions and Firefox add-ons, and I struggled to get it to work in Firefox.  My Firefox add-ons are using the [Jetpack SDK](https://wiki.mozilla.org/Labs/Jetpack) rather than the old XUL way.

###Passing data around in Chrome extensions

[Passing data around in Chrome extensions](http://blog.papersapp.com/chrome-development-parent-and-child-windows/) by Erica Salvaneschi is an introduction to using `chrome.runtime.sendMessage` and `addListener`:

> We wanted to get data from the current web page and then use it to populate a form that appears in a new window.
> It was easy to create a context menu item that triggered an event, but sending data based on the current page to the new window wasn't obvious.

You might find this useful if you're just getting into Chrome extensions and want more concrete examples than what Google provides.
