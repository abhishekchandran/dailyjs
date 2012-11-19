---
layout: post
title: "Mastering Node Streams: Part 2"
author: "Roly Fentanes"
categories: 
- tutorials
- node
- streams
---

<div class="intro">Part 1: <a href="http://dailyjs.com/2012/09/10/streams/">Mastering Node Streams</a>.</div>

If you've ever used the [Request](https://github.com/mikeal/request) module, you've probably noticed that calling it returns a stream object synchronously. You can pipe it right away. To see what I mean, this is how you would normally pipe HTTP responses:

{% highlight javascript %}
var http = require('http');

http.get('http://www.google.com', function onResponse(response) {
  response.pipe(destinationStream);
});
{% endhighlight %}

Compare that example to using the Request module:

{% highlight javascript %}
var request = require('request');

request('http://www.google.com').pipe(destinationStream);
{% endhighlight %}

That's easier to understand, shorter, and requires one less level of indentation. In this article, I'll explain how this is done so you can make modules that work this way.

### How to do It

First, it's vitally important to understand how the stream API works. If you haven't done so yet, take a look at the [stream API docs](http://nodejs.org/api/stream.html), I promise it's not too long.

First, we'll take a look at readable streams. Readable streams can be `paused()`d and `resume()`d. If we're using another object to temporarily represent it while it's not available, the reasonable thing to do would be to keep a `paused` property on this object, updated properly as `pause()` and `resume()` are called. Some readable streams also have `destroy()` and `setEncoding()`. Again, the first thing that might come to mind is to keep the properties `destroyed` and `encoding` on the temporary stream.

But, not all readable streams are created equal, some might have more methods or they might not have a `destroy()` method. The most reliable method I've found is to look at the stream's prototype, iterate through the functions including those it inherits, and buffer all calls to them until the real stream is available. This works for a writable stream's `write()` and `end()` methods, and for even emitter methods such as `on()`.

Standard stream methods don't return anything, except for `write()` which returns `false` if the write buffer is full. In this case it will be `false` as long as the real stream is not yet available.

Another special case is `pipe()`. Every readable stream's pipe method [works the same way][1]. It doesn't need to be overwritten or queued. When `pipe()` is called, it listens for events from both the source and destination streams. It writes to the destination stream whenever `data` is emitted from the source, and it pauses and resumes the source as needed. We're already queueing calls to methods inherited from event emitter.

[1]: https://github.com/joyent/node/blob/master/lib/stream.js#L33 "pipe insides"

What about emitting an event before the real source stream is available? You couldn't do this if you queued calls to `emit()`. The events would fire only after the real stream becomes available. If you're a perfectionist, you would want to consider this very rare case and come up with a solution.

### Introducing Streamify

[Streamify](https://github.com/fent/node-streamify) does all of this for you, so you don't have to deal with the complexities and still get the benefits of a nicer API. Our previous http example can be rewritten to work like Request does.

{% highlight javascript %}
var http = require('http');
var streamify = require('streamify');

var stream = streamify();
http.get('http://www.google.com', function onResponse(response) {
  stream.resolve(response);
});

// `stream` can be piped already
stream.pipe(destinationStream);
{% endhighlight %}

You might think this is unnecessary since Request already exists and it already does this. Keep in mind Request is only one module which handles one type of stream. This can be used with any type of stream which is not immediately available in the current event loop iteration.

You could even do something crazy like this:

{% highlight javascript %}
var http = require('http');
var fs = require('fs');
var streamify = require('streamify');

function uploadToFirstClient() {
  var stream = streamify({ superCtor: http.ServerResponse });

  var server = http.createServer(function onRequest(request, response) {
    response.writeHead(200);
    stream.resolve(response);
  }).listen(3000);

  stream.on('pipe', function onpipe(source) {
    source.on('end', server.close.bind(server));
  });

  return stream;
}

fs.createReadStream('/path/to/myfile').pipe(uploadToFirstClient);
{% endhighlight %}

In the previous example I used Node's standard HTTP module, but it could easily be replaced with Request -- Streamify works fine with Request.

Streamify also helps when you need to make several requests before the stream you actually want is available:

{% highlight javascript %}
var request = require('request');
var streamify = require('streamify');

module.exports = function myModule() {
  var stream = streamify();

  request.get('http://somesite.com/authenticate', function onAuthenticate(err, response) {
    if (err) return stream.emit('error', err);
    
    var options = { uri: 'http://somesite.com/listmyfiles', json: true };
    request.get(options, function onList(err, result) {
      if (err) return stream.emit('error', err);
      stream.resolve(request.get('http://somesite.com/download/' + result.file));
    });
  });

  return stream;
};
{% endhighlight %}

This works wonders for any use case in which we want to work with a stream that will be around in the future, but is preceded by one or many asynchronous operations.

![streamland](/images/posts/streamcannon.gif)
