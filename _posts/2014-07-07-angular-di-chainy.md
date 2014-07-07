---
layout: post
title: "Registering Angular.js Components, ChainyJS"
author: "Alex Young"
categories:
- angularjs
- articles
- modules
- libraries
- data
- flow-control
---

### Registering Angular.js Components

In [Registering Angular.js Components without Hassle](https://medium.com/@bestander_nz/registering-angular-js-components-without-a-hassle-e8b371330348), Konstantin Raev discusses a way to automate component registration in AngularJS.  The solution is based around Require.js and gulp.js, and he even has examples in TypeScript.

It goes against AngularJS's design a little bit, but the author is obviously experienced with inversion of control containers so he's adopted an approach that might be more familiar to Java or C# developers.

###ChainyJS

[ChainyJS](https://github.com/chainyjs/chainy/wiki) (GitHub: [chainyjs / chainy](https://github.com/chainyjs/chainy), License: _MIT_, npm: [chainy](https://www.npmjs.org/package/chainy)) is a library for handling data in a similar way to jQuery's DOM API.  The author has published [an introductory talk](https://www.youtube.com/watch?v=anr0heaHXcE), and the GitHub wiki has documentation for each of the main features.

Chainy supports some built-in data flow actions: `set`, `action`, `done`, and `map`.  You can use them like this:

{% highlight javascript %}
require('chainy').create().require('set map')
  // Set the chain's data to an array of two items
  .set(['some', 'data'])
  .map(function(itemValue) {
    // Capitalize each item
    return itemValue.toUpperCase();
  })
  .action(function(currentChainValue) {
    // Join the chain's data and add an exclamation
    return currentChainValue.join(' ') + '!';
  })
  // Handle an error (if applicable), and log the output
  .done(function(err, resultChainValue) {
    if (err) throw err;
    console.log('result:', resultChainValue);
  });
{% endhighlight %}

The `map` and `action` methods can be asynchronous -- just include an extra argument to get a callback.

The `map` method is actually a plugin.  [Plugins are extensions](https://github.com/chainyjs/chainy/wiki/Plugins) that extend API calls.  You can bundle plugins using the Chainy command-line tool, and npm `peerDependencies` can be used as well.
