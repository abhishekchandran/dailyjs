---
layout: post
title: "Node Roundup: Unifying Node with io.js, JSON Object to JSON Schema, conveyor-belt"
author: Alex Young
categories:
- node
- libraries
- modules
- connect
- express
- iojs
- json-schema
---

###StrongLoop on Unifying Node with io.js

The StrongLoop blog has a post by Issac Roth about [the unification of Node and io.js](http://strongloop.com/strongblog/node-js-foundation-io-js-unification/):

> Unification is something you can help with! The io.js repository and the Node Google group are open to all. Get involved, post issues and comments, let people know your ideas and solutions.  Tell people where you stand on the issue. I've worked with all of the contributors in small or large ways and they are each kind people--if they hear from a wide swath of the community something you want, it will surely get considered, as everyone I've met likes to serve the community.

Issac is involved with both the Node Advisory Board and [Node Forward](http://nodeforward.org/).  Bert Belder, also at StrongLoop, is also involved with these groups as well, and works with Issac.  This post gives a good insight into what's happening with Node and io.js, which is sometimes bewildering to outsiders, particularly if you pay attention enough to see core contributors switching to io.js with seemingly no explanation.

And, according to Issac, the technical divergence between the projects might not be as extreme as some people make out:

> Having witnessed some of the early discussions between the io.js technical committee and the Joyent contributors, there are only a small number of points of disagreement on both governance (stuff like how voting would happen if needed) and technical decisions (stuff like which version of v8 to use in the next release.)

He ends saying that he's confident that we'll end up with a single Node project.  I don't personally have a problem with forks existing, but it would make my life easier if I only had to write about one "Node".

###JSON Object to JSON Schema

Nijiko Yonskai, who has sent in several small but perfectly well-formed Node modules, has recently published JSON Object to JSON Schema (GitHub: [Nijikokun/generate-schema](https://github.com/Nijikokun/generate-schema), License: _MIT_, npm: [generate-schema](https://www.npmjs.com/package/generate-schema)).  This project helps you to convert JSON objects to schemas:

{% highlight javascript %}
var GenerateSchema = require('generate-schema')
 
console.log(GenerateSchema({
  "_links": {
    "self": {
      "href": "/gists/42"
    },
    "star": {
      "href": "/gists/42/star"
    }
  },
  "id": "42",
  "created_at": "2014-04-14T02:15:15Z",
  "description": "Description of Gist",
  "content": "String contents"
}));
{% endhighlight %}

This outputs an object with the types based on the content, so in this case it's mostly `{ "type": "string" }`.  I've recently been creating JSON schemas from existing JSON data sets, so this would have made my job easier!

###conveyor-belt

Svilen Gospodinov sent in conveyor-belt (GitHub: [svileng/conveyor-belt](https://github.com/svileng/conveyor-belt), License: _MIT_, npm: [conveyor-belt](https://www.npmjs.com/package/conveyor-belt)).  It's designed to switch client-side assets based on the current environment, so you can easily load development mode client-side scripts with lots of logging.

It looks like it'll work well with Connect/Express-based applications, but you could use it with other frameworks as well.
