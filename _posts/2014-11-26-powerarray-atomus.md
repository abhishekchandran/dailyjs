---
layout: post
title: "PowerArray, Atomus"
author: "Alex Young"
image: "/images/posts/atomus.png"
categories:
- array
- testing
- libraries
- modules
---

###PowerArray

[PowerArray](http://techfort.github.io/PowerArray/) (GitHub: [techfort/PowerArray](https://github.com/techfort/PowerArray), License: _BSD_) by Joe Minichino is a small library that attempts to replace native `Array` methods with faster ones.  You can use `PowerArray.prototype.forEach` to iterate over values using a simple `for` loop, which is known to be faster than `Array.prototype.forEach`.  However, it also includes `PowerArray.prototype.binarySearch` which performs a binary search on the array.

> Thanks to [Oliver Caldwell's post](http://oli.me.uk/2013/06/08/searching-javascript-arrays-with-a-binary-search/) for a quick version of the algorithm. Also note the contribution of Yehonatan and other authors of comments to the post which helped to optimise the implementation of binary search further.

Oliver wrote this about the binary search algorithm:

> A binary search searches by splitting your array into smaller and smaller chunks until it finds your desired value. Unlike the normal indexOf which searches from left to right in a simple iteration. The binary search Wikipedia article explains it best (as always). There are a couple of downsides; It will be slower with smaller data sets (this needs proving) and the array you are searching needs to be sorted.

To use the binary search you'll need to sort the array first, and there's `PowerArray.prototype.numericSort` which just uses `Array.prototype.sort` with `return a.id < b.id ? -1 : 1`.

The project includes some benchmarks so you can try it out for yourself.

###Atomus

Everytime I use a Node/DOM testing library my tests seem to suffer from bitrot and stop working after a few months.  So I was glad to see a new one by Krasimir Tsonev called Atomus (GitHub: [krasimir/atomus](https://github.com/krasimir/atomus), License: _MIT_, npm: [atomus](https://www.npmjs.org/package/atomus)).  It's based on jsdom, so you get a `window` object and browser instance that lets you trigger events like `clicked` and `blurred`.

The following snippet is taken from the bundled AngularJS test:

{% highlight javascript %}
var b = atomus()
.html('<html><body><div ng-controller="Controller"><register-form></register-form></div></body></html>')
.external(__dirname + '/data/angular.js')
.external(__dirname + '/data/angular.register-form.js')
.ready(function(errors, window) {
  if (errors !== null) console.log(errors);

  var Controller = function($scope) {
    var runTests = function() {

      var register = b.$('#register-button');
      var message = b.$('#message');
      var username = b.$('#username');
      var password = b.$('#password');

      b.clicked(register);

      assert.equal(message.text(), 'Missing username.');
{% endhighlight %}

The `b.clicked(register)` line causes the `#register-button` element to be clicked, and then there are some standard Node `assert` calls to ensure the document was updated as expected.

I've used other libraries like this, including [Zombie.js](http://zombie.labnotes.org/).  They all work in a slightly different way -- Zombie.js also uses jsdom but some use PhantomJS or drive browsers with Selenium.  It's worth trying a few out to see what works for your project.
