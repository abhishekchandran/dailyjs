---
layout: post
title: "Your First Meteor Application, CommonJS React Components, WebComponents"
author: Alex Young
image: "/images/posts/yourfirstmeteor.png"
categories:
- meteor
- books
- sponsored-content
- WebComponent
- react
---

###Your First Meteor Application

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a book that we think will appeal to DailyJS readers.</p>
</div>

![Your First Meteor Application](/images/posts/yourfirstmeteor.png)

David Turnbull sent me [Your First Meteor Application](http://meteortips.com), a highly focused, beginner-friendly introduction to Meteor.  One thing that's cool about this is book is David updates it regularly when Meteor changes.

You can [read the book online](http://meteortips.com/book/introduction/) or download the PDF for free.  There are [even screencasts](http://meteortips.com/screencasts/)!

###CommonJS React Components

What do you do if you want to create reusable isomorphic CommonJS React components?  You can install React with npm, but what's the ideal pattern for structuring these components?  How should the CSS be managed?

Aaron Kaka has been working on an experiment to use CommonJS modules as a way of sharing UI components.  The work is inspired by [a blog post by Simon Smith](http://simonsmith.io/writing-react-components-as-commonjs-modules/), and you can find it on GitHub here: [aaronkaka/commonjs-react-components](https://github.com/aaronkaka/commonjs-react-components).

This proof-of-concept uses events for all interactions, so knowledge of the internal library and its dependencies is not required.  You can use styling through `require` statements -- component specific styling is scoped to the component.

It uses [webpack](http://christianalfoni.github.io/javascript/2014/12/13/did-you-know-webpack-and-react-is-awesome.html) and live reload, so it should fit in with a modern Node-based toolchain.

Using CommonJS modules and events should appeal to Node programmers who want to make reusable client-side components.  If you're a little lost with React in Node, or CommonJS and React, then this repository will give you a head start.

###WebComponents

Interest in [WebComponents](http://webcomponents.org) is growing, but unless you're involved with them it can be hard to see the benefits.  Leon Revill has been working with them, and has written an article that outlines the basics of how to create WebComponents and why they're exciting.  From [What are WebComponents and why are they important?](http://www.revillweb.com/articles/why-web-components-are-important/):

> Once WebComponents are properly supported and established you should be able to write a WebComponent that can be used in all of your projects regardless of the other technologies used. Forget writing plugins for jQuery, directives for AngularJS and addons for Ember.js. Write once use many. This has a huge benefit and in my mind is one of the most significant benefits of WebComponents.

The article includes technical examples and addresses some concerns about the divergence between X-Tag, Polymer and Bosonic.


