---
layout: post
title: "Assertion Counting in Mocha"
author: "Alex Young"
categories: 
- node
- libraries
- testing
- mocha
---

A few weeks ago I wrote about node-tap, in [Why Don't You Use Tap?](http://dailyjs.com/2013/10/21/tap/).  I usually use Mocha for my tests, and one thing I liked about node-tap was the idea of test plans:

{% highlight javascript %}
test('Check out my plan', function(t) {
  t.plan(1);
  t.ok(true, "It's ok to plan, and also end.  Watch.");
  t.end();
});
{% endhighlight %}

Test plans help in situations where you want to put assertions inside asynchronous events.  For example, if you're testing a web application and it makes HTTP requests in the test cases, but you also intercept events that indicate various lifecycle events.  These could be things like ensuring a notification email was sent when a user signs up, and also checking that their account was saved to the database.

In Mocha, such a test might look like this:

{% highlight javascript %}
describe('Account creation', function() {
  it('should allow users to sign up', function(done) {
    app.on('notify:accounts:create', function(account) {
      assert(account, 'expected a user account object');
      done();
    });

    request(app).post('/accounts').send(userDetails).expect(200, done);
  });
});
{% endhighlight %}

That's OK, but it has some problems: `done` will be called twice -- once when the web request finishes, and again when the email event is sent (`notify:accounts:create`).

We could fix this by counting how many assertions have been called:

{% highlight javascript %}
describe('Account creation', function() {
  it('should allow users to sign up', function(done) {
    var expected = 2;

    function checkDone() {
      expected--;
      if (expected === 0) {
        done();
      }
    }

    app.on('notify:accounts:create', function(account) {
      assert(account, 'expected a user account object');
      checkDone();
    });

    request(app).post('/accounts').send(userDetails).expect(200, checkDone);
  });
});
{% endhighlight %}

Seeing `checkDone` all over my tests made me create something more generic.  In the following example I use instances of an object called `Plan` that allows assertions to be counted, and `done` to only get called once the specified number of assertions have passed.  This example can be run with the `mocha` command-line script.

{% highlight javascript %}
var assert = require('assert');

function Plan(count, done) {
  this.done = done;
  this.count = count;
}

Plan.prototype.ok = function(expression) {
  assert(expression);

  if (this.count === 0) {
    assert(false, 'Too many assertions called');
  } else {
    this.count--;
  }

  if (this.count === 0) {
    this.done();
  }
};

describe('Asynchronous example', function() {
  it('should run two asynchronous methods', function(done) {
    var plan = new Plan(2, done);

    setTimeout(function() {
      plan.ok(true);
    }, 50);

    setTimeout(function() {
      plan.ok(true);
    }, 25);
  });
});
{% endhighlight %}

This code could be expanded to tie in with Mocha's timeouts to display the number of missed assertions, if any.  Otherwise it does the job: if any of the asynchronous callbacks don't fire, Mocha will raise a timeout error.  It also protects against calling assertions too many times, which can actually happen if you're making your own asynchronous APIs: I've had cases where I've triggered callbacks twice by mistake.  And, it ensures `done` is only called when needed.

The question of ensuring assertions were actually called was brought up in this issue for Chai.js: [Asserting that assertions were made](https://github.com/chaijs/chai/issues/94).  And, the Mocha wiki has this assertion counting snippet: [Assertion counting](https://github.com/visionmedia/mocha/wiki/Assertion-counting).

Outside of Mocha, I found [QUnit has asyncTest](http://api.qunitjs.com/asyncTest/) which allows assertions to be planned like TAP-style tests.  With this approach we don't need to broker calls to `done` because it uses [start](http://api.qunitjs.com/start/) instead.

I've never quite found the perfect solution to this problem, however.  How do you ensure assertions are triggered in Mocha, and how do you handle calling `done` in tests where there are multiple asynchronous operations?
