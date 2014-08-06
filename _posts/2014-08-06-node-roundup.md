---
layout: post
title: "Node Roundup: V8 Vulnerability, git-promise, awesome-nodejs"
author: "Alex Young"
categories:
- node
- modules
- security
- git
---

###V8 Memory Corruption

The versions of V8 included with Node 0.8 and 0.10 were found to have a memory corruption vulnerability.  The issue was discovered by a security specialist, and then a core Node contributor worked with the V8 team to fix the problem.  More details can be found in the [V8 Memory Corruption and Stack Overflow](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow/) post on the Node blog.

That means [Node 0.8.28](http://blog.nodejs.org/2014/07/31/node-v0-8-28-maintenance/) and [Node 0.10.30](http://blog.nodejs.org/2014/07/31/node-v0-10-30-stable/) have been released which both include a fix.  0.10.30 also has some changes to several core modules, including buffer, streams, and child process.

###git-promise

git-promise (GitHub: [piuccio / git-promise](https://github.com/piuccio/git-promise), License: _MIT_, npm: [git-promise](https://www.npmjs.org/package/git-promise)) by Fabio Crisci is a promise-based wrapper for Git:

{% highlight javascript %}
var git = require('git-promise');

git('rev-parse --abbrev-ref HEAD').then(function(branch) {
  console.log(branch); // This is your current branch
});
{% endhighlight %}

The readme has more advanced examples, like finding the commit where master diverged from your current branch.  Fabio has included some tests written with nodeunit.

###awesome-nodejs

Sindre Sorhus sent in [awesome-nodejs](https://github.com/sindresorhus/awesome-nodejs), a curated list of Node modules and resources.  It's a handy list to check if you're looking for a module and are overwhelmed by choice, or not sure where to start on a topic.

There's also an [awesome list of awesome lists](https://github.com/sindresorhus/awesome), which leads to [awesome-javascript](https://github.com/sorrycc/awesome-javascript), and then back again.


