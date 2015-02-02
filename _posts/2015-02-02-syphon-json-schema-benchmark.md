---
layout: post
title: "Syphon, json-schema-benchmark"
author: Alex Young
categories:
- node
- modules
- libraries
- react
- json
- json-schema
---

###Syphon

Syphon (GitHub: [scttnlsn/syphon](https://github.com/scttnlsn/syphon), License: _MIT_, npm: [syphon](https://www.npmjs.com/package/syphon)) by Scott Nelson is an implementation of the Flux architectural pattern for React.  It helps you to structure applications around a single immutable state value, and implements the dispatching of actions to various state-transitioning handler functions.

The application's state is stored in an immutable data structure that you create with the `atom` method.  To access a value, you `deref` it, and you can also modify it by using `swap`:

{% highlight javascript %}
var state = syphon.atom({ foo: 'bar' });

state.swap(function(current) {
  console.log(current.toJS());

  return current.set('foo', 'baz');
});

console.log(state.deref().toJS());
// => { foo: 'baz' }
{% endhighlight %}

Responding to state changes involves writing handlers, which takes the form of functions with two arguments: `value` and `currentState`.  The application's state is available in the second argument.

Syphon's author recommends using the [multimethod](https://www.npmjs.com/package/multimethod) module to deal with handlers that branch on multiple values.

Syphon includes the `root` method for mounting your component hierarchy, and a mixin for adding helpers to components for accessing application data and dispatch values.

###json-schema-benchmark

I may need to create some JSON schemas in the near future, so it was fortunate that Allan Ebdrup sent in [json-schema-benchmark](https://github.com/Muscula/json-schema-benchmark).  This is a benchmark for JSON schema validators, and covers the following modules:

* [`is-my-json-valid`](https://github.com/mafintosh/is-my-json-valid)
* [`themis`](https://github.com/playlyfe/themis)
* [`z-schema`](https://github.com/zaggino/z-schema)
* [`jjv`](https://github.com/acornejo/jjv)
* [`skeemas`](https://github.com/Prestaul/skeemas)
* [`jayschema`](https://github.com/natesilva/jayschema)
* [`jsck`](https://github.com/pandastrike/jsck)
* [`jassi`](https://github.com/iclanzan/jassi)
* [`JSV`](http://github.com/garycourt/JSV)
* [`request-validator`](https://github.com/bugventure/request-validator)
* [`json-gate`](https://github.com/oferei/json-gate)
* [`json-model`](https://github.com/geraintluff/json-model)
* [`tv4`](https://github.com/geraintluff/tv4)
* [`jsonschema`](https://github.com/tdegrunt/jsonschema)
* [`revalidator`](https://github.com/flatiron/revalidator)

It also shows test failures when run against the official [JSON Schema Test Suite](https://github.com/json-schema/JSON-Schema-Test-Suite).  One cool addition is a summary of tests that caused side-effects, so you can see which validators altered values.
