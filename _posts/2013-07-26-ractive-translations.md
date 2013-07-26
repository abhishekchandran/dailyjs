---
layout: post
title: "Ractive.js, Japanese DailyJS Translations"
AUthor: Alex Young
categories:
- dom
- translations
- community
- libraries
- mvc
---

###Ractive

Ryan McDonough sent in [Ractive.js](http://www.ractivejs.org/) (GitHub: [Rich-Harris/Ractive](https://github.com/rich-harris/Ractive), License: _MIT_, Bower: _ractive_), a new alternative to libraries like AngularJS, created by developers at [The Guardian](http://guardian.co.uk).  Are we still calling these libraries MVC, MV\*, or something else?

> Ractive.js is different. It solves some of the biggest headaches in web development - data binding, efficient DOM updates, event handling - and does so with almost no learning curve.

There's a nice and short example in the documentation.  Given the following HTML fragment:

{% highlight html %}
<p>Hello {{user}}! You have
    <strong>{{messages.unread}} new messages</strong>.
</p>
{% endhighlight %}

Then the `Ractive` constructor can be used to populate data:

{% highlight javascript %}
var ractive = new Ractive({
  el: result,
  template: html,
  data: {
    user: 'Dave',
    messages: { total: 11, unread: 4 }
  }
});

ractive.set('messages.unread', 5);
{% endhighlight %}

However...:

> Ractive.js constructs a parallel DOM representation which is aware of its dependencies on the values of `user` and `messages.unread`. When those values change, it knows exactly which parts of the real DOM need to be updated.

This could be the data-binding library with an idiomatic JavaScript API that we've been looking for.  By focusing on the "data model" problem the project seems immediately easier to understand than some larger libraries, and the early adoption of Bower and Grunt means it should be straightforward to slot into your projects.

###Japanese DailyJS Translations

Hideharu Sakai sent in his translation of my recent "Getting started with Nodebots" article: [Nodebot を始めよう（著者：アレックス・ヤング）](http://panda.node.ws/?p=150).  He said there's a lot of interest in Node and DailyJS from the Japanese developer community, so thanks for that!
