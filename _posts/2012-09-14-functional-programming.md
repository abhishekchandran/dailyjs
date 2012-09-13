---
layout: post
title: "Functional Programming in JavaScript"
author: "Nathaniel Smith"
categories: 
- functional
- tutorial
---

 JavaScript has two parents: Scheme and Self. We can thank Self for all of the object-orientedness of JavaScript and indeed we do in our code and our tutorials. However, Scheme played just as important a role in the language's design, and we would do ourselves ill to overlook JavaScript's functional heritage.

What exactly does it mean for JavaScript to be functional? "Functional" merely describes a collection of traits a given language may or may not have. A language like Haskell has all of them: immutable variables, pattern matching, first class functions, and others. Some languages hardly have any, like C.  While JavaScript certainly doesn't have immutable variables or pattern matching it does have a strong emphasis on first class functions; mutating, combining, and using these function objects for cleaner and more succinct code is the purpose of this tutorial.

###Partial Application

Partial application is a technique for taking a function _f_ and binding it against one or more arguments to produce a new function _g_ with those arguments applied. We'll demonstrate this operation by adding a helper function _p_ to Function's prototype.

{% highlight javascript %}
Function.prototype.p = function() {
  // capture the bound arguments
  var args = Array.prototype.slice.call(arguments);
  var f = this;
  // construct a new function
  return function() {
    // prepend argument list with the closed arguments from above
    var inner_args = Array.prototype.slice.call(arguments);
    return f.apply(this, args.concat(inner_args))
  };
};

var plus_two = function(x,y) { return x+y; };
var add_three = plus_two.p(3);
add_three(4); // 7
{% endhighlight %}

###Composition

Composition is an operation that produces a new function _z_ by nesting functions _f_ and _g_. You can think of it in this way: _z(x) == f(g(x))_.  Let's add a helper like we did for partial application.

{% highlight javascript %}
Function.prototype.c = function(g) {
  // preserve f
  var f = this;
  // construct function z
  return function() {
    var args = Array.prototype.slice.call(arguments);
    // when called, nest g's return in a call to f
    return f.call(this, g.apply(this, args));
  };
};

var greet = function(s) { return 'hi, ' + s; };
var exclaim = function(s) { return s + '!'; };
var excited_greeting = greet.c(exclaim);
excited_greeting('Pickman') // hi, Pickman!
{% endhighlight %}

###Flipping

Flipping at first seems like a scary and arbitrary thing to do to a poor Function. However, it is useful when one desires to use partial application to bind arguments other than the first. To perform a flip we take function _f_ which takes parameters _(a,b)_ and construct a function _g_ which takes parameters _(b,a)_.

{% highlight javascript %}
Function.prototype.f = function() {
  // preserve f
  var f = this;
  // construct g
  return function() {
    var args = Array.prototype.slice.call(arguments);
    // flip arguments when called
    return f.apply(this, args.reverse());
  };
};

var div = function(x,y) { return x / y; };
div(1, 2) // 0.5
div.f()(1,2) // 2
{% endhighlight %}

###Point-Free Style

Point-free programming is a style of coding that one doesn't see much outside of languages like Haskell or OCaml. However, it can help drastically reduce the use of the rather verbose function declaration syntax omnipresent in JavaScript code.  Programming in a point-free style is made possible by our helpers above, and we'll combine them to illustrate this concept.

{% highlight javascript %}
// We'll start by solving the following problem in a non point-free way.
// Produce a function which, given a list, returns the same list with
// every number made negative.

// First, declare some helpers:
var negate = function(x) { return -1 * x; };
var abs = function(x) { return Math.abs(x); };
var map = function(a, f) { return a.map(f); };
var numbers = [-1, 2, 0, -2, 3, 4, -6]

var negate_all = function(array) { return map(array, negate.c(abs)); };
negate_all(numbers); // [-1, -2, 0, -2, -3, -4, -6]

// That solves it; but we can do better:

var negate_all = map.f().p(negate.c(abs));
negate_all(numbers); // [-1, -2, 0, -2, -3, -4, -6]
{% endhighlight %}

What did we do here? First, we flipped `map`'s signature to be _(f,a)_; this allows us to then partially apply a function to map and turn it into a function that takes only a single parameter: the array we wish to negate. But what function do we want to bind to our map? The result of `negate.c(abs)`, which represents a function that does `negate(abs(x))`. We've produced the same function in the end and solved our problem. In the former attempt, we declare a new function to imperatively do what we wish; in the latter we construct a new function based on functions we already have.

What makes this point-free? Note the redundancy of the `array` argument in the former declaration. We already have a function that knows how to produce a new array from an existing one; why not convert that function into a new one to do what we want? We cut characters by 37% and, for many, achieve better readability.

###Conclusions

In the end, functional programming is a matter of taste. For some it is a thing of subtle beauty and for others a wild nest of parentheses. This tutorial is a suggestion of styles that might be and is in no way a 'Functional is better' argument. If this has piqued the reader's interest, she or he may be interested in the following resources:

* [Oliver Steele's Functional library](http://osteele.com/sources/javascript/functional/). A library which provides the above operators and much more.
* [Learn You a Haskell For Great Good](http://learnyouahaskell.com/). Doubles as a great introduction to functional programming.
* [The Little JavaScripter](http://www.crockford.com/javascript/little.html). A take on The Little Schemer by Douglas Crockford.
* [Point-free (or Tacit) Programming](http://en.wikipedia.org/wiki/Tacit_programming). From Wikipedia.
