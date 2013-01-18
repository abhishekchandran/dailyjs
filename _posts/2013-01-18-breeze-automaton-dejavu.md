---
layout: post
title: "BreezeJS, Automaton, dejavu"
author: Alex Young
categories:
- libraries
- oo
- databases
---

###BreezeJS

[BreezeJS](http://www.breezejs.com/) (GitHub: [IdeaBlade / Breeze](https://github.com/IdeaBlade/Breeze), License: _MIT_) by IdeaBlade is a data management library -- it can be used to build queries, track changes, bind to MVC libraries like Knockout, and cache data in the client.

The query interface is like LINQ, but it doesn't specifically require .NET:

{% highlight javascript %}
var query = breeze.EntityQuery
           .from('Customers')
           .where('CompanyName', 'startsWith', 'A')
           .orderBy('CompanyName');
{% endhighlight %}

BreezeJS supports asynchronous queries through promises:

{% highlight javascript %}
var promise = manager.executeQuery(query)
              .then(querySucceeded)
              .fail(queryFailed);
{% endhighlight %}

Although it's open source, the company behind it has [commercial support packages](http://www.breezejs.com/support).  There are also [BreezeJS tutorials](http://learn.breezejs.com/) for getting started.  It can work with various SQL and NoSQL databases -- the nature of this and the relationship to the .NET Entity Framework is explained in the [BreezeJS FAQ](http://www.breezejs.com/documentation/faq) (before complaining about .NET in the comments read the FAQ first).

###Automaton

<img src="/images/posts/automaton.png" style="background: transparent; border: none; float: right" alt="" />

[Automaton](http://indigounited.com/automaton/) (GitHub: [IndigoUnited / automaton](https://github.com/IndigoUnited/automaton), License: _MIT_, npm: [automaton](https://npmjs.org/package/automaton)) from Indigo United is a task automation tool, similar to Grunt but (from what I can gather) the way tasks are reused works differently.

It's designed to be used with Node and installed through npm, and it has an API for programatically running tasks.  The documentation is good, and it makes it clear what parts of the API use streams or other things you can easily hook into with Node.

###dejavu

![dejavu](/images/posts/dejavu.png)

[dejavu](http://indigounited.com/dejavu/) (GitHub: [IndigoUnited / dejavu](https://github.com/IndigoUnited/dejavu), License: _MIT_, npm: [dejavu](https://npmjs.org/package/dejavu)) also from Indigo United is a classical OO toolkit that can be used with browsers or Node.  It can work with AMD, and in that case the syntax reminds me of Backbone projects written using RequireJS.

It supports the usual features: classes, inheritance, mixins, private and protected members, and also adds some type checking tools like method signature checks and a custom `instanceOf`.  The authors have provided benchmarks, which is good, because I've seen too many libraries that say they're fast without any proof.

After writing [JS101](http://dailyjs.com/tags.html#js101), which has some coverage of working with prototypes and JavaScript objects in general, seeing "classical OO" libraries makes me extremely wary.  However, I've given dejavu a cursory look, and it includes Mocha tests, and takes a wide range of influences into account, so it might be worth adding to your microjs/component library bookmarks for the next time you really need some of the features this library provides.  I thought the name "dejavu" was a nod to the plethora of similar libraries out there, but I think it refers to the fact it looks more like OO in other languages.

