---
layout: post
title: "ForerunnerDB, rdb"
author: Alex Young
image: "/images/posts/forerunner.png"
categories:
- node
- libraries
- databases
---

###ForerunnerDB

![ForerunnerDB](/images/posts/forerunner.png)

Rob Evans sent in [ForerunnerDB](http://www.forerunnerdb.com) (GitHub: [Irrelon/ForerunnerDB](https://github.com/Irrelon/ForerunnerDB), License: _MIT_, npm: [forerunnerdb](https://www.npmjs.com/package/forerunnerdb)), a new database written with Node that uses MongoDB's query language.

> ForerunnerDB was created primarily to allow web application developers to easily store, query and manipulate JSON data in the browser via a simple query language. It provides the ability to store data passed by an API to the front-end and query it throughout your application making handling JSON data client-side significantly easier.
>
> Furthermore, if you use the optional data-binding module, changes to your JSON data stored in ForerunnerDB are automatically propagated to the DOM. Some web application frameworks provide similar functionality which is why data-binding is an optional module.

The data-binding layer is optional, and is provided through a separate module.  It depends on jQuery, and works using data attributes.  It's a little bit like KnockoutJS.

This project seems ideal if you're trying to create single page applications that receive initial chunks of JSON from the server, and if your team is used to MongoDB.  Browser-based persistence is available through IndexedDB, WebSQL, and LocalStorage.

One unique feature of ForerunnerDB is iOS support.  It's still experimental, but sounds like it could be useful for transitioning single page apps to native iOS applications:

> The iOS version is part of the roadmap and will include data-binding for list structures like UITableView, as well as individual controls like UILabel. Data-persistence is already working as well as inserting and basic data queries, update and remove.

###rdb

rdb (GitHub: [alfateam/rdb](https://github.com/alfateam/rdb), License: _MIT_, npm: [rdb](https://www.npmjs.com/package/rdb)), a new ORM module, was posted to [Hacker news today](https://news.ycombinator.com/item?id=9073033), and got lots of interest.  Finding the right ORM is always difficult, but this one already has support for transactions, lazy loading, and promises.  It supports PostgreSQL and MySQL. Someone on Hacker News mentioned the lack of SQLite support, but I always run a local version of the database I'm going to deploy against, just because I don't trust ORMs to work seamlessly between databases.

If you like promises, you may prefer rdb to the Active Record-inspired ORMs that most people seem to use.  Given some suitable functions, you can write clean statements like this:

{% highlight javascript %}
db.transaction()
  .then(insert)
  .then(getById)
  .then(verifyInserted)
  .then(rdb.commit)
  .then(null, rdb.rollback)
  .then(onOk, onFailed);
{% endhighlight %}

I've taken this from the [rdb documentation and examples](https://github.com/alfateam/rdb/blob/master/docs/docs.md#_manytodto).  The main developer, Lars-Erik Roald, has been working on this module since May 2013, and he said it's [used commercially on Hacker News](https://news.ycombinator.com/item?id=9073543), so you should give it a try if you haven't found the right ORM yet.
