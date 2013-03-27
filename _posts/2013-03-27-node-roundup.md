---
layout: post
title: "Node Roundup: wish, Vow, shell-jobs"
author: "Alex Young"
categories:
- node
- modules
- testing
- promises
- async
- time
- daemons
- unix
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###wish

wish (GitHub: [EvanBurchard / wish](https://github.com/evanburchard/wish), License: _MIT_, npm: [wish](https://npmjs.org/package/wish)) by Evan Burchard is an assertion module designed to raise meaningful, human-readable errors.  When assertions fail, it parses the original source to generate a useful error message, which means the standard comparison operators can be used.

For example, if `wish(a === 5)` failed an error like this would be displayed:

{% highlight text %}
WishError:
  Expected "a" to be equal(===) to "5".
{% endhighlight %}

If `assert(a === 5)` had been used instead, `AssertionError: false == true` would have been raised.  A fairer comparison would be `assert.equal`, which would produce `AssertionError: 4 == 5`, but it's interesting that wish is able to introspect the variable name and add that to the error.

###Vow

Vow (GitHub: [dfilatov / jspromise](https://github.com/dfilatov/jspromise), License: _MIT/GPL_, npm: [vow](https://npmjs.org/package/vow)) by Filatov Dmitry is a [Promises/A+](https://github.com/promises-aplus/promises-spec) implementation.  Promises can be created, fulfilled, and rejected -- you should be able to get the hang of it if you've used libraries with `then` methods elsewhere, but there are some [differences to Promises/A](https://github.com/promises-aplus/promises-spec/blob/master/differences-from-promises-a.md) which feels like it actually simplifies some of the potentially messier parts of the [original CommonJS specification](http://wiki.commonjs.org/wiki/Promises/A).

Here's an example of the Vow API:

{% highlight javascript %}
var promise1 = Vow.promise(),
    promise2 = Vow.promise();

Vow.all([promise1, promise2, 3])
  .then(function(value) {
    // value is [1, 2, 3]
  });

promise1.fulfill(1);
promise2.fulfill(2);
{% endhighlight %}

The author has written some pretty solid looking tests, and benchmarks are included as well.  The project performs favorably when compared to other popular promise libraries:

<table>
  <thead>
    <tr><th>&nbsp;</th><th>mean time</th><th>ops/sec</th></tr>
  </thead>
  <tbody>
    <tr>
      <th>Q</th><td>54.891ms</td><td>18</td>
    </tr>
    <tr>
      <th>When</th><td>3.484ms</td><td>287</td>
    </tr>
    <tr>
      <th>Vow</th><td>1.158ms</td><td>864</td>
    </tr>
  </tbody>
</table>

###shell-jobs

I like seeing daemons made in Node, and Azer Koçulu recently sent in a cron-inspired daemon called shell-jobs (GitHub: [azer / shell-jobs](https://github.com/azer/shell-jobs), License: _MIT_, npm: [shell-jobs](https://npmjs.org/package/shell-jobs)).  It uses `.jobs` files that are intended to be human readable.  All you need to do is write a shell command followed by a `# =>` and then a time:

{% highlight text %}
cowsay "Hello" > /tmp/jobs.log # => 2 minutes
{% endhighlight %}

The `shell-jobs` script will then parse this file and output the following:

{% highlight text %}
  jobs Starting "cowsay "Hello" > /tmp/jobs.log" [2 minutes] +2ms
{% endhighlight %}

After two minutes has passed the job will be executed:

{% highlight text %}
  exec 1. Running cowsay "Hello" > /tmp/jobs.log. +0ms
{% endhighlight %}


