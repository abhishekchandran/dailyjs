---
layout: post
title: "Encapsulation Breaking"
author: "Justin Naifeh"
categories: 
- encapsulation
- tutorial
---

Encapsulation is the process by which an object's internal components and behavioral details are hidden from calling code. Only that which should be exposed is exposed, making objects self-contained black boxes to the outside world. Many languages support encapsulation by supplying visibility modifiers (e.g., private) and constructs such as inner classes.

Unfortunately, JavaScript offers very little in the encapsulation department. While there are certain tricks that can wrap protected code in closures (see [Module Pattern](http://www.adequatelygood.com/2010/3/JavaScript-Module-Pattern-In-Depth)), many have disadvantages that compromise code flexibility and extensibility.

###Standard Convention

Instead of using closure-based encapsulation, which often makes object-oriented inheritance difficult, many libraries and code-bases opt to mark private properties and functions with an underscore prepend. This convention makes inspecting the properties and functions easy within browser debuggers.

{% highlight javascript %} 
var Person = function(first, last){
  // private properties _first, _last, and _id
  this._first = first;
  this._last = last;
  this._id = this._generateId();
};

Person.prototype = {
  getId : function(){
    return this._id;
  },
  getFirstName: function(){
    return this._first;
  },
  getLastName : function(){
    return this._last;
  },
  // private function to generate an id for this object
  _generateId : function(){
    return new Date().getTime().toString();
  }
};
{% endhighlight %}

This convention is commonplace, similar to naming constants in uppercase. The downside is that private properties and functions can still be accessed, thus breaking encapsulation because of a careless developer.

###Encapsulation Breaking

The dynamic nature of JavaScript allows for a free-for-all environment where a developer can do whatever he or she wants. Consider the following:

{% highlight javascript %} 
var person = new Person("Bob", "Someguy");
console.log(person._first); // logs "Bob"
{% endhighlight %}

This appears all fine and well, but now that we've coupled our code to the Person implementation. Any change to the internals -- the category of change encapsulation should protect us against -- could break calling code.

{% highlight javascript %} 
var Person = function(first, last){
  this._firstName = first; // property change
  this._lastName = last; // property change
  this._id = this._generateId();
};

// ... 
var person = new Person("Bob", "Someguy");
console.log(person._first); // logs "undefined"
{% endhighlight %}

These bugs can be difficult to track, especially since the application code may not have changed...an updated external library or resource, in which `Person` may be defined, is all that it takes. The best defense against such couplings is to avoid breaking encapsulation. If a property or method is marked as private, do not access, modify, or invoke it. The overhead in rethinking the architecture and design is almost always less than the cost of dealing with the consequences of breaking encapsulation.

In other words: "Developers don't let developers break encapsulation."

###Method Stealing

As troublesome as accessing private properties can be in JavaScript, there is another much more insidious practice that seems commonly accepted: method stealing.

The methods [Function.prototype.call](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function/call) and [Function.protoype.apply](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function/apply) are integral to modern libraries and code-bases by allowing a method to inject a custom context (*this* reference) into the execution scope. Without these capabilities the reliance on closures to achieve the same effect would be too cumbersome.

Just as some properties should be hidden, so too should some methods. Given our prior example, `Person.prototype._generateId()` might function as an inadequate [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) generator. A clever developer notices that another available method `Book.prototype._setUUID()` sets a `this._id` property on all Book objects whose value is much more unique across space and time than `Person.prototype._generateId();`

{% highlight javascript %} 
var Book = function(title, author){
  this._title = title;
  this._author = author;
  this._id = null;
  this._setUUID();
}
Book.prototype = {
  getId : function(){
    return this._id;
  },
  getTitle : function(){
    return this._title;
  },
  getAuthor : function(){
    return this._author;
  },
  _setUUID : function(){
    var result = '';
    for(var i=0; i<32; i++)
    {
      result += Math.floor(Math.random()*16).toString(16);
    } 
    this._id = result;
  }
};
{% endhighlight %}

In return, the developer has chosen to "steal" this behavior from `Book` for `Person` and modify `Person.prototype._generateId()` to invoke `Book.prototype._setUUID()`.

{% highlight javascript %} 
var Person = function(first, last){
  // private properties _first, _last, and _id
  this._first = first;
  this._last = last;
  this._id = null;
  this._generateId();
};

Person.prototype = {
  getId : function(){
    return this._id;
  },
  getFirstName: function(){
    return this._first;
  },
  getLastName : function(){
    return this._last;
  },
  // private function to generate an id for this object
  _generateId : function(){
    // sets this._id withing _setUUID()
    Book.prototype._setUUID.call(this);
  }
};
{% endhighlight %}

Again this works...ostensibly so, by having `this._id` set by `Book.prototype._setUUID()`. The design is brittle, however, because `Book`'s internals can be refactored unbeknownst to `Person`, thus breaking `Person` objects. If `Book.prototype._setUUID()` is refactored to set `this._uuid` rather than `this._id` then all `Person.prototype.getId()` invocations will return *undefined*. With one myopic decision we broke our application because it was easier to break encapsulation rather than rethink the design.

###Conclusion

There is not much of a conclusion except **do not break encapsulation**. In fact, apply the Golden Rule while coding: *treat other code as you wish yours would be treated*. Any API deficiencies should be brought to the original author, not hacked apart to make it usable for one use case or instance. The maintenance headache down the road is just not worth it.
