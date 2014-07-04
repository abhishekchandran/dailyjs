---
layout: post
title: "Moving Atom To React"
author: "Alex Young"
categories:
- reactive
- atom
---

There's a post on the Atom blog about some performance improvements that you can optionally enable: [Moving Atom To React](http://blog.atom.io/2014/07/02/moving-atom-to-react.html).  It discusses how Facebook's [React](http://facebook.github.io/react/index.html) library was used to improve the performance of the text editing component:

> Right out of the box, React's virtual DOM got us a long way toward our goal of treating the DOM with kid gloves. Though we worked with raw DOM nodes in a few places for performance and measurement reasons, it offered a declarative abstraction that relieved us of the tedious state management typically associated with DOM updates. In addition, React's well-defined reconciliation strategy and lifecycle hooks made it easy to reason about the sequencing of the manual DOM interactions we did have to perform.
>
> With the React editor, these kinds of changes can now be performed with the new decorations API. Decorations allow metadata to be associated with markers, instructing the editor to render classes on lines and line numbers, or draw highlight regions. Using decorations is faster and more convenient than manual DOM interactions, and we plan on introducing more APIs for common DOM interactions going forward.

This highlights several things that React is good at:

* It's relatively small and self-contained, so you can drop it into an existing project
* The virtual DOM is fast
* It helps to improve managing state

I've been using Knockout for a while now, and I'm even thinking about using [RxJS](https://github.com/Reactive-Extensions/RxJS) for some projects.  However, after reading this I think a combination of Knockout and React might work well for the messier parts in my Knockout view models that deal with the DOM.
