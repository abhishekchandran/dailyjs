---
layout: post
title: "Z3d, is-progressive, Japanese Translations, textlint"
author: Alex Young
image: "/images/posts/z3d.png"
categories:
- webgl
- graphics
- libraries
- japanese
- translations
- jpeg
---

###Z3d

![Z3d](/images/posts/z3d.png)

[Z3d](http://nathanepstein.github.io/jekyll/update/2015/01/11/z3d.html) (GitHub: [NathanEpstein/Z3d](https://github.com/NathanEpstein/Z3d), License: _MIT_, Bower: _z3d_) by Nathan Epstein is a library that generates 3D plots.  It gives you a Three.js scene, so you can further manipulate the graph with the Three.js API.

One of the useful things about Z3d is it has sensible built-in defaults, so you can throw data at it and get something cool out.  The basic example is just `plot3d(x, y, z)`, where the arguments are arrays of numbers to plot in 3D space.

The `plot3d` function also accepts a configuration argument, which allows things like colours and labels to be defined.

###is-progressive

If you're running through a checklist of website performance improvements and see image optimisation, then you might want some automated tools to do the job for you.  Sindre Sorhus suggests using progressive JPEG images, and sent in a tool that can check if a JPEG is progressive or not.

It's called is-progressive (GitHub: [is-progressive](https://github.com/sindresorhus/is-progressive), License: _MIT_, npm: [is-progressive](https://www.npmjs.com/package/is-progressive)), and can be used as a Node module or on the command-line.  The command-line use is either `is-progressive filename` or you can redirect data into it.

The Node module supports streams and has a synchronous API.  That means you can do `isProgressive.fileSync`, or pipe HTTP requests through it with `res.pipe(isProgressive.stream(callback))`.

###DailyJS Japanese Translation and textlint

Hideharu Sakai wrote in to say he's been translating DailyJS into Japanese, here: [panda.node.ws/?cat=19](http://panda.node.ws/?cat=19).

He also mentioned a nice project for linting text: [textlint](https://github.com/azu/textlint) (License: _MIT_, npm: [textlint](https://www.npmjs.com/package/textlint)).  You can use it to check plain text and Markdown files for various rules which are customisable.  The example ensures to-do lists are written a certain way.

You can use textlint as a command-line tool or a Node module, so you could put it into a build script to validate your project's documentation.

Many thanks to Hideharu!
