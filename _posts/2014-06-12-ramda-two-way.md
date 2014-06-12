---
layout: post
title: "Why Ramda?, Two-Way Data Binding Review"
author: "Alex Young"
categories:
- ui
- data-binding
- functional
- mvvm
---

###Why Ramda?

Scott Sauyet sent in [Why Ramda?](http://fr.umio.us/why-ramda/), a post that attempts to explain the [Ramda](https://github.com/CrossEye/ramda) library:


> To those not used to functional programming, Ramda seems to serve no purpose whatsoever. Most of its major capabilities are already covered by libraries like Underscore and LoDash.
>
> These folks are right. If you want to keep coding with the same imperative and object-oriented styles you've been using, Ramda does not have much to offer you.
>
> However, it does offer a different style of coding, a style that's taken for granted in purely functional programming languages: Ramda makes it simple for you to build complex logic through functional composition. Note that any library with a compose function will allow you do functional composition; the real point here is: "makes it simple".

The article builds on the functional composition idea and leads up to the kind of data-focused programming that Ramda makes possible.

###Two-Way Data Binding Review

[Two-Way Data Binding](http://n12v.com/2-way-data-binding/) by Nikita Vasilyev is a review of two-way data binding in Backbone, React, Angular, Meteor and plain JavaScript.

It highlights an issue that some libraries might have if they change fields at the wrong time:

> The problem is that data flows from an input field to a model,  and then back to the same input field, overriding the current value even if it's exactly the same.
>
> React.js doesn't have Backbone's problem with moving the cursor position. Its virtual DOM, a layer between the actual DOM and React's state, prevents React from unnecessary DOM changes.

There's also an informative comment by Leo Horie about the effort required to learn each framework:

> Something that strikes me about the framework versions is the amount of framework-specific knowledge required to get these examples working. It's one thing to say "here's a version in framework X", and it's quite another to actually write the code (from the standpoint of someone who's still considering framework options and who is not familiar with the lingo and caveats for any of them.)

