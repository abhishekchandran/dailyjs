---
layout: post
title: "Recreating core.async with ES6 Generators, JSON Mask"
author: Alex Young
categories:
- tutorials
- node
- json
- es6
- generators
- clojure
---

###Recreating core.async with ES6 Generators

[Recreating core.async with ES6 Generators](http://andreypopp.com/posts/2013-11-09-recreating-core-async-tutorial-with-es6-generators.html) is a post by Andrey Popp inspired by Clojure's core.async.  He uses Browserify with a transpiler module that allows ES6 generators to be used in browsers:

{% highlight javascript %}
function *listen(el, evType) {
  while (true)
    yield function(cb) {
      var fire = function(ev) {
        el.removeEventListener(evType, fire);
        cb(null, ev);
      }
      el.addEventListener(evType, fire);
    }
}
{% endhighlight %}

The tutorial goes on to use JSONP to fetch data from the Wikipedia API.  The full source is available as a gist: [andreypopp / index.html](https://gist.github.com/andreypopp/7385755).

###JSON Mask

[JSON Mask](https://github.com/nemtsov/json-mask) (GitHub: [nemtsov / json-mask](https://github.com/nemtsov/json-mask), License: _MIT_, npm: [json-mask](https://npmjs.org/package/json-mask)) by Yuriy Nemtsov is a module that provides a DSL for filtering JSON.  It works in browsers, includes unit tests, and there's also [Express middleware](https://github.com/nemtsov/express-partial-response) that can help you filter responses in your Express applications.

> One use-case is when you have an HTTP service that returns `{"name": "mary", "age": 25}` (for example), and you have two clients: (1) that needs all of that information, and (2) that just needs the `name`.

> Now, if the server uses JSON Mask, it would accept a `?fields=` query-string. The (2)nd client would then add the following query-string to the request: `?fields=name`; after which the server would respond with `{"name": "mary"}`, and filter out the rest of the information.

> This *saves bandwidth* and *improves performance*; especially on large objects.

> Although trivial in the simplest cases, the task of filtering objects becomes a difficult one quickly. This is why JSON Mask is actually a tiny (and highly optimized) language that is loosely based on XPath, and has support for filtering parts of objects, arrays, wild-card filtering and combinations of the three. So, here's a less trivial example and usage (note how p/a/b is filtered out):

