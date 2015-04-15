---
layout: post
title: "Private npm Modules, Rust ffi, Ruff"
image: "/images/posts/npm-private-modules.png"
author: Alex Young
categories:
- node
- modules
- npm
- libraries
- generators
- es6
---

###Private npm Modules

![Private npm](/images/posts/npm-private-modules.png)

[npm private modules are here!](https://www.npmjs.com/private-modules) This is something that people have wanted for a long time.  There are ways to do this yourself, including third-party services and using private Git repositories.  The actual production version is a little bit different to simply limiting who can see packages, however.  For $7 a month you can have unlimited private packages, and grant read-write access to any other paid user.  You can also collaborate on packages, which means other people can release your private module.

Packages are scoped under your username, and you can use the command-line tool to add collaborators.

Despite the low fee, I suspect many readers would prefer that their employer paid for the subscription.  Fortunately, organisational accounts are coming:

> Currently, private packages are only available for individual users, but support for organization accounts is coming soon. Feel free to create a user for your organization in the meantime, and we can upgrade it to an organization when support is here.

This implies that an organisational account will be an umbrella account for multiple users, so I expect pricing will differ to the individual account.  I'm going to pay for an individual account right now because I think npm is cool, even though I really want an organisational account!

npm was also mentioned on TechCrunch because it [recently raised $8M](http://techcrunch.com/2015/04/14/popular-javascript-package-manager-npm-raises-8m-launches-private-modules/):

> The new funding, Schlueter says, will mostly go toward hiring to push npm's product roadmap forward (the company currently has eleven employees). This is partly driven by Schlueter's philosophy around developer productivity. "When you are running this registry with 2.4 million users using it on a regular basis, you need a lot of reliability etc. — and that takes people," he said. "So you can either burn your employees out or build the company in a sustainable fashion."

###Rust ffi

[Matias Piipari](https://github.com/mz2) sent me [Andrew Oppenlander's Rust ffi tutorial](http://oppenlander.me/articles/rust-ffi), which explains how to extend Node with Rust.

> Rust is an excellent candidate for an embedded language. In a larger project, it provides safety, which helps protect against memory issues, and speed, which keeps the host platform responsive by letting Rust do the heavy lifting.
>
> I've implemented this boilerplate and example bindings for JavaScript/nodejs in Rust ffi. All JavaScript library and testing code is stored in the js folder and it is a valid NPM module, which will compile the Rust dylib on install.

The tutorial shows you how to make a Rust dynamic library, and how to use ffi to convert between C types and Rust types and call Rust from Node:

> The JavaScript code is fairly straightforward, with the help of node-ffi. We just need to tell it where our dynamic library is and stub out what the C ABI function signature look like. The signature uses the C types from ref, which is used internally in node-ffi.

###Ruff

Coderaiser sent in Ruff (GitHub: [coderaiser/ruff](https://github.com/coderaiser/ruff), License: _MIT_, npm: [ruff](http://npmjs.com/package/ruff)), a module that mashes up coroutines with ES6 generators and `EventEmitter`.

{% highlight javascript %}
var ruff = require('ruff');
var minify = require('minify');

ruff(function*() {
  var first = minify.bind(null, '1.js');
  var second = minify.bind(null, '2.js');

  yield [first, second];
  console.log('done');
}).on('error', function(error) {
  console.log(error);
}).on('end', function() {
  console.log('ok what\'s next?');
});
{% endhighlight %}

This example uses Coderaiser's [minify](https://www.npmjs.com/package/minify) module to minify two JavaScript files in parallel.  Because the API is based on `EventEmitter` it should be relatively easy to understand for Node programmers.
