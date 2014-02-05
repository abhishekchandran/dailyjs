---
layout: post
title: "Node Roundup: bitcoinaddress.js, atry, Node Web Modules"
author: Alex Young
categories:
- node
- modules
- apps
- bitcoin
---

###bitcoinaddress.js

If you need to take Bitcoin payments on your site, then [bitcoinaddress.js](http://miohtama.github.io/bitcoinaddress.js/) (GitHub: [miohtama / bitcoinaddress.js](https://github.com/miohtama/bitcoinaddress.js), License: _MIT_, npm: [bitcoinaddress](https://npmjs.org/package/bitcoinaddress)) by Mikko Ohtamaa might help.  It's a module for handling Bitcoin payments.  It can be run as a client-side script, or as a Node module.  It allows Bitcoins to be sent, or specific currency amounts based on "fiat" amounts.

It's based around `bitcoin:` URIs, and allows you to display "Pay from wallet" links on your pages.  It also displays QR codes so people can easily make payments using mobile Bitcoin apps.

###atry

atry (GitHub: [CodeCharmLtd / atry](https://github.com/CodeCharmLtd/atry), License: _MIT_, npm: [atry](https://npmjs.org/package/atry)) from Code Charm (Damian Kaczmarek) is an alternative to Node's domain module.  The basic idea is to allow exceptions to be caught using an asynchronous API:

{% highlight javascript %}
atry(function() {
  setTimeout(function() {
    throw new Error('I am Error');
  }, 10);
}).catch(function(err) {
  console.log('Error:', err);
});
{% endhighlight %}

It has an `intercept` method that returns an "exception safe" callback that you can pass as a callback to asynchronous APIs like `fs.readFile`.

###Node Web Modules

[Node Web Modules](http://nodewebmodules.com/) (GitHub: [caio-ribeiro-pereira / node-web-modules](https://github.com/caio-ribeiro-pereira/node-web-modules), License: _MIT_) by Caio Ribeiro Pereira is a Node web application that shows a list of popular web frameworks for Node.  If you select one of the modules it shows a screenshot and some statistics.

The project is powered by Express and Redis, and it uses the GitHub API.  The module list it displays on <http://nodewebmodules.com/> is useful for beginners, but you might also like to take a look at the source to see how it works.
