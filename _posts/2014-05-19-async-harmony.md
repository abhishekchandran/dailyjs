---
layout: post
title: "Async Harmony Tests"
author: "Alex Young"
categories:
- es6
- async
- firefox
---

Simeon Velichkov sent in [async-harmony tests](https://simov.github.io/async-harmony/test/) (GitHub: [simov / async-harmony](https://github.com/simov/async-harmony), License: _MIT_), which contains examples of new ES6 features.  Each example is based on methods from [async](https://www.npmjs.org/package/async), but written using new features like generators, including arrow functions.

It only currently works in Firefox 29, but I thought the examples were quite interesting:

{% highlight javascript %}
function eachSeries (items, job, done, kill=true) {
  var results = [], errors = [];

  var it = iterator();
  it.next();

  function* iterator () {
    for (let item of items) {
      yield job(item, (err, result) => {
        if (kill && err) return done(err);
        if (err) errors.push(err);
        results.push(result||null);
        setTimeout(() => it.next(), 0);
      });
    }
    done((errors.length ? errors : null), results);
  }
}
{% endhighlight %}

The corresponding usage looks like this:

{% highlight javascript %}
async.eachSeries([0,1], (item, done) => {
  done(new Error('error'+item));
}, (err, result) => {
  err.message.should.equal('error0');
  done();
});
{% endhighlight %}

Give them a read if you're interesting in seeing ES6 in action.
