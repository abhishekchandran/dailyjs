---
layout: post
title: "V8 Optimization Killers"
author: "Alex Young"
categories:
- node
- v8
- performance
---

[Bluebird](https://github.com/petkaantonov/bluebird) gets a lot of respect for its performance and API style, and reading [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers) on the Bluebird wiki reinforced my own inclination to use it over the dozens of other competent promise libraries.

Dug up by [diggan on Hacker News](https://news.ycombinator.com/item?id=7943303), this wiki page explores some ways seemingly innocent JavaScript can cause V8 to avoid optimisation.  It contains a code sample that allows you to detect if a function has been optimised, which I've been playing with:

{% highlight javascript %}
// Function that contains the pattern to be inspected (using with statement)
function codeToTest(a, b) {
  if (arguments.length < 2) b = 5;
}

function printStatus(fn) {
  switch(%GetOptimizationStatus(fn)) {
    case 1: console.log('Function is optimized'); break;
    case 2: console.log('Function is not optimized'); break;
    case 3: console.log('Function is always optimized'); break;
    case 4: console.log('Function is never optimized'); break;
    case 6: console.log('Function is maybe deoptimized'); break;
  }
}

// Fill type-info
codeToTest(1, 2);

%OptimizeFunctionOnNextCall(codeToTest);
// The next call
codeToTest(1, 2);

// Check
printStatus(codeToTest);
{% endhighlight %}

`%OptimizeFunctionOnNextCall` causes V8 to to check if a function can be optimised, and then marks it for optimisation.  Running it and then calling `%GetOptimizationStatus` will get debugger information so you can see if a given function can be optimised.

To run this example, the Bluebird wiki suggests using the following Node options:

{% highlight text %}
node --trace_opt --trace_deopt --allow-natives-syntax test.js
{% endhighlight %}

The `--trace_opt` option logs the names of optimised functions, and `--trace_deopt` logs "deoptimisations".  The `--allow-natives-syntax` option allows you to use the V8 functions that start with a percent, like `%OptimizeFunctionOnNextCall`.

If this all sounds interesting but you're focused on client-side development, then you might like to look at the [Web Tracing Framework](http://google.github.io/tracing-framework/index.html) from Google.  It can use some of V8's extra tracing options, and has both Chrome and Firefox extensions with rich instrumentation features.  You'll need to [enable some flags](http://google.github.io/tracing-framework/advanced-features.html#chrome-flags) to use it.
