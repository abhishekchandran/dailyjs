---
layout: post
title: "Book Review: The Meteor Book"
author: "Alex Young"
categories: 
- meteor
- reviews
- books
---

<div class="image">
  <img src="/images/posts/discovermeteor.png" alt=""/>
  <small>Discover Meteor, by Sacha Greif and Tom Coleman</small>
</div>

Sacha Greif sent me a copy of [The Meteor Book](http://www.themeteorbook.com/), a new book all about Meteor that he's writing with Tom Coleman.  He was also kind enough to offer a 20% discount to DailyJS readers, which you can redeem at [discovermeteor.com/dailyjs](http://www.discovermeteor.com/dailyjs) (in theory, bookmark it and try later).

The book itself is currently being distributed as a web application that allows the authors to collect early feedback.  Each chapter is displayed as a page, with chapter navigation along the left-hand-side of the page and Disqus comments.  There will also be downloadable formats like PDF, ePub, and Kindle.

The authors teach Meteor by structuring the book around building a web application called _Microscope_, based on the open source Meteor app [Telescope](http://telesc.pe/).  Each chapter is presented as a long form tutorial: a list of chapter goals is given, and then you're walked through adding a particular feature to the app.  Each code listing is visible on the web through a specific instance of the app, and every sample has a Git tag so it's easy to look up the full source at any point.  I really liked this aspect of the design of the book, because it makes it easier for readers to recover from mistakes when following along with the tutorial themselves (something many DailyJS readers contact me about).

<div class="image">
  <img src="/images/posts/meteor-book-commit.png" alt=""/>
  <small>Accessing a specific code sample is easy in <em>The Meteor Book</em></small>
</div>

There are also "sidebar chapters", which are used to dive into technical topics in more detail.  For example, the _Deploying_ chapter is a sidebar, and explains Meteor deployment issues in general rather than anything specific to the Microscope app.

Although I work with Node, Express, Backbone.js (and increasingly AngularJS), I'm not exactly an expert on Meteor.  The book is pitched at intermediate developers, so you'll fly through it if you're a JavaScript developer looking to learn about Meteor.

Something that appealed to me specifically was how the authors picked out points where Meteor is similar to other projects --  there's a section called _Comparing Deps_ which compares Meteor's data-binding system to AngularJS:

> We've seen that Meteor's model uses blocks of code, called computations, that are tracked by special 'reactive' functions that invalidate the computations when appropriate. Computations can do what they like when they are invalidated, but normally simply re-run. In this way, a fine level of control over reactivity is achieved.

They also explain the practical implications of some of Meteor's design.  For example, how hot code reloading relates to deployment and sessions, and how data can be limited to specific users for security reasons:

> So we can see in this example how a local collection is a secure subset of the real database. The logged-in user only sees enough of the real dataset to get the job done (in this case, signing in). This is a useful pattern to learn from as you'll see later on.

If you've heard about [Meteor](http://meteor.com/), then this book serves as a solid introduction.  I like the fact a chapter can be digested in a single sitting, and it's presented with some excellent diagrams and cleverly managed code listings.  It's not always easy to get started with a new web framework, given the sheer amount of disparate technologies involved, but this book makes learning Meteor fun and accessible.

