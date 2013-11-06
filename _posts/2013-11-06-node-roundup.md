---
layout: post
title: "Node Roundup: Mongovi, hoquet"
author: "Alex Young"
categories: 
- node
- modules
- templating
- clojure
- mongodb
---

###Mongovi

I've been working on a project that uses MongoDB, and one of the problems I have is with Mongo's REPL.  For one thing, I keep hitting `CTRL-C` because I expect it to cancel the current line rather than exit the whole REPL, but a bigger problem for me is they've switched to [linenoise](https://github.com/antirez/linenoise).  I'm used to Vim's shortcuts, which readline can use.  When dealing with programs with non-readline REPLs, I often invoke [rlwrap](http://freecode.com/projects/rlwrap) (or write an alias to use `rlwrap`), but when it comes to Mongo a better solution might be Tim Kuijsten's Mongovi.

Mongovi (GitHub: [timkuijsten / node-mongovi](https://github.com/timkuijsten/node-mongovi), License: _MIT_, npm: [mongovi](https://npmjs.org/package/mongovi)) is a REPL for MongoDB with Vi keys.  It uses [readline-vim](https://npmjs.org/package/readline-vim) and [node-mongodb-native](http://mongodb.github.io/node-mongodb-native/), so it isn't a wrapper around the command-line `mongo` tool but instead a reimplementation in Node.

Several high-level commands work: `show dbs` lists databases, `use db` switches to a different database, and the usual commands like `db.collection.find`, `update`, and `insert` work.  The author has included Mocha tests, and documentation can be found in the readme.

###hoquet

I had a brief love affair with Clojure.  It was a romance that lasted a few months, but work got in the way and we had to break up.  However, thanks to Tom Brennan I can relive those days with hoquet (GitHub: [tjb1982 / hoquet](https://github.com/tjb1982/hoquet), License: _MIT_, npm: [hoquet](https://npmjs.org/package/hoquet)).  This is a templating library based on Clojure's Hiccup.  It uses a structured language based on arrays for generating HTML:

{% highlight javascript %}
var http = require('http'),
    h = require('hoquet');

function layout(c) {
  var out =
    ['html',
     ['head',
      ['title', c.title],
      h.styles('/css/reset.css',
               '/css/style.css'),
      c.head],
     ['body', {'ng-app':'MyApp'}, c.body]];

  return out;
}

var index = layout({
  title: 'My Page',
  body: ['div', {'ng-view':''},
         ['h1', 'Hello world']],
  head: [['meta', {'name':'description',
                   'content':'Templating'}],
         h.scripts('/js/lib/angular.min.js',
                   '/js/lib/jquery.min.js')]
});

http.createServer(function(q,s) {
  s.writeHead(200, {'Content-Type': 'text/html'});
  s.end( h.doc('html5', index) );
}).listen(8080);
{% endhighlight %}

Tom also notes that hoquet can be used in browsers, because the underlying implementation is plain ol' JavaScript:

> You create your own functions/literals to pass in whatever you want and call render, which stringifies it. You can also render inner portions at any time and insert them as Strings so you don't have to worry about when `render` is called.

