---
layout: post
title: "The Art of Error"
author: Alex Young
categories:
- node
- errors
---

<div class="image">
  <img src="/images/posts/iamerror.png" />
  <small>Error was originally a character in the hit video game, "Zelda".</small>
</div>

I like to define a lot of objects that inherit from `Error`.  I find it helps me to track down issues -- post-mortem -- but also to clearly handle expected errors.  Sometimes writing error handling code feels like a chore, but it shouldn't be an afterthought.  Well-designed and well-tested errors will help you maintain projects, but also help users figure out what to do when things go wrong.

When it comes to using `Error`, I've found two bad practices that should be avoided:

1. `new Error` is used instead of a subclass.
2. `Error` is avoided altogether because "exceptions are bad".

Let's look at how to avoid these issues and use errors properly.

###Subclassing Error

Subclassing errors is easy with `Object.create` or `util.inherits` (in Node).  Here's how you do it in Node:

{% highlight javascript %}
var assert = require('assert');
var util = require('util');

function NotFound(message) {
  Error.call(this);
  this.message = message;
}

util.inherits(NotFound, Error);

var error = new NotFound('/bitcoin-wallet not found');

assert(error.message);
assert(error instanceof NotFound);
assert(error instanceof Error);
assert.equal(error instanceof RangeError, false);
{% endhighlight %}

The assertions check that the expected property was set (`message`), and `error` is an instance of `NotFound`, `Error`, but _not_ `RangeError`.

If you were using this with [Express](http://expressjs.com/), you could set other properties to make the error more useful.  This is great when passing errors to `next()` in routes.  When dealing with errors at the HTTP layer, I like to include a status code:

{% highlight javascript %}
function NotFound(message) {
  Error.call(this);
  this.message = message;
  this.statusCode = 404;
}
{% endhighlight %}

Now you could have error handling middleware that handles errors in a more DRY fashion:

{% highlight javascript %}
app.use(function(err, req, res, next) {
  console.error(err.stack);

  if (!err.statusCode || err.statusCode === 500) {
    emails.error({ err: err, req: req });
  }

  res.send(err.statusCode || 500, err.message);
});
{% endhighlight %}

This will send the HTTP status code to the browser, if available.  It also only emails errors when the `statusCode` is 500 or not set.  I took this from production code that generates emails when unusual things happen, and I don't want to get notified about general errors like 401, 403, and 404.

The line that reads `console.error(err.stack)` won't actually work as expected.  In V8 platforms like Node and Chrome you can use `Error.captureStackTrace(this, arguments.callee)` in the error's constructor to get the stack trace.

{% highlight javascript %}
function NotFound(message) {
  Error.call(this);
  Error.captureStackTrace(this, arguments.callee);
  this.message = message;
  this.statusCode = 404;
}
{% endhighlight %}

When I was researching this article I noticed there's a lot of confusion about inheriting from `Error` and capturing the stack.  It's hard to do it properly in every browser.  If you want to read more, there's a good Stack Overflow post about it here: [What's a good way to extend Error in JavaScript?](http://stackoverflow.com/questions/1382107/whats-a-good-way-to-extend-error-in-javascript).

###Throwing and Catching Errors

You might have noticed I've been quiet about `throw`, and that's because we hardly ever use it anymore.  It's more common to see errors passed as the first argument to a callback, or emitted as an `'error'` event's first argument.

If you're using an API like this, you'll probably use something like `if (err) return handleError(err)` at the top of your callback.  You can also use `if (err instanceof SpecificError)` to add your own context specific error handling code.

Node developers usually avoid raising exceptions, but if you really think it's necessary you can use `throw new Error('I am Error')` and then `assert.throws` in your tests.  I find I hardly ever need to use `throw`.

###Designing Error Objects

Once you start subclassing `Error` and adding your own properties, you can cause new problems by breaking the [SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29) principles.  To keep your errors clean, ensure an error class only has one responsibility -- don't make Swiss Army knife error objects, or trigger complex behaviours inside their constructors.

You should also create errors in logical places.  If you've written a database layer, don't raise the previous `NotFound` error from something that loads data from the database.  In this case it would be better to have a `Database.NotFound` error object, or maybe just return `undefined` and then raise `NotFound` at the view layer.

Following the [Liskov substitution principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle) also helps create maintainable error handling code.  If you replace the previous `NotFound` error with a new class that has more context-specific information, then the existing code should still work.  You'd break this rule if you somehow changed what `notFound.statusCode` did.

###Conclusion

I create a lot of `Error` classes in my projects, but I rarely use `throw` and `catch`.  You should set useful properties in error objects, but use such properties consistently.  And, don't cross the streams: HTTP errors have no place in your database code.  Or for browser developers, Ajax errors have a place in code that talks to the server, but not code that processes Mustache templates.
