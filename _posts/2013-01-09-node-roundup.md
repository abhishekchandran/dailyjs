---
layout: post
title: "Node Roundup: AsyncMachine, require-directory, sayeasy"
author: "Alex Young"
categories: 
- node
- modules
- audio
- express
- async
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###AsyncMachine

[AsyncMachine](https://github.com/TobiaszCudnik/asyncmachine) (License: _MIT_, npm: [asyncmachine](https://npmjs.org/package/asyncmachine)) by Tobiasz Cudnik is a state machine for declaring asynchronous logic.  It's written in TypeScript, and supports state definition using an object-oriented API.

Transitions between states are exposed using an `EventEmitter`, and promises are supported for "deferred state changes".  Although the project is written with TypeScript, the documentation includes a plain JavaScript example.

AsyncMachine isn't based on a formalised state machine design, but it has an interesting blend of concepts from other finite state machine implementations, asynchronous programming in Node, and object-oriented design.  It's definitely got a lot of ideas on how to deal with state in an asynchronous environment.

###require-directory

[require-directory](https://github.com/TroyGoode/node-require-directory) (License: _MIT_, npm: [require-directory](https://npmjs.org/package/require-directory)) by [Troy Goode](https://twitter.com/troygoode) allows directories to be loaded with `require` as if an `index.js` file had been used.

If you've got a project with an `index.js` file -- let's say it's in `routes/`, and it looks like this:

{% highlight javascript %}
module.exports = {
  auth: require('./auth')
, products: require('./products')
, categories: require('./categories')
};
{% endhighlight %}

When it's loaded using `require('./routes')`, you'll get an object with `auth`, `products`, and `categories`.  Troy argues that this can cause maintenance problems, and prefers to write the `index.js` file like this: `module.exports = require('require-directory')(module);`.

Files can also be blacklisted and whitelisted, and `index.js` will be automatically ignored.

###sayeasy

[sayeasy](https://github.com/smithclay/sayeasy) (License: _MIT_, npm: [sayeasy](https://npmjs.org/package/sayeasy)) by Clay Smith is a RESTful wrapper around Mac OS X's `say` command, created with Express.  The author is using it to speak notifications in a continuous integration environment -- you could have a sayeasy server in your office that speaks when tests start to fail.

It also has a command-line wrapper, allowing messages to be sent to a central sayeasy server.

