---
layout: post
title: "React Inline, FluxThis"
author: Alex Young
categories:
- flux
- react
- css
---

###React Inline

If you're looking for a solution for managing CSS in React projects, then take a look at React Inline (GitHub: [martinandert/react-inline](https://github.com/martinandert/react-inline), License: _MIT_, npm: [react-inline](https://www.npmjs.com/package/react-inline)) by Martin Andert.  It transforms inline styles into CSS code and class names, so you get a CSS file and a list of class names.

There's [an example](https://github.com/martinandert/react-inline/tree/master/example/quick) that shows how the `StyleSheet.create` syntax can be turned into a more succinct `const styles` object with a [corresponding CSS file](https://github.com/martinandert/react-inline/blob/master/example/quick/Button.transformed.css).

The project has tests (that are written with ES6 with Babel), and [there's a demo site](http://react-inline-demo.herokuapp.com).

###FluxThis

Josh Horwitz sent in [FluxThis](https://fluxthis.io/#/) (GitHub: [addthis/fluxthis](https://github.com/addthis/fluxthis), License: _Apache 2_, npm: [fluxthis](https://www.npmjs.com/package/fluxthis)), a Flux framework by AddThis.  It's designed to make debugging easier, and comes with immutability and performance optimisations.

For more on immutability, see the [immutable stores](https://fluxthis.io/#/docs/immutable-stores) documentation.  There's also a [non-immutable store](https://fluxthis.io/#/docs/oo-stores) known as the `ObjectOrientedStore`.  Internally the project uses [immutable](https://www.npmjs.com/package/immutable), and Babel is also used so all of the internal FluxThis code is ES6.
