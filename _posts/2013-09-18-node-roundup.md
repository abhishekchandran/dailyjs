---
layout: post
title: "Node Roundup: Bedecked, Knockout.sync.js, express-promise"
author: "Alex Young"
categories: 
- node
- modules
- npm
- apps
- express
- knockout
- mvc
---

###Bedecked

Who wants to write presentations in Keynote or PowerPoint?  No one!  That's why Justin Russell made Bedecked (GitHub: [jtrussell / bedecked](https://github.com/jtrussell/bedecked), License: _MIT_, npm: [bedecked](https://npmjs.org/package/bedecked)):

> A small module for quickly and simply authoring snazzy presentations in Markdown - or Jade, or vanilla HTML. Inspired by hackynote (thiagofelix/hackynote), Bedecked splits your Markdown into slides and spits them out as a single html file that you can share with Dropbox, S3, or whatever you like.

The command-line tool allows you to transform Markdown files into presentations.  It uses `stdout`, so you can redirect the output into a `.html` file.

It can also run as a server which supports live reloading.

###Knockout.sync.js

Knockout.sync.js (GitHub: [imrefazekas / knockout.sync.js](https://github.com/imrefazekas/knockout.sync.js), License: _MIT_, npm: [knockout.sync.js](https://npmjs.org/package/knockout.sync.js)) by Imre Fazekas adds syncing to [Knockout](http://knockoutjs.com/), supported by a Node server.  This allows data to be persisted to a server and shared between clients as desired.

Timestamps can be used to allow clients to respond to outdated data, and Socket.IO is used in the client.

###express-promise

express-promise (GitHub: [luin / express-promise](https://github.com/luin/express-promise), License: _MIT_, npm: [express-promise](https://npmjs.org/package/express-promise)) by Zihua Li is middleware for folding repetitive asynchronous operations into leaner synchronous-style operations.

This is the kind of thing you're probably used to writing:

{% highlight javascript %}
app.get('/users/:userId', function(req, res) {
  User.find(req.params.userId).then(function(user) {
    Project.getMemo(req.params.userId).then(function(memo) {
      res.json({ user: user, memo: memo });
    });
  });
});
{% endhighlight %}

But with express-promise you can do this:

{% highlight javascript %}
app.use(require('express-promise')());

app.get('/users/:userId', function(req, res) {
  res.json({
    user: User.find(req.params.userId),
    memo: Project.getMemo(req.params.userId)
  });
});
{% endhighlight %}

The readme has more documentation, with examples for Mongoose and Sequelize.


