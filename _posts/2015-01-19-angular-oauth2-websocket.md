---
layout: post
title: "angular-oauth2, angular-websocket"
author: Alex Young
categories:
- angular
- authentication
- websockets
- browser
- libraries
- modules
---

###angular-oauth2

angular-oauth2 (GitHub: [seegno/angular-oauth2](https://github.com/seegno/angular-oauth2), License: _MIT_, npm: [angular-oauth2](https://www.npmjs.com/package/angular-oauth2), Bower: `angular-oauth2`) by Rui Silva at Seegno is an AngularJS OAuth2 client module that uses ES6 internally.  The author has kindly released it on npm and Bower, so it should be easy to quickly try it out.

To use it, you have to configure `OAuthProvider` with the server's base URL, and then the client ID and secret.  Then you can request access and refresh tokens as required.  The error handling is nice because you can hook into error events on `$rootScope.$on('oauth:error'`.

I've written a few browser extensions that use OAuth, and this seems ideal for that kind of work.  It will also be useful for your Angular single page web apps.

###angular-websocket

PatrickJS (Patrick Stapleton) sent in angular-websocket (GitHub: [gdi2290/angular-websocket](https://github.com/gdi2290/angular-websocket), License: _MIT_, npm: [angular-websocket](https://www.npmjs.com/package/angular-websocket), Bower: `angular-websocket`), which is a WebSocket library for AngularJS 1.x.  It works by providing a factory, `$websocket`, that you can use to stream data between the server and your Angular app.

The API is modeled around the standard WebSocket API:

{% highlight javascript %}
angular.module('YOUR_APP', [
  'ngWebSocket' // you may also use 'angular-websocket' if you prefer
])
//                          WebSocket works as well
.factory('MyData', function($websocket) {
  // Open a WebSocket connection
  var dataStream = $websocket('wss://website.com/data');

  var collection = [];

  dataStream.onMessage(function(message.data) {
    collection.push(JSON.parse(message.data));
  });

  var methods = {
    collection: collection,
    get: function() {
      dataStream.send(JSON.stringify({ action: 'get' }));
    }
  };

  return methods;
})
.controller('SomeController', function(MyData) {
  $scope.MyData = MyData;
});
{% endhighlight %}

In this example you would use `MyData` in the corresponding markup.  Patrick's example uses `ng-repeat` to iterate over the data.

The project includes browser tests and a build script.  It doesn't have any fallback for browsers that don't support WebSockets, so it's a pure WebSocket module rather than something like Socket.IO.
