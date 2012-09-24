---
layout: post
title: "Linking the Hash Map"
author: "Justin Naifeh"
categories: 
- tutorials
- data structures
- linked hash map
---

###The Hashmap

The [hash map](https://en.wikipedia.org/wiki/Hashmap) is a classic and indispensable data structure in application programming. It is so ubiquitous that almost every modern language supports it either with a library, or by baking the functionality into the syntax itself. Hash maps are often implemented as an [associative array](http://www.quirksmode.org/js/associative.html).

A hash map provides constant-time access to a value via a unique key. The most common methodology in JavaScript is to use an object literal as a hash map.

{% highlight javascript %}
var map = {};

// dot notation
map.foo = "bar";
console.log(map.foo); // "bar"

// bracket notation
map["foo"] = "bar";
console.log(map["foo"]); // "bar"

// mix and match
map.foo = "bar";
console.log(map["foo"]); // "bar"
{% endhighlight %}

In this example, the string `"bar"` is the value assigned to the object property `foo`. Notice that treating an object literal like a hash map is the same syntax as normal property access and manipulation; we can leverage the language itself as a data structure. Because there isn't native hash code support in JavaScript, the `Object.prototype.toString()` method is invoked on the key to create the property name.

{% highlight javascript %}
var map = {};
  
map[1] = "one";
console.log(map[1] === "one"); // true
console.log(map["1"] === "one"); // true
console.log(map[(1).toString()] === "one"); // true
{% endhighlight %}

While object literals suffice for basic hash map uses like caching, there are many operations that require boilerplate code such as listing all values in a hash map:

{% highlight javascript %} 
var map = {};

map["key1"] = "one";
map["key2"] = "two";
map["key3"] = "three";

// get all values
var values = [];
for (var key in map) {
  if (map.hasOwnProperty(key)) {
    values.push(map[key]);
  }
}

// the key order is not guaranteed with a basic hash map
// and each browser might have different implementations
console.log(values.join(',')); // "two,three,one"
{% endhighlight %}

To rescue ourselves from reinventing the wheel, it is advisable to use a hash map class that encapsulates the behavior. The  details of implementation is beyond the scope of this article, but there are many open-source libraries and articles that are worth perusing for details. For this article, we will use the following rudimentary hash map class:

![Hash Map](/images/posts/lhm-hashmap.png)

{% highlight javascript %}
/**
 * Simple hash map class.
 */
var HashMap = function() {
  this._size = 0;
  this._map = {};
};

HashMap.prototype = {

  /**
   * Puts the key/value pair into the map, overwriting
   * any existing entry.
   */
  put: function(key, value) {
    if (!this.containsKey(key)) {
      this._size++;
    }
    this._map[key] = value;
  },
  
  /**
   * Removes the entry associated with the key
   * and returns the removed value.
   */
  remove: function(key) {
    if (this.containsKey(key)) {
      this._size--;
      var value = this._map[key];
      delete this._map[key];
      return value;
    } else {
      return null;
    }
  },
  
  /**
   * Checks if this map contains the given key.
   */
  containsKey: function(key) {
    return this._map.hasOwnProperty(key);
  },
  
  /**
   * Checks if this map contains the given value.
   * Note that values are not required to be unique.
   */
  containsValue: function(value) {
    for (var key in this._map) {
      if (this._map.hasOwnProperty(key)) {
        if (this._map[key] === value) {
          return true;
        }
      }
    }

    return false;
  },
  
  /**
   * Returns the value associated with the given key.
   */
  get: function(key) {
    return this.containsKey(key) ? this._map[key] : null;
  },
  
  /**
   * Clears all entries from the map.
   */
  clear: function() {
    this._size = 0;
    this._map = {};
  },
  
  /**
   * Returns an array of all keys in the map.
   */
  keys: function() {
    var keys = [];
    for (var key in this._map) {
      if (this._map.hasOwnProperty(key)) {
        keys.push(key);
      }
    }
    return keys;
  },
  
  /**
   * Returns an array of all values in the map.
   */
  values: function() {
    var values = [];
    for (var key in this._map) {
      if (this._map.hasOwnProperty(key)) {
        values.push(this._map[key]);
      }
    }
    return values;
  },
  
  /**
   * Returns the size of the map, which is
   * the number of keys.
   */
  size: function() {
    return this._size;
  }
};
{% endhighlight %}

This `HashMap` class lacks advanced features, but it is simple, effective, and library-agnostic.

###Insertion Order

Even a robust and well tested hash map has one shortcoming if it relies on an object literal backbone: the return order of `HashMap.keys()` or `HashMap.values()` is unpredictable, meaning insertion order is not preserved. The overhead of tracking insertion order is why most hash map implementations ignore such a requirement and do not guarantee return order.

Although insertion order seems trivial, there are many cases in which it is critical to use hash maps for constant time access while also tracking when key/value pairs were inserted into the map. For example, a user interface library might allow a developer to add widgets to a dashboard.

![Composition](/images/posts/lhm-composition.png)

`Widget` objects are added to a `Dashboard`, and when a `Dashboard` is rendered, so too are all of its `Widget` children in a predictable order. This is to avoid having a dashboard's widgets randomly allocated to different layout slots per render.

{% highlight javascript %}
var dashboard = new Dashboard();
dashboard.add(new Calendar("myCalendar"));
dashboard.add(new StockTicker("myStockTicker"));
dashboard.add(new Twitter("myTwitter"));

// modify the Calendar before rendering
var calendar = dashboard.getWidget("myCalendar");
calendar.setTimeZone("MST");

// render the dashboard and its widgets in order: Calendar, StockTicker, Twitter
dashboard.render();
{% endhighlight %}

We access the `Calendar` object--and other `Widget` objects--by its unique id, with `Dashboard.getWidget()` internally delegating to a private hash map. This introduces an implementation problem: we want to preserve the widget insertion order but give the developer constant time access to its `Widget` children. A common solution is to maintain two data structures within the `Dashboard` by synchronizing a hash map for access and an `Array` for order.

![Dashboard](/images/posts/lhm-dashboard.png)

The code to ensure consistency and integrity between the two structures is non-trivial and not reusable, hence it is not ideal. Another solution is to abandon the hash map and rely solely on an `Array`, but this will slow `Widget` access time to a crawling *O(n)*, which is also unacceptable.

Enter the linked hash map.

A linked hash map is a specialized hash map that is synchronized with a [doubly linked list](https://en.wikipedia.org/wiki/Doubly_linked_list). We can merge these two data structures into a new class called `LinkedHashMap`, which allows constant time access backed by a doubly linked list to preserve insertion order. There is minimal overhead to synchronize the two structures when performing write operations on the core hash map. By extending the `HashMap` class we can add an optimized doubly linked list to track the keys. (If the hash map cannot be subclassed then consider [decorating](https://en.wikipedia.org/wiki/Decorator_pattern) it or rolling your own if there are application-specific or critical optimization requirements.)

![LinkedHashMap](/images/posts/lhm-linkedhashmap.png)

{% highlight javascript %}
/**
 * Constructor that initializes the parent HashMap
 * and the doubly linked list head and tail.
 */
var LinkedHashMap = function() {
  // invoke super constructor
  HashMap.apply(this, arguments);

  // "inner" Entry class
  this._Entry = function(value) {
    this.prev = null;
    this.head = null;
    this.value = value;
  };

  // doubly linkedlist instance variables
  this._head = this._tail = null;
};

// extend HashMap and overwrite the necessary functions
var temp = function() {};
temp.prototype = HashMap.prototype;
LinkedHashMap.prototype = new temp();

/**
 * Puts the key/value pair in the HashMap and records
 * the insertion record if it does not exist.
 * 
 * @override HashMap.put()
 */
LinkedHashMap.prototype.put = function(key, value) {
  var entry = new this._Entry(key);

  if (!this.containsKey(key)) {
    if (this.size() === 0) {
      this._head = entry;
      this._tail = entry;
    } else {
      this._tail.next = entry;
      entry.prev = this._tail;
      this._tail = entry;
    }
  }

  HashMap.prototype.put.apply(this, arguments);
};

/**
 * Removes the key/value pair from the map and 
 * the key from the insertion order.
 * 
 * @override Hashmap.remove()
 */
LinkedHashMap.prototype.remove = function(key) {
  if (this.containsKey(key)) {
    // iterate over list keys and remove the entry
    for (var cur = this._head; cur != null; cur = cur.next) {
      if (key === cur.value) {
        if (cur === this._head) {
          this._head = cur.next;
          this._head.prev = null;
        } else if (cur === this._tail) {
          this._tail = cur.prev;
          this._tail.next = null;
        } else {
          cur.prev.next = cur.next;
          cur.next.prev = cur.prev;
        }

        break;
      }
    }
  }

  return HashMap.prototype.remove.apply(this, arguments);
};

/**
 * Clears the HashMap and insertion order.
 *
 * @override HashMap.clear()
 */
LinkedHashMap.prototype.clear = function() {
  HashMap.prototype.clear.apply(this, arguments);
  this._head = this._tail = null;
};

/**
 * Returns the HashMap keys in insertion order.
 *
 * @override HashMap.keys()
 */
LinkedHashMap.prototype.keys = function() {
  var keys = [];
  for (var cur = this._head; cur != null; cur = cur.next) {
    keys.push(cur.value);
  }
  return keys;
};

/**
 * Returns the HashMap values in insertion order.
 * 
 * @override HashMap.values()
 */
LinkedHashMap.prototype.values = function() {
  var values = [];
  for (var cur = this._head; cur != null; cur = cur.next) {
    values.push(this.get(cur.value));
  }
  return values;
};
{% endhighlight %}

This new data structure, a marriage between a hash map and doubly linked list, is perfect as the sole backbone of `Dashboard` to manage widgets.

![Dashboard](/images/posts/lhm-widgets.png)

###Moving On

With just a little overhead for write operations to the `LinkedHashMap`, even basic problems that require hash map behavior can query the insertion order with ease.

{% highlight javascript %}
var map = new LinkedHashMap();

map.put("key1", "one");
map.put("key2", "two");
map.put("key3", "three");

// return order is now predictable
console.log(map.keys().join(',')); // "key1,key2,key3"
console.log(map.values().join(',')); // "one,two,three"
{% endhighlight %}

Because `LinkedHashMap` implements the same API as `HashMap` via inheritance, calling code can switch to a `LinkedHashMap` at runtime without breaking. The beauty of object-oriented design is that the declared type (`HashMap`) of a variable is irrelevant to the runtime type (`LinkedHashMap`). The only difficulty is enforcing the API in a type-unsafe language like JavaScript...but that's another article.
