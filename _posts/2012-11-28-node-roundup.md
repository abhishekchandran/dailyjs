---
layout: post
title: "Node Roundup: 0.8.15, JSPath, Strider"
author: "Alex Young"
categories: 
- node
- modules
- apps
- express
- json
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.15

[Node 0.8.15 is out](http://blog.nodejs.org/2012/11/26/node-v0-8-15/), which [updates npm to 1.1.66](https://github.com/isaacs/npm/commits/v1.1.66), fixes a `net` and `tls` resource leak, and has some miscellaneous fixes for Windows and Unix systems.

###JSPath

[JSPath](https://github.com/dfilatov/jspath) (License: _MIT/GPL_, npm: [jspath](https://npmjs.org/package/jspath)) by Filatov Dmitry is a DSL for working with JSON.  The DSL can be used to select values, and looks a bit like CSS selectors:

{% highlight javascript %}
// var doc = { "books" : [ { "id" : 1, "title" : "Clean Code", "author" : { "name" : "Robert C. Martin" } ...

JSPath.apply('.books.author', doc);
// [{ name : 'Robert C. Martin' }, ...
{% endhighlight %}

It can also be used to apply conditional expressions, like this: `.books{.author.name === 'Robert C. Martin'}.title`.  Other comparison operators are also supported like `>=` and `!==`.  Logical operators can be used to combine predicates, and the API also supports substitution.

The author has included unit tests, and build scripts for generating a browser-friendly version.

###Strider

[Strider](http://strider-cd.com/) (GitHub: [Strider-CD / strider](https://github.com/Strider-CD/strider), License: _BSD_, npm: [strider](https://npmjs.org/package/strider)) by Niall O'Higgins is a continuous deployment solution built with Express and MongoDB.  It's designed to be easy to deploy to Heroku, and can be used to deploy applications to your own servers.  It directly supports Node and Python applications, and the author is also working on supporting Rails and JVM languages.

Strider integrates with GitHub, so it can display a list of your repositories and allow them to be deployed as required.  It can also test projects, so it can be used for continuous integration if deployment isn't required.

The documentation includes full details for installing Strider, linking a GitHub account, and then setting it up as a CI/CD server with an example project.
