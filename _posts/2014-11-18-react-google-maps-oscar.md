---
layout: post
title: "React Google Maps, TypeScript Tests"
author: "Alex Young"
image: "/images/posts/reactgooglemaps.png"
categories:
- libraries
- testing
- typescript
- google-maps
- react
---

###React Google Maps

![React Google Maps](/images/posts/reactgooglemaps.png)

[React Google Maps](http://tomchentw.github.io/react-google-maps/) (GitHub: [tomchentw/react-google-maps](https://github.com/tomchentw/react-google-maps), License: _MIT_, Bower: _react-google-maps_, npm: [react-google-maps](https://www.npmjs.org/package/react-google-maps)) by Tom Chen is a React component for creating Google Maps.  It has a mixin called `GoogleMapsMixin` that you can use to create React components for your own maps.

Tom has posted some examples that demonstrate things like [click events](http://tomchentw.github.io/react-google-maps/#events/simple-click-event) and [geolocation](http://tomchentw.github.io/react-google-maps/#basics/geolocation).  These examples are based on Google's developer documentation so you can see how React compares to the original Google APIs.

###TypeScript Data Structures and Tests

Adrien Cadet sent in some TypeScript projects: [Ludivine](http://ludivine.adriencadet.com/), a TypeScript data structure library, and [Oscar](http://oscar.adriencadet.com/), a test harness.

[Ludivine has a wiki](https://github.com/acadet/ludivine/wiki) that describes each of the interfaces and classes.  For example, [LinkedList](https://github.com/acadet/ludivine/wiki/LinkedList) inherits from several interfaces to implement a linked version of [IList](https://github.com/acadet/ludivine/wiki/IList).

[Oscar has a getting started guide](https://github.com/acadet/oscar/wiki/Get-started) that explains how to create tests and test suites:

{% highlight text %}
class MyTestClass extends UnitTestClass {
    firstTest() : void {
        // ... AAA stuff
    }

    secondTest() : void {
        // ... another AAA stuff
    }
}
{% endhighlight %}

This example is for testing a class called `UnitTestClass`.  Each method that ends in `Test` will be run by the test suite runner.
