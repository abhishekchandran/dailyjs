---
layout: post
title: "NoFlo, Peppy"
author: "Alex Young"
categories: 
- node
---

###NoFlo

![NoFlo](/images/posts/noflo.png)

[NoFlo](http://noflojs.org/) (GitHub: [noflo](https://github.com/noflo)) is a project to bring a visual-based approach to programming.  It currently focuses on Node, but the authors want to branch out to other platforms if you [give them enough money](http://www.kickstarter.com/projects/noflo/noflo-development-environment).

The project and the site seem interesting enough, but the Kickstarter video comes off a little bit too enthusiastic.  Here is a spoonfull of delicious hyperbole for you to digest: "Nothing new has really been invented in programming in the last 50 years", "code starts as whiteboards", "flow-based programming can eliminate spaghetti code".

Whether or not something is truly new is irrelevant: monads have been around _less_ than 50 years, but even so we're still exploring their uses after a good 20 something years (random citation: [Extensibe Effects: An Alternative to Monad Transformers](http://www.cs.indiana.edu/~sabry/papers/exteff.pdf)).  Just because strongly typed object oriented programming is the dominant paradigm doesn't stop thousands of papers a year being published about programming and related fields.  Even if you spend all day writing JavaScript, Java, C#, or whatever, the field is still forging ahead: these languages themselves are evolving.

The assumption that we use whiteboards perplexes me.  I don't think I've used a whiteboard once in my career, and I've been programming commercially for 12 years now.  How can making tangled masses of diagrams be a solution to spaghetti code?  Won't we just end up with spaghetti diagrams?

> NoFlo has been written in CoffeeScript for simplicity.

Oh, OK... Before I give up and post that Grandpa Simpson hat gif, I'll say this: I'm not sold on the idea, but that doesn't mean I won't try it.  Let's set aside the hilariously hyperbolic marketing video and see what it can do.

###Peppy

Peppy (GitHub: [jdonaghue / Peppy](https://github.com/jdonaghue/Peppy), License: _FreeBSD_) by James Donaghue is a CSS selector engine.  He originally wrote it over four years ago, and it was well known at the time for being fast.  He's [recently rewritten it](http://spectaclelabs.io/blog/2013/08/05/peppy-version-2-0-0-beta/) with a different focus:

> Peppy no longer uses large regular expressions for parsing selector strings. It now uses a selector parser that I wrote called LLSelectorParser. This is a top down parser that returns an abstract syntax tree. Peppy internally now works off of this tree.

Back when I regularly wrote the [Let's Make a Framework](http://dailyjs.com/tags#lmaf) posts I was fascinated by how CSS frameworks work.  Things have changed since then, but parsing selectors is still an interesting topic.  Check out [LLSelectorParser](https://github.com/jdonaghue/LLSelectorParser) if you want to see how James implemented his.
