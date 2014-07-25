---
layout: post
title: "TypeScript Log, Supplemental"
author: "Alex Young"
categories:
- typescript
- languages
- microsoft
- libraries
---

<div class="intro">
  <p>This week on DailyJS every post is about TypeScript!  This article is a roundup of interesting TypeScript libraries.</p>
</div>

This is the end of TypeScript week on DailyJS.  I've been going through my email archives looking for TypeScript-related things that people have sent in.  Here is a selection!  As always, please share anything TypeScript (or JavaScript) related with me by going to [contact.dailyjs.com](http://contact.dailyjs.com/).

###VCL.JS

[VCL.JS](http://vcljs.com/) (GitHub: [vclteam / VCL.JS](https://github.com/vclteam/VCL.JS), License: _Apache 2.0_) is a component-based web framework.  The built-in components are based on Bootstrap, so the UI code should be quite easy to work with if you've used Bootstrap before.

It has deep Visual Studio integration, so Microsoft developers should be able to get started quickly.  It even supports data binding and AMD for client-side code.

###EndGate

I'm intrigued by [EndGate](http://endgate.net/), a game framework for HTML5 games written in TypeScript.  It has APIs for input, graphics, animations (tweening), and collision detection.

There's a tutorial that explains how to use [collisions and tweens](http://endgate.net/Tutorials/GettingStarted3).  It seems to focus on map-based 2D games, which usually work well in browsers anyway.

###asyncawait

One of the big things in C# 5.0 was the `async` modifier and `await` operator.  These keywords allow C# code to be asynchronous, without callbacks or delegate methods.

The [asyncawait](https://github.com/yortus/asyncawait) module for Node is inspired by this API.  You can `await` asynchronous methods, so you get to use non-blocking APIs with synchronous convenience:

{% highlight javascript %}
var foo = async (function() {
    var resultA = await (firstAsyncCall());
    var resultB = await (secondAsyncCallUsing(resultA));
    var resultC = await (thirdAsyncCallUsing(resultB));
    return doSomethingWith(resultC);
});
{% endhighlight %}

This module is based on two great projects: [node-fibers](https://github.com/laverdet/node-fibers) and [bluebird](https://github.com/petkaantonov/bluebird), but it's written with TypeScript:

> TypeScript: asyncawait is written in TypeScript (look in the src folder), and includes a type declaration file. TypeScript makes JavaScript development faster, less error-prone, more scaleable, and generally more pleasant.

