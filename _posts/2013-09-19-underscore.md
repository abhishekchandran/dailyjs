---
layout: post
title: "Underscore, Array.prototype, and You"
author: "The Angry JavaScript Nerd"
categories:
- node
- underscore
---

What's the most dependent module on npm?  [Underscore.js](http://underscorejs.org/)!  Why do people use it?  Presumably because they can't be bothered to learn how JavaScript works.

There are things I like about Underscore.  No global meddling, sane internals -- it's a solid piece of work.  But I occasionally find myself working with programmers who are probably better than me yet have weaker JavaScript skills, and they reach for Underscore like a drunk reaching for cheap gin.

At this point I stay their hand and point to [Annotated ECMAScript](http://es5.github.io/#x15.4.4), highlighting the superpowers baked into `Array.prototype`.  Granted it lacks some of the things Underscore has, but it often does what you want.

Mozilla's documentation is also good because it shows you how to duplicate the functionality with lengthy code samples, which is educational if you take the time to read it.

If this is new to you or you're a little uncomfortable with `Array.prototype`, start with [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) then [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) and [some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some).  They're the methods that crop up in my own code a lot.

Another related JavaScript quirk is array type checking.  Because JavaScript says `typeof [1, 2, 3]` is `'object'` you might want to pack your bags and give up altogether.  I don't blame you.  But hiding in that ES5 documentation is a beastie called `Array.isArray`.  You'll find it in `util` in Node, which is puzzling -- you'll be OK using `Array.isArray([1, 2, 3])`.

I don't think it's a bad thing to depend on Underscore, but it makes me feel like people don't learn Node or indeed JavaScript well enough before flinging their modules up on npm.
