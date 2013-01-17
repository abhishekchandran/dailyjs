---
layout: post
title: "Backbone.js Tutorial: Build Environment"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
---

<ul class="parts">
  <li><a href="http://dailyjs.com/2012/11/29/backbone-tutorial-1/"><strong>Part 1: Build Environment</strong></a></li>
  <li><a href="http://dailyjs.com/2012/12/06/backbone-tutorial-2/">Part 2: Google's APIs and RequireJS</a></li>
  <li><a href="http://dailyjs.com/2012/12/13/backbone-tutorial-3/">Part 3: Authenticating with OAuth2</a></li>
  <li><a href="http://dailyjs.com/2012/12/20/backbone-tutorial-4/">Part 4: Backbone.sync</a></li>
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/">Part 5: List Views</a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
</ul>

This new Backbone.js tutorial series will walk you through building a single page web application that has a customised [Backbone.sync](http://backbonejs.org/#Sync) implementation.  I started building the application that these tutorials are based on back in August, and it's been running smoothly for a few months now so I thought it was safe enough to unleash it.

<div class="image">
  <img src="/images/posts/backbone-tutorial-todo.png" alt="" />
  <small>Gmail to-do lists: not cool enough!</small>
</div>

The application itself was built to solve a need of mine: a more usable Google Mail to-do list.  The Gmail-based interface rubs me the wrong way to put it mildly, so I wrote a `Backbone.sync` method that works with Google's APIs and stuck a little [Bootstrap](http://twitter.github.com/bootstrap/) interface on top.  As part of these tutorials I'll also make a few suggestions on how to customise Bootstrap -- there's no excuse for releasing vanilla Bootstrap sites!

The app we'll be making won't feature _everything_ that Google's to-do lists support: I haven't yet added support for indenting items for example.  However, it serves my needs very well so hopefully it'll be something you'll actually want to use.

###Roadmap

Over the next few weeks I'll cover the following topics:

* Creating a new Node project for building the single page app
* Using RequireJS with Backbone.js
* Google's APIs
* Writing and running tests
* Creating the Backbone.js app itself
* Techniques for customising Bootstrap
* Deploying to Dropbox, Amazon S3, and potentially other services

###Creating a Build Environment

If your focus is on client-side scripting, then I think this will be useful to you.  Our goal is to create a development environment that can do the following:

* Allow the client-side code to be written as separate files
* Combine separate files into something suitable for deployment
* Run the app locally using separate files (to make development and debugging easier)
* Manage supporting Node modules
* Run tests
* Support Unix and Windows

To do this we'll need a few tools and libraries:

* [Node](http://nodejs.org/)
* [RequireJS](http://requirejs.org/)
* [Grunt](http://gruntjs.com/)

Make sure your system has Node installed.  The easiest way to install it is by using one of the [Node packages for your system](http://nodejs.org/download/).

###Step 1: Installing the Node Modules

Create a new directory for this project, and create a new file inside it called `package.json` that contains this JSON:

{% highlight javascript %}
{
  "name": "btask"
, "version": "0.0.1"
, "private": true
, "dependencies": {
    "requirejs": "latest"
  , "connect": "2.7.0"
  }
, "devDependencies": {
    "mocha": "latest"
  , "chai": "latest"
  , "grunt": "latest"
  , "grunt-exec": "latest"
  }
, "scripts": {
    "grunt": "node_modules/.bin/grunt"
  }
}
{% endhighlight %}

Run `npm install`.  These modules along with their dependencies will be installed in `./node_modules`.

The `private` property prevents accidentally publicly releasing this module.  This is useful for closed source commercial projects, or projects that aren't suitable for release through npm.

Even if you're not a server-side developer, managing dependencies with npm is useful because it makes it easier for other developers to work on your project.  When a new developer joins your project, they can just type `npm install` instead of figuring out what downloads to grab.

###Step 2: Local Web Server

Create a directory called `app` and a file called `app/index.html`:

{% highlight html %}
<!DOCTYPE html>
<head>
  <meta charset="utf-8">
  <title>bTask</title>
  <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
  <script type="text/javascript" src="js/lib/require.js"></script>
</head>
<body>
</body>
</html>
{% endhighlight %}

Once you've done that, create a file called `server.js` in the top-level directory:

{% highlight javascript %}
var connect = require('connect')
  , http = require('http')
  , app
  ;

app = connect()
  .use(connect.static('app'))
  .use('/js/lib/', connect.static('node_modules/requirejs/'))
  .use('/node_modules', connect.static('node_modules'))
  ;

http.createServer(app).listen(8080, function() {
  console.log('Running on http://localhost:8080');
});
{% endhighlight %}

This file uses the Connect middleware framework to act as a small web server for serving the files in `app/`.  You can add new paths to it by copying the `.use(connect.static('app'))` line and changing `app` to something else.

Notice how I've mapped the web path for `/js/lib/` to `node_modules/requirejs/` on the file system -- rather than copying RequireJS to where the client-side scripts are stored we can map it using Connect.  Later on the build scripts will copy `node_modules/requirejs/require.js` to `build/js/lib` so the `index.html` file won't have to change.  This will enable the project to run on a suitable web server, or a hosting service like Amazon S3 for static sites.

To run this Node server, type `npm start` (or `node server.js`) and visit `http://localhost:8080`.  It should display an empty page with no client-side errors.

###Step 3: Configuring RequireJS

This project will consist of [modules written in the AMD format](https://github.com/amdjs/amdjs-api/wiki/AMD).  Each Backbone collection, model, view, and so on will exist in its own file, with a list of dependencies so RequireJS can load them as needed.

RequireJS projects that work this way are usually structured around a "main" file that loads the necessary dependencies to boot up the app.  Create a file called `app/js/main.js` that contains the following skeleton RequireJS config:

{% highlight javascript %}
requirejs.config({
  baseUrl: 'js',

  paths: {
  },

  shim: {
  }
});

require(['app'],

function(App) {
  window.bTask = new App();
});
{% endhighlight %}

The part that reads `require(['app']` will load `app/js/app.js`.  Create this file with the following contents:

{% highlight javascript %}
define([], function() {
  var App = function() {
  };

  App.prototype = {
  };

  return App;
});
{% endhighlight %}

This is a module written in the AMD format -- the `define` function is provided by RequireJS and in future will contain all of the internal dependencies for the project.

To finish off this step, the `main.js` should be loaded.  Add some suitable script tags near the bottom of `app/index.html`, before the `</body>` tag.

{% highlight html %}
<script type="text/javascript" src="js/main.js"></script>
{% endhighlight %}

If you refresh `http://localhost:8080` in your browser and open the JavaScript console, you should see that `bTask` has been instantiated.

![window.bTask](/images/posts/backbone-tutorial-window.png)

###Step 4: Testing

Everything you've learned in the previous three steps can be reused to create a unit testing suite.  [Mocha](http://visionmedia.github.com/mocha/) has already been installed by npm, so let's create a suitable test harness.

Create a new directory called `test/` (next to the 'app/' directory) that contains a file called `index.html`:

{% highlight html %}
<html>
<head>
  <meta charset="utf-8">
  <title>bTask Tests</title>
  <link rel="stylesheet" href="/node_modules/mocha/mocha.css" />
  <style>
.toast-message, #main { display: none }
  </style>
</head>
<body>
  <div id="mocha"></div>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
  <script src="/node_modules/chai/chai.js"></script>
  <script src="/node_modules/mocha/mocha.js"></script>
  <script src="/js/lib/require.js"></script>
  <script src="/js/main.js"></script>
  <script src="setup.js"></script>
  <script src="app.test.js"></script>
  <script>require(['app'], function() { mocha.run(); });</script>
</body>
</html>
{% endhighlight %}

The `require` near the end just makes sure `mocha.run` only runs when `/js/app.js` has been loaded.

Create another file called `test/setup.js`:

{% highlight javascript %}
var assert = chai.assert;

mocha.setup({
  ui: 'tdd'
, globals: ['bTask']
});
{% endhighlight %}

This file makes [Chai's assertions](http://chaijs.com/api/assert/) available as `assert`, which is how I usually write my tests.  I've also told Mocha that `bTask` is an expected global variable.

With all this in place we can write a quick test.  This file goes in `test/app.test.js`:

{% highlight javascript %}
suite('App', function() {
  test('Should be present', function() {
    assert.ok(window.bTask);
  });
});
{% endhighlight %}

All it does is checks `window.bTask` has been defined -- it proves RequireJS has loaded the app.

Finally we need to update where Connect looks for files to serve. Modify 'server.js' to look like this:

{% highlight javascript %}
var connect = require('connect')
  , http = require('http')
  , app
  ;

app = connect()
  .use(connect.static('app'))
  .use('/js/lib/', connect.static('node_modules/requirejs/'))
  .use('/node_modules', connect.static('node_modules'))
  .use('/test', connect.static('test/'))
  .use('/test', connect.static('app'))
  ;

http.createServer(app).listen(8080, function() {
  console.log('Running on http://localhost:8080');
});
{% endhighlight %}

Restart the web server (from step 2), and visit `http://localhost:8080/test/` (the last slash is important).  Mocha should display that a single test has passed.

###Step 5: Making Builds

Create a file called `grunt.js` for our "gruntfile":

{% highlight javascript %}
module.exports = function(grunt) {
  grunt.loadNpmTasks('grunt-exec');

  grunt.initConfig({
    exec: {
      build: {
        command: 'node node_modules/requirejs/bin/r.js -o require-config.js'
      }
    }
  });

  grunt.registerTask('copy-require', function() {
    grunt.file.mkdir('build/js/lib');
    grunt.file.copy('node_modules/requirejs/require.js', 'build/js/lib/require.js');
  });

  grunt.registerTask('default', 'exec copy-require');
};
{% endhighlight %}

This file uses the [grunt-exec](https://github.com/jharding/grunt-exec) plugin by Jake Harding to run the RequireJS command that generates a build of everything in the `app/` directory.  To tell RequireJS what to build, create a file called `require-config.js`:

{% highlight javascript %}
({
  appDir: 'app/'
, baseUrl: 'js'
, paths: {}
, dir: 'build/'
, modules: [{ name: 'main' }]
})
{% endhighlight %}

RequireJS will minimize and concatenate the necessary files.  The other Grunt task copies the RequireJS client-side code to `build/js/lib/require.js`, because our local Connect server was mapping this for us.  Why bother?  Well, it means whenever we update RequireJS through npm the app and builds will automatically get the latest version.

To run Grunt, type `npm run-script grunt`.  The npm command `run-script` is used to invoke scripts that have been added to the `package.json` file.  The `package.json` created in step 1 contained `"grunt": "node_modules/.bin/grunt"`, which makes this work.  I prefer this to installing Grunt globally.

I wouldn't usually use Grunt for my own projects because I prefer Makefiles.  In fact, a Makefile for the above would be very simple.  However, this makes things more awkward for Windows-based developers, so I've included Grunt in an effort to support Windows.  Also, if you typically work as a client-side developer, you might find Grunt easier to understand than learning [GNU Make](http://www.gnu.org/software/make/) or writing the equivalent Node code (Node has a good file system module).

###Summary

In this tutorial you've created a Grunt and RequireJS build environment for Backbone.js projects that use Mocha for testing.  You've also seen how to use Connect to provide a convenient local web server.

This is basically how I build and manage all of my Backbone.js single page web applications.  Although we haven't written much code yet, as you'll see over the coming weeks this approach works well for using Backbone.js and RequireJS together.

The code for this project can be found here: [dailyjs-backbone-tutorial (2a8517)](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/2a8517e011a8e1041c7f86f8311336ffba7e85e8).

###Contributions

* [Tobbe Lundberg](https://github.com/Tobbe/dailyjs/commit/5d6fe8b73114adaa09e20889cdcd3ae1875c5eb4)

