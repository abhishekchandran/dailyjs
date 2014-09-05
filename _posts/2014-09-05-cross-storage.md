---
layout: post
title: "Cross-Storage: Share Local Data Across Domains"
author: "Alex Young"
categories:
- localStorage
- es6
---

![Cross-Storage](/images/posts/crossstorage.png)

The [localStorage API](http://diveintohtml5.info/storage.html) has some limitations, which you may need to work around for larger applications.  The new [cross-storage](https://github.com/zendesk/cross-storage) (License: _Apache 2.0_, npm: [cross-storage](https://www.npmjs.org/package/cross-storage), Bower: `cross-storage`) library from Daniel St. Jules at Zendesk adds support for cross-domain localStorage with permissions.  It even has an ES6 Promise API.

It uses two components: hubs and clients.  Hubs can set permissions based on on domain, and this is enforced using the same-origin policy.  The available types of access are read, write, and delete (`get`, `set`, `del`).

{% highlight javascript %}
CrossStorageHub.init([
  { origin: /\.example.com$/, allow: ['get'] },
  { origin: /:(www\.)?example.com$/, allow: ['get', 'set', 'del'] }
]);
{% endhighlight %}

Clients can then access the hub like this:

{% highlight javascript %}
var storage = new CrossStorageClient('https://store.example.com/hub.html');

storage.onConnect().then(function() {
  // Set a key with a TTL of 90 seconds
  return storage.set('newKey', 'foobar', 90000);
}).then(function() {
  return storage.get('existingKey', 'newKey');
}).then(function(res) {
  console.log(res.length); // 2
}).catch(function(err) {
  // Handle error
});
{% endhighlight %}

Notice that the `onConnect` method returns a promise which is fulfilled when a connection has been established with the hub.  You could also call `storage.close` to end the connection, which is actually implemented with an `iframe`.

Daniel recommends using the [es6-promise](https://github.com/jakearchibald/es6-promise) polyfill for older browsers.

The project uses Gulp to build the client-side code, and comes with tests that use [zuul](https://github.com/defunctzombie/zuul).
