---
layout: post
title: "Node Roundup: Node 0.11.15, PublicSuffixList, Robe"
author: Alex Young
categories:
- node
- modules
- libraries
- mongodb
---

###Node 0.11.15

[Node 0.11.15 is out](http://blog.nodejs.org/2015/01/20/node-v0-11-15-unstable/).  This is a substantial release that updates v8 to 3.28.73, npm to 2.1.6, and uv to 1.0.2.  There are patches for the build system and core modules as well.  I looked over the changes to the core modules and it looks like it's mostly bug fixes, but some modules (`url` and `readline`) have had performance improvements as well.

Meanwhile, [io.js](https://iojs.org/) was updated to 1.0.3.  This upgrades v8 from 3.31 to 4.1, which the [changelog notes](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) is not a major release because "4.1" is derived from Chrome 41.  There's also better platform support, including Windows XP, Windows 2003, and improved FreeBSD support.

If you look through the commits in both projects it should be obvious that some commits are shared, but some are unique to each fork.  There was a popular post on Hacker News about performance comparisons between [Node and io.js](https://news.ycombinator.com/item?id=8911301), so it'll be interesting to see how the projects diverge and converge over the next few months.

###PublicSuffixList

Matthias Thoemmes sent in PublicSuffixList (GitHub: [cmtt/publicsuffixlist](https://github.com/cmtt/publicsuffixlist), License: _MIT_, npm: [publicsuffixlist](https://www.npmjs.com/package/publicsuffixlist)), a validator for domain names and top level domains.  It uses data from Mozilla's [publicsuffix.org](https://publicsuffix.org/) project:

> A "public suffix" is one under which Internet users can directly register names. Some examples of public suffixes are .com, .co.uk and pvt.k12.ma.us. The Public Suffix List is a list of all known public suffixes.

The module provides methods like `validateTLD`, `validate(domainString)`, and you can also look up a domain to destructure it:

{% highlight javascript %}
var result = psl.lookup('www.domain.com');

/*
result === {
  domain: 'domain',
  tld: 'com',
  subdomain: 'www'
} */
{% endhighlight %}

###Robe

[Robe](http://hiddentao.github.io/robe/) (GitHub: [hiddentao/robe](https://github.com/hiddentao/robe/), License: _MIT_, npm: [robe](https://www.npmjs.com/package/robe)) by Ramesh Nair is a MongoDB ODM that uses ES6 generators.  The author said he couldn't quite find the MongoDB API that he wanted, although Mongorito came close.  So he used [Monk](https://github.com/Automattic/monk) to build Robe.

Because it supports generators you can `yield` results in the synchronous style:

{% highlight javascript %}
var result = yield collection.findOne({
  score: {
    $gt: 20
  },
}, {
  fields: ['name'],
  sort: { name: 1 },
  skip: 1,
});
{% endhighlight %}

It also supports lifecycle hooks, so you can run callbacks after or before data is inserted, removed, and so on.

Robe will validate data based on your schema, so running `yield collection.insert()` with an invalid record will cause an exception to be raised.  Finally, it also supports streams, so you can use an event-based API to handle large sets of data.
