---
layout: post
title: "ES6 for Node"
author: Alex Young
categories:
- node
- ES6
- tutorials
---

In [Harmony of Dreams Come True](https://brendaneich.com/2012/10/harmony-of-dreams-come-true/), Brendan Eich discusses the "new-in-ES6 stuff" that is starting to come to fruition.  Although his discussion mostly focuses on Mozilla-based implementations, he does relate upcoming language features to a wide range of JavaScript projects, including games.  This is relevant to Node developers because ECMAScript 6 _is_ happening, and changes are already present in V8 itself.

Let's look at some of these changes in a moment.  For now you might be wondering how to track such changes as they become available in Node.  When new builds of Node are released, the version of V8 is usually mentioned if it has changed.  You can also view the commit history on GitHub for a given release tag to see what version of V8 has been used, or take a look at the value of [process.versions](http://nodejs.org/docs/latest/api/all.html#all_process_versions):

{% highlight text %}
~  node -e 'console.log(process.versions)'
{ http_parser: '1.0',
  node: '0.8.12',
  v8: '3.11.10.22',
  ares: '1.7.5-DEV',
  uv: '0.8',
  zlib: '1.2.3',
  openssl: '1.0.0f' }
{% endhighlight %}

Once you've got the V8 version, you can check take a look at the [V8 ChangeLog](http://v8.googlecode.com/svn/trunk/ChangeLog) to see what has been included.  Just searching that text for "Harmony" shows the following for Node 0.8.12:

* Block scoping
* Harmony semantics for typeof
* `let` and `const`
* `Map` and `WeakMap`
* Module declaration
* The `Proxy` prototype

###Running Node with Harmony Options

Typing `node --v8-options` shows all of the available V8 options:

* `--harmony_typeof`: Enable harmony semantics for typeof
* `--harmony_scoping`: Enable harmony block scoping
* `--harmony_modules`: Enable harmony modules (implies block scoping)
* `--harmony_proxies`: Enable harmony proxies
* `--harmony_collections`: Enable harmony collections (sets, maps, and weak maps)
* `--harmony`: Enable all harmony features (except typeof)

To actually use one of these options, just include it when running a script:

{% highlight javascript %}
node --harmony script.js
{% endhighlight %}

###Example: `typeof`

The `--harmony_typeof` option is special because it isn't included with `--harmony`, this is most likely because the proposal was rejected: [harmony:typeof_null](http://wiki.ecmascript.org/doku.php?id=harmony:typeof_null&s=typeof).  The possibility of a proposal being rejected is part of working with cutting edge language features -- if you're unsure about the status of a given feature the best thing to do is search the [ECMAScript DokuWiki](http://wiki.ecmascript.org/doku.php).

With this option enabled, `typeof null === "null"` is `true`.

###Example: Type Checking

Standard Node 0.8 without the `--harmony` flag supports `isNaN` and `isFinite`.  However, `toInteger` and `isInteger` don't seem to be supported yet.

{% highlight javascript %}
var assert = require('assert');

assert(!isNaN(1));
assert(!isNaN('1'));
assert(isNaN('test'));
assert(isFinite(1));
assert(!isFinite(1/0));
{% endhighlight %}

###Example: Block Scoping

Strict mode helps fix a major JavaScript design flaw: a missing `var` statement makes a variable globally visible.  ES6 goes a step further by introducing `let` which can be used to create block-local variables.  The following example must be run with `node --use-strict --harmony`:

{% highlight javascript %}
for (let i = 0; i < 3; i++) {
  console.log('i:', i);
}

console.log(i);
{% endhighlight %}

The final statement, `console.log(i)`, will cause a `ReferenceError` to be raised.  The variable `i` is out of scope.  Great, but doesn't that mean forgetting `let` will just create a global?  No, because in that case strict mode causes a `ReferenceError` to be raised.

The advantages of `let` are paired with `const` -- by declaring a constant in global code the semantics are clear, and leaking uninitialised properties into the global object is avoided.

###Example: Collections

ES6 adds new APIs for dealing with groups of values: `Map`, `Set`, and `WeakMap`.  The `Map` constructor allows any object or primitive value to be mapped to another value.  This is confusing because it sounds similar to plain old objects, but that's only because we often use objects to implement what maps are designed to solve more efficiently.

{% highlight javascript %}
var assert = require('assert')
  , m = new Map()
  , key = { a: 'Test' }
  , value = 'a test value'
  ;

m.set(key, value);

assert.equal(m.get(key), value);
{% endhighlight %}

This example shows that map keys don't need to be converted to strings, unlike with objects.

Node also currently has `Set` when running with `--harmony`, but instantiation with an array doesn't seem to work yet, and neither does `Set.prototype.size`.

{% highlight javascript %}
var assert = require('assert')
  , s = new Set()
  ;

s.add('a');

assert.ok(s.has('a'));
{% endhighlight %}

Finally, `WeakMap` is a form of map with _weak_ references.  Because `WeakMap` holds weak references to objects, the keys are not enumerable.  The advantage of this is the garbage collector can remove entries when they're no-longer in use.  To justify the relevance of `WeakMap`, Brendan mentioned the [Ephemeron](http://en.wikipedia.org/wiki/Ephemeron):

> Ephemerons solve a problem which is commonly found when trying to "attach" properties to objects by using a registry. When some property should be attached to an object, the property should (in terms of GC behavior) typically have the life-time that an instance variable of this object would have.

So the `WeakMap` API should give us a memory-efficient and faster-than-O(n) key/value map.

There's a post from last year by Andy E called [ES6 – a quick look at Weak Maps](http://whattheheadsaid.com/2011/10/es6-a-quick-look-at-weak-maps) that relates `WeakMap` to jQuery's expando property:

> Weak maps come in here because they can do the job much better. They cut out the need for the expando property entirely, along with the requirement of handling JS objects differently to DOM objects. They also expand on jQuery's ability to allow garbage collection when DOM elements are removed by its own methods, by automatically allowing garbage collection when DOM elements no longer reachable after they've been removed by any method.

I tried creating some instances of `WeakMap` with circular references and forcing the garbage collector to run by using `node --harmony --expose_gc` and calling `gc()`, but it's difficult to tell if the object is actually being removed yet:

> We can't tell, however: there's no way to enumerate a `WeakMap`, as doing so could expose the GC schedule (in browsers, you can't call `gc()` to force a collection). Nor can we use `wm.has` to probe for entries, since we have nulled our `objkey` references!

###Proxies

The current version of Node seems to include the [old Proxy API](http://wiki.ecmascript.org/doku.php?id=harmony:proxies), so I don't think it's worth exploring here.  The [newer Proxy API](http://wiki.ecmascript.org/doku.php?id=harmony:direct_proxies) doesn't seem to work as expected, and I can't find specific mention of a change to the new API style in the V8 issues or developer mailing list.

###Generators, Classes, and Macros

Generators, classes, and macros are not currently supported by V8.  These are still hotly debated areas, which you can read more about on the ECMAScript DokuWiki:

* [Generators](http://wiki.ecmascript.org/doku.php?id=harmony:generators)
* [Classes](http://wiki.ecmascript.org/doku.php?id=harmony:classes)

Andreas Rossberg said [the V8 developers are aware of generators](https://groups.google.com/d/msg/v8-users/mV38oWvA2Nk/txtSzVdDhpUJ), but there aren't any concrete plans for supporting them yet.

[Destructuring](http://wiki.ecmascript.org/doku.php?id=harmony:destructuring) has been added to the draft ECMAScript 6 specification.

If you're desperate to try macros in Node now, Mozilla released [sweet.js](http://sweetjs.org/) (GitHub: [mozilla / sweet.js](https://github.com/mozilla/sweet.js), License: _BSD_, npm: [sweet.js](https://npmjs.org/package/sweet.js)) a few weeks ago.  It's a command-line tool that "compiles" scripts, in a similar way to CoffeeScript.  This isn't specifically an ES6 shim, although there are plenty of those out there.  Some new features like `WeakMap` seem like they can be supported using shims, but a complete implementation isn't always possible in older versions of ECMAScript.

###References

* [Harmony of Dreams Come True](https://brendaneich.com/2012/10/harmony-of-dreams-come-true/) by Brendan Eich
* [MDN: Map](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Map)
* [MDN: Set](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Set)
* [MDN: WeakMap](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/WeakMap)
* [ES6 – a quick look at Weak Maps](http://whattheheadsaid.com/2011/10/es6-a-quick-look-at-weak-maps) by Andy E
