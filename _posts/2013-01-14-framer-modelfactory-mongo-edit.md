---
layout: post
title: "Framer, ModelFactory, Mongo Edit"
author: Alex Young
categories:
- testing
- backbone.js
- mongodb
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Framer

![Framer](/images/posts/framer.png)

[Framer](http://www.framerjs.com/) (GitHub: [koenbok / Framer](https://github.com/koenbok/Framer), License: _MIT_) by Koen Bok is a prototyping tool aimed at designers who can write basic JavaScript.  It uses hardware acceleration and a simple JavaScript API for working with a subset of view types that are reminiscent of the ones used in Apple's iOS frameworks.

The example on the site creates the iPhone container view, so you could adapt it to show something else if you wanted.  The author suggests using Framer in conjunction with [Cactus](https://github.com/koenbok/Cactus) and [Ratchet](http://maker.github.com/ratchet/) for creating rapid prototypes of iOS applications.

###Backbone.ModelFactory

[Backbone.ModelFactory](https://github.com/misteroneill/backbone-model-factory) (License: _MIT_) by Pat O'Neill generates model constructors that never produce multiple instances of a model with the same unique identifier.  This is intended to make sharing models between views easier.  This steps around Backbone's built-in behaviour, and was based on [Building the Next SoundCloud](http://backstage.soundcloud.com/2012/06/building-the-next-soundcloud/) -- an internal cache of model instances can be created based on their IDs:

> Almost all views are instantiated only with the id of its model, so it's quite possible that the data for that model hasn't been loaded yet.  To solve this, we use a construct we call the _instance store_. This store is an object which is implicitly accessed and modified each time a constructor for a model is called. When a model is constructed for the first time, it injects itself into the store, using its id as a unique key. If the same model constructor is called with the same id, then the original instance is returned.

###Mongo Edit

[Mongo Edit](https://github.com/tldrio/mongo-edit) (License: _MIT_, npm: [mongo-edit](https://npmjs.org/package/mongo-edit)) from tldr.io is a simple editor for data in MongoDB.  It's built with Express, and the ACE editor.

If you're looking for examples of Express applications, this one is built with route separation, and includes some simple Mocha tests.

