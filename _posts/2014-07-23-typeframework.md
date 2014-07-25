---
layout: post
title: "TypeFramework: A TypeScript Web Framework"
author: "Alex Young"
categories:
- typescript
- languages
- microsoft
---

<div class="intro">
  <p>This week on DailyJS every post is about TypeScript!  This post is about TypeFramework, a possibly Rails inspired web framwork aimed at TypeScript developers.</p>
</div>

One of the aims of TypeScript is to help you write large applications.  In Node, the popular idiom is "small modules" -- programs are composed from small packages with APIs based on patterns found in Node's core modules.  That means EventEmitter, streams, callbacks with the error-first signature, and modules that return a single function.

This can work well, but people still seem to struggle to maintain larger web applications.  Surely a TypeScript MVC framework offers insights on how to structure larger projects?

[TypeFramework](http://typeframework.com/) (GitHub: [zekelevu / typeframework](https://github.com/zekelevu/typeframework), License: _MIT_, npm: [typeframework](https://www.npmjs.org/package/typeframework)) by Zeke Kievel is built on Express.  It has controllers, models, views, routing, and configuration.  The models are based on the [Waterline ORM](https://www.npmjs.org/package/waterline), and they look like this:

{% highlight javascript %}
class User extends TF.Model {
  name: string;
  email: string;
  age?: number;
}

app.addModel(User);
{% endhighlight %}

The chainable API is quite nice:

{% highlight javascript %}
User.find()
  .where({ name: 'John' })
  .skip(10)
  .limit(5)
  .done((err, users: User[]) => { /* callback */ });
{% endhighlight %}

Everything looks very much like a lightweight Rails.  It will probably help C# developers who want to write things that run on Node, or Rails developers who are transitioning to Node.

What I'd really like to see is a more MVVM-style framework with interfaces for code contracts, services, and ReactiveUI-style APIs.  I'd prefer skinny models so I can avoid putting business logic in them and use my own persistance layer.  I think TypeScript is perfectly suited to this, but I haven't yet found such a framework.

