---
layout: post
title: "Node Roundup: Knockout, bignumber.js, r...e, Mongoose-Filter-Denormalize"
author: "Alex Young"
categories: 
- node
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node.js Knockout

![Node.js Knockout site](/images/posts/nodeknockout.png)

[Node.js Knockout](http://nodeknockout.com/) is currently being judged, the winners will be announced on the 20th of November.  The site is actually a small game in itself -- click around to move your character and type to say something.

###bignumber.js

[bignumber.js](https://github.com/MikeMcl/bignumber.js) (License: _MIT Expat_, npm: [bignumber.js](https://npmjs.org/package/bignumber.js)) by Michael Mclaughlin is an arbitrary-precision arithmetic module.  It works in Node, browsers, and is available as an AMD module.  It comes with both tests and benchmarks, which is useful because one of Mile's goals was to write something faster and easier to use than JavaScript versions of Java's BigDecimal.

Objects created with `BigNumber` behave like the built-in `Number` type in that they have  `toExponential`, `toFixed`, `toPrecision`, and `toString` methods.

Mike found the only other serious arbitrary-precision library for decimal arithmetic on npm is [bigdecimal](https://npmjs.org/package/bigdecimal), which originates from the Google GWT project.  Mike has written some examples of [bigdecimal's problems](https://github.com/MikeMcl/bignumber.js/tree/master/perf/lib/bigdecimal_GWT/bugs.js) to illustrate bugs he found while working with it, and offers bignumber.js as an alternative.

###r...e

[r...e](https://github.com/vesln/r...e) (License: _MIT_, npm: [r...e](https://npmjs.org/package/r...e)) by Veselin Todorov is a module for manipulating range expressions.  Ranges are specified as separate arguments or strings, and a suitable array will be returned:

{% highlight javascript %}
range(1, 3).toArray();
range('1..3').toArray();
// [1, 2, 3]

range('a', 'c').toArray();
// ['a', 'b', 'c']
{% endhighlight %}

Stepped ranges are supported (`0, 10, 5`) as well as convenience methods like `range(1, 3).include(2)`, `map`, `join`, `sum`, and so on.  It works in browsers, and includes Mocha tests.

###Mongoose-Filter-Denormalize

[Mongoose-Filter-Denormalize](https://github.com/STRML/mongoose-filter-denormalize) (License: _MIT_) by Samuel Reed is a filtering and denormalization for Mongoose -- it essentially provides a way of preventing Mongoose from accidentally exposing sensitive data:

{% highlight javascript %}

UserSchema.plugin(filter, {
  readFilter: {
    'owner' : ['name', 'address', 'fb.id', 'fb.name', 'readOnlyField'],
    'public': ['name', 'fb.name']
  },
  writeFilter: {
    'owner' : ['name', 'address', 'fb.id', 'writeOnlyField']
  },
  // 'nofilter' is a built-in filter that does no processing, be careful with this
  defaultFilterRole: 'nofilter',
  sanitize: true // Escape HTML in strings
});
{% endhighlight %}

Now when passing the result of a `findOne` or other query to, say, `res.send` in your Express app, fields can be restricted based on user:

{% highlight javascript %}
User.findOne({ name: 'Foo Bar' }, User.getReadFilterKeys('public')), function(err, user) {
  if (err) next(err);
  res.send({ success: true, users: [user] });
});
{% endhighlight %}
