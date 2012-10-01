---
layout: post
title: "JavaScript for Node Part 1: Enumeration"
author: Nathan Sweet
categories:
- node
- Enumeration
- ES3
- ES5
- benchmarking
- performance
- maintainability
---

JavaScript developers have been accustomed to a very scattered and incoherent API (the DOM) for some time. As a result, some of JavaScript's most common patterns are pretty weird and unnecessary when programming for a unified and coherent API like Node. It can be easy to forget that the entire ES5 specification is available to you, but there are some standard patterns that deserve to be rethought because of ES5's newer features.

###Objects in ES5

Since no object in JavaScript can have identical same-tier keys, all objects can be thought of as being hash tables. Indeed, V8 implements a [hash function](https://github.com/v8/v8/blob/master/src/objects.cc#L3494) for object keys. This important concept did not go unnoticed in the ES5 draft and so the method `Object.keys` was created to extract the internal associative array of any object and return it as a JavaScript Array. In layman's terms, this means that `Object.keys` returns only the keys that belong to that object and NOT any properties that it may have inherited. This is a powerful and useful construct that can be utilized in Node when enumerating over an object.

###The Old Way

Chances are you have run into the following looping pattern:

{% highlight javascript %}
var key;
for (key in obj) {
  if (obj.hasOwnProperty(key))
    obj[key];
}
{% endhighlight %}

This was the only way to traverse an object in ES3 without going up an object's prototype chain.

###A Better Way

In ES5 there is a better approach.  Given that we can simply get the keys of an object and put them into an array, we can loop over an object, but only at the cost of looping over an array. First consider the following:

{% highlight javascript %}
var keys = Object.keys(obj), i, l;

for (i = 0, l = keys.length; i < l; i++)
  obj[keys[i]];
{% endhighlight %}

This is usually the fastest way of looping over an object in ES5 (at least in V8). However, this method has some drawbacks. If new variables are needed to make calculations, this approach starts to feel overly verbose. Consider the following:

{% highlight javascript %}
function calculateAngularDistanceOfObject(obj) {
  if (typeof obj !== 'object') return;
  var keys = Object.keys(obj),
    , EARTH_RADIUS = 3959
    , RADIAN_CONST = Math.PI / 180
    , deltaLat
    , deltLng
    , halfTheSquareChord
    , angularDistanceRad
    , temp
    , a, b, i, l
    ;

  for (i = 0, l = keys.length; i < l; i++) {
    temp = obj[keys[i]];
    a = temp.a;
    b = temp.b;
    deltaLat = a.subLat(b) * RADIAN_CONST;
    deltaLng = a.subLng(b) * RADIAN_CONST;
    halfTheSquareChord = Math.pow(Math.sin(deltaLat / 2), 2) + Math.pow(Math.sin(deltaLng / 2), 2) * Math.cos(a.lat * RADIAN_CONST) * Math.cos(b.lat * RADIAN_CONST);
    obj[keys[i]].angularDistance = 2 * Math.atan2(Math.sqrt(halfTheSquareChord), Math.sqrt(1 - halfTheSquareChord));
  }
}
{% endhighlight %}

###An Even Better Way

In situations like this, instead of looping over the array of keys using Array’s native `forEach` method will allow us to create a new scope for the variables we are working with. This will allow us to do our processing in a more encapsulated manner:

{% highlight javascript %}
function calculateAngularDistanceOfObject(obj) {
  if (typeof obj !== 'object') return;

  var EARTH_RADIUS = 3959
    , RADIAN_CONST = Math.PI / 180;

  Object.keys(obj).forEach(function(key) {
    var temp = obj[key]
      , a = temp.a
      , b = temp.b
      , deltaLat = a.subLat(b) * RADIAN_CONST
      , deltaLng = a.subLng(b) * RADIAN_CONST;

    halfTheSquareChord = Math.pow(Math.sin(deltaLat / 2), 2) + Math.pow(Math.sin(deltaLng / 2), 2) * Math.cos(a.lat * RADIAN_CONST) * Math.cos(b.lat * RADIAN_CONST);
    obj[key].angularDistance =  2 * Math.atan2(Math.sqrt(halfTheSquareChord), Math.sqrt(1 - halfTheSquareChord));
  });
}
{% endhighlight %}

###Benchmarking

Choosing the right pattern depends on balancing maintainability with performance.  Of the two patterns, `forEach` is generally considered more readable.  In general, iterating over large arrays will generally perform worse with `forEach` (although better than the old ES3 way), but it's important to correctly benchmark code before making a decision.

One popular solution for Node is [node-bench](https://github.com/isaacs/node-bench) (npm: [bench](https://npmjs.org/package/bench)) written by Isaac Schlueter.  After installing it here is something to start with:

{% highlight javascript %}
var bench = require('bench')
  , obj = { zero: 0, one: 1, two: 2, three: 3, four: 4, five: 5, six: 6, seven: 7, eight: 8, nine: 9 };

// This is to simulate the object having non-enumerable properties
Object.defineProperty(obj, 'z', { value: 26, enumerable: false });

exports.compare = {
  'old way': function() {
    for (var name in obj) {
      if (obj.hasOwnProperty(name))
        obj[name];
    }
  },

  'loop array': function() {
    var keys = Object.keys(obj)
      , i
      , l;

    for (i = 0, l = keys.length; i < l; i++)
      obj[keys[i]];
  },

  'foreach loop': function() {
    Object.keys(obj).forEach(function(key) {
      obj[key];
    });
  }
};

// This is number of iterations on each test we want to run
bench.COMPARE_COUNT = 8;
bench.runMain();
{% endhighlight %}
