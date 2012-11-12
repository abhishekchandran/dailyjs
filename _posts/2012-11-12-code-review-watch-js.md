---
layout: post
title: "How Does Watch.js Work?"
author: Alex Young
categories:
- observer
- code-review
---

Last week noticed a lot of interest in [Watch.js](https://github.com/melanke/Watch.JS) (License: _MIT_) by Gil Lopes Bueno, so I thought it would be interesting to take a look at how it works.  It allows changes to properties on objects to be observed -- whenever a change is made, a callback receives the new and old values, as well as the property name:

{% highlight javascript %}
var ex1 = {
  attr1: 'initial value of attr1'
, attr2: 'initial value of attr2'
};

ex1.watch('attr1', function() {
  alert('attr1 changed');
});
{% endhighlight %}

The `watch` method can also accept an array of property names, and omitting it will cause the callback to run whenever any property changes.  The `unwatch` method will remove a watcher.

First, let's get the elephant out of the room: this implementation modifies `Object.prototype` -- that's where the `watch` method comes from in the previous example.  The author [is planning to change the API](https://github.com/melanke/Watch.JS/issues/12) to avoid modifying `Object.prototype`.

Second, this method is polymorphic in that it behaves differently based on the supplied arguments.  This is quite common in client-side code.  It's implemented by looking at the number of arguments without requiring too much type checking, in [watch](https://github.com/melanke/Watch.JS/blob/52a89a0cae3f791f00868fc4a134e84b7fa084af/src/watch.js#L61-70):

{% highlight javascript %}
WatchJS.defineProp(Object.prototype, "watch", function() {

    if (arguments.length == 1) 
        this.watchAll.apply(this, arguments);
    else if (WatchJS.isArray(arguments[0])) 
        this.watchMany.apply(this, arguments);
    else
        this.watchOne.apply(this, arguments);

});
{% endhighlight %}

You're probably wondering what [WatchJS.defineProp](https://github.com/melanke/Watch.JS/blob/52a89a0cae3f791f00868fc4a134e84b7fa084af/src/watch.js#L47-58) is.  It's actually a convenience method to use ES5's `Object.defineProperty` in browsers that support it:

{% highlight javascript %}
defineProp: function(obj, propName, value){
    try{
        Object.defineProperty(obj, propName, {
                enumerable: false
            , configurable: true
            , writable: false
            , value: value
            });
    }catch(error){
        obj[propName] = value;
    }
}
{% endhighlight %}

The `watchMany` method uses a utility method, `WatchJS.isArray`, to determine how to loop over the supplied arguments, calling `watchOne` on each in turn.  The `watchAll` method calls `watchMany`, so there's a lot of internal code reuse.

Most of the work gets carried out by [watchOne](https://github.com/melanke/Watch.JS/blob/52a89a0cae3f791f00868fc4a134e84b7fa084af/src/watch.js#L111-161).  This calls `WatchJS.defineGetAndSet(obj, prop, getter, setter)` with a custom getter and setter to wrap around values so they can be watched.  However, watching values change has a few complications.

For one thing, arrays have [mutator methods](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Array#Mutator_methods) like `push` and `pop`.  Therefore, `watchFunctions` is called to wrap each of these methods with a suitable call to `WatchJS.defineProp`.  Also, when a property is set to a new value, all of these wrapped methods will be lost.  To get around this, the custom setter calls `obj.watchFunctions(prop)` again.

When a value has changed, `callWatchers` is called.  An internal list of watcher callbacks indexed on property names is maintained and called by a for-in loop.  It's important to note that these callbacks only run if the values are actually different.  This is tested by calling `JSON.stringify(oldval) != JSON.stringify(newval)` -- presumably the author used this approach because it's an easy way to compare the value of objects.  I'd consider benchmarking this against other solutions.

Finally, we get to `WatchJS.defineGetAndSet`, which attempts to use `Object.defineProperty` if available, otherwise `Object.prototype.__defineGetter__.call` and `Object.prototype.__defineSetter__.call` are used.

###Conclusion

Rather than using exceptions to track browser support, it might be better to use capability testing to check for `Object.defineProperty` and `Object.prototype.__defineGetter__.call` when the first call is made, then cache the result.  As noted in the project's issues, [Object.observe](http://wiki.ecmascript.org/doku.php?id=harmony:observe) should provide a more efficient approach in the future -- this is an accepted Harmony proposal.

To really mature this project, changing the API to avoid modifying `Object.prototype` would be a good idea, and adding benchmarks and unit tests would be useful as well.

This article was based on [watch.js commit dc9aac6a6e](https://github.com/melanke/Watch.JS/blob/52a89a0cae3f791f00868fc4a134e84b7fa084af/src/watch.js).
