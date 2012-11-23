---
layout: post
title: "Blanket.js, xsdurationjs, attr"
author: Alex Young
categories: 
- libraries
- testing
- node
- browser
- dates
---

###Blanket.js

![Blanket and QUnit](/images/posts/blanket-koans.png)

[Blanket.js](http://migrii.github.com/blanket/) (GitHub: [Migrii / blanket](https://github.com/Migrii/blanket), License: _MIT_, npm: [blanket](https://npmjs.org/package/blanket)) by Alex Seville is a code coverage library tailored for Mocha and QUnit, although it should work elsewhere.  Blanket wraps around code that requires coverage, and this can be done by applying a `data-cover` attribute to script tags, or by passing it a path, regular expression, or array of paths in Node.

It actually parses and instruments code using [uglify-js](https://npmjs.org/package/uglify-js), and portions of [Esprima](http://esprima.org/) and James Halliday's [falafel](https://github.com/substack/node-falafel) library.

The author has prepared an example test suite that you can run in a browser: [backbone-koans-qunit](http://migrii.github.com/blanket/examples/backbone-koans-qunit/index.html).  Check the "Enable coverage" box, and it will run through the test suite using Blanket.js.

###xsdurationjs

[xsdurationjs](https://github.com/revington/xsdurationjs) (License: _MIT_, npm: [xsdurationjs](https://npmjs.org/package/xsdurationjs)) by Pedro Narciso García Revington is an implementation of [Adding durations to dateTimes](http://www.w3.org/TR/xmlschema-2/#adding-durations-to-dateTimes) from the W3C Recommendation _XML Schema Part 2_.  By passing it a [duration](http://www.w3.org/TR/xmlschema-2/#duration) and a date, it will return a new date by evaluating the duration expression.

The duration expressions are [ISO 8601 durations](http://en.wikipedia.org/wiki/ISO_8601#Durations) -- these can be quite short like `P5M`, or contain year, month, day, and time:

> For example, "P3Y6M4DT12H30M5S" represents a duration of "three years, six months, four days, twelve hours, thirty minutes, and five seconds".

The project includes Vows tests that include coverage for the W3C functions (`fQuotient` and `modulo`).

###attr

[attr](https://github.com/weepy/attr) (License: _MIT_) by Jonah Fox is a [component](https://github.com/component) for "evented attributes with automatic dependencies."  Once an attribute has been created with `attr('name')`, it will emit events when the value changes.  Convenience methods are also available for toggling boolean values and getting the last value.

It's designed to be used in browsers, and comes with Mocha tests.
