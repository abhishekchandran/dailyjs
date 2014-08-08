---
layout: post
title: "Face Tracking, tcomb"
author: "Alex Young"
categories:
- graphics
- webcam
---

###JavaScript Face Tracking

Konrad Dzwinel sent in a [JavaScript Face Tracking Demo](https://kdzwinel.github.io/JS-face-tracking-demo/) that demonstrates how to use `getUserMedia` with [tracking.js](https://github.com/eduardolundgren/tracking.js) to track your face and add an image based on the position.  It also uses [gif.js](https://github.com/jnordberg/gif.js) to generate GIFs, and Imgur's API to upload the images.

Konrad made a [video](https://www.youtube.com/watch?v=bC7uALxKDg8&feature=youtu.be) about the project with more details about each of the libraries and how you can use them.

###tcomb

[tcomb](http://gcanti.github.io/tcomb/) (GitHub: [gcanti / tcomb](https://github.com/gcanti/tcomb), License: _MIT_, npm: [tcomb](https://www.npmjs.org/package/tcomb)) by Giulio Canti is a library for making types and combinators.  You can use it for validating input or perhaps even lightweight models.

It supports JavaScript primitive type checking, structs, unions, tuples, and subtypes.  This is an example of a struct:

{% highlight javascript %}
var Product = struct({
  name: Str,                  // a REQUIRED string
  description: maybe(Str),    // an OPTIONAL string (can be `null`)
  homepage: Url,              // a SUBTYPE of string representing an URL
  shippings: list(Shipping),  // a LIST of shipping methods
  category: Category,         // a string in [Audio, Video] (ENUM)
  price: union(Num, Price),   // price expressed in dollars OR in another currency (UNION)
  dim: tuple([Num, Num])      // width x height (TUPLE)
});
{% endhighlight %}

The project is tested with Mocha, and the readme and homepage have lots of examples.
