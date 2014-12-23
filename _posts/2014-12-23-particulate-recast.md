---
layout: post
title: "Particle Paintings, AMD to CommonJS with Recast"
author: Alex Young
image: "/images/posts/particulate-small.png"
categories:
- animation
- graphics
- modules
- amd
---

###Particture

![Particture](/images/posts/particulate-small.png)

Tadeu Zagallo sent in a Canvas experiment that uses typed arrays, optimised sorting algorithms, and inlining and bitwise operators to boost performance.  The [Particture demo](http://tadeuzagallo.com/particture/) allows you to use your webcam for the source image, and draws images with a cool trail effect.

The repository at [tadeuzagallo/particture](https://github.com/tadeuzagallo/particture) has the source, and it uses [dat.gui](http://workshop.chromeexperiments.com/examples/gui/#1--Basic-Usage) for the controls.

###Recast

Many readers seem to be searching for solutions to the module refactor problem, where older projects are refactored to use modern module systems.  Dustan Kasten wanted to convert projects that use AMD to CommonJS, and he's used [Recast](https://github.com/benjamn/recast) to do this, through the [recast-to-cjs](https://github.com/Skookum/recast-to-cjs) project that is published by his company (Skookum Digital Works).

Dustan has written an article that shows how to convert a project to CommonJS: [Converting a project from AMD to CJS with Recast](http://skookum.com/blog/converting-a-project-from-amd-to-cjs-with-recast/).  The AST is traversed to find AMD definitions, and then converted into equivalent CommonJS dependencies.

It's possible that Node developers may end up doing something like this if ES6 modules become the norm, although I suspect ES6's `export` and `import` statements will need manual intervention to take advantage of `import obj from lib`.
