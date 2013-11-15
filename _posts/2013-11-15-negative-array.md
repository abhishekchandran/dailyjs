---
layout: post
title: "Negative Array Indexes"
author: "Alex Young"
categories: 
- node
- modules
- es6
- code-review
---

Sindre Sorhus sent in [negative-array](https://github.com/sindresorhus/negative-array), a module for supporting negative array indexes.  It's built using [ES6's Proxy](http://soft.vub.ac.be/~tvcutsem/proxies/).

Proxies allow you to run methods when certain conditions are met, which means things like profilers become easier to implement.  They're created with `var proxy = Proxy(target, handler)`, where `target` is an object that will be wrapped with the proxy, and `handler` is an object that implements the proxy API.

The handler can include methods like `has`, `defineProperty`, `getPrototypeOf`, and more, for controlling access to an object.  For more details on how this works, see the [Direct Proxies](http://wiki.ecmascript.org/doku.php?id=harmony:direct_proxies) page on the ECMAScript Harmony Wiki.

Sindre's module allows you to do this:

{% highlight javascript %}
var negativeArray = require('negative-array');

// adds negative array index support to any passed array
var unicorn = negativeArray(['pony', 'cake', 'rainbow']);

// get the last item by using an negative index
console.log(unicorn[-1]);
{% endhighlight %}

It'll work in Node 0.8+ with the `--harmony` flag, and Chrome with Harmony enabled.  Visit `chrome://flags/#enable-javascript-harmony` to set it up.

The implementation is what will probably become a classic pattern: `Proxy` is used to wrap the array instance with `get` and `set` methods that dynamically map the requested array index to something native JavaScript can handle.

{% highlight javascript %}
Proxy(arr, {
  get: function (target, name) {
    var i = +name;
    return target[i < 0 ? target.length + i : i];
  },
  set: function (target, name, val) {
    var i = +name;
    return target[i < 0 ? target.length + i : i] = val;
  }
});
{% endhighlight %}

I like this example because it adds new functionality that feels like a language feature without changing built-in prototypes.  It's clean and fairly easy to understand once you know what `Proxy` does.  If you wanted to learn about proxies but couldn't find any good examples, then check out the source on GitHub.
