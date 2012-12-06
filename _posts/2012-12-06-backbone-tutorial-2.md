---
layout: post
title: "Backbone.js Tutorial: Google's APIs and RequireJS"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
---

<ul class="parts">
  <li><a href="http://dailyjs.com/2012/11/29/backbone-tutorial-1/">Part 1: Build Environment</a></li>
  <li><a href="http://dailyjs.com/2012/12/06/backbone-tutorial-2/">Part 2: Google's APIs and RequireJS</a></li>
</ul>

In <a href="http://dailyjs.com/2012/11/29/backbone-tutorial-1/">Part 1: Build Environment</a>, I explained how to set up a simple Node server to host your Backbone.js app and test suite.  Something that confused people was the way I used relative paths, which meant the tests could fail if you didn't visit `/test/` (`/test` won't work).  There was a reason for this: I developed the original version to run on Dropbox, so I wanted to use relative paths.  It's probably safer to use absolute paths, so I should have made this clearer.

In this part you'll learn the following:

* How `Backbone.sync` works
* How to load Backbone.js and Underscore.js with RequireJS
* How to get started with Google's APIs

###The `Backbone.sync` Method

Network access in Backbone.js is nicely abstracted through a single method which has the following signature:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
};
{% endhighlight %}

The `method` argument contains a string that can be one of the following values:

* `create`
* `update`
* `delete`
* `read`

Internally, Backbone.js maps these method names to HTTP verbs:

{% highlight javascript %}
var methodMap = {
  'create': 'POST',
  'update': 'PUT',
  'delete': 'DELETE',
  'read':   'GET'
};
{% endhighlight %}

If you're familiar with that particular flavour of RESTful API then this should all look familiar.

The second argument, `model`, is a `Backbone.Model` or `Backbone.Collection` -- collections are used when reading multiple values.

The final argument, `options`, is an object that contains success and error callbacks.  It's ultimately handed off to the jQuery Ajax API.

To work with Google's APIs we need to write our own `Backbone.sync` method.  In general terms our implementation should be structured like this:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
  switch (method) {
    case 'create':
      googleAPI.create(model, options);
    break;

    case 'update':
      googleAPI.update(model, options);
    break;

    case 'delete':
      googleAPI.destroy(model, options);
    break;

    case 'read':
      // The model value is a collection in this case
      googleAPI.list(model, options);
    break;

    default:
      // Something probably went wrong
      console.error('Unknown method:', method);
    break;
  }
};
{% endhighlight %}

The `googleAPI` object is fictitious, but this is basically how `Backbone.sync` is usually extended -- a lightweight wrapper that maps the method names and models to another API.  Using a lightweight wrapper means the underlying target API can be easily used outside of a Backbone.js.

In our case, Google actually provides a JavaScript API -- there will be a `gapi.client` object available once the Google APIs have been loaded.

###Setting Up A Google API Account

The main page for Google's developer documentation is at [developers.google.com](https://developers.google.com/), but what we're interested in is the [Google Tasks API](https://developers.google.com/google-apps/tasks/) which can be found under Application APIs.

Google's Application APIs are designed to work well with both server-side scripting and client-side JavaScript.  To work with the Google Tasks API you'll need three things:

1. A Google account (an existing one is fine)
2. Google API Console access (you may have already enabled it if you work with Google's services)
3. An API key

To set up your account to work with the Google API Console, visit [code.google.com/apis/console](https://code.google.com/apis/console/).  Once you've enabled it, scroll down to _Tasks API_:

![Google Tasks API switch](/images/posts/gapi-tasks.png)

Then switch the button to _on_, and accept the terms (if you agree to them).  Next, click _API Access_ in the left-hand navigation bar, and look under _Simple API Access_ for the API key.  This "browser apps" key is what we need.  *Make a note* of it for later.

###OAuth 2.0 for Client-side Applications

Still in the _API Access_ section of the console, click the button to create an OAuth 2.0 project.  Enter "bTask" (or whatever you want) for the product name, then `http://localhost:8080` for the URL.  In the next dialog, make sure `http://` is selected instead of `https://`, then enter `localhost:8080` and click "Create client ID".

You'll now see a set of values under "Client ID for web applications".  The field that says "Client ID" is important -- *make a note* of this one as well.

You should now have an API key _and_ a Client ID.  These will be used to load Google's APIs and allow us to use an OAuth 2.0 service from within the browser -- we won't need to write our own server-side code to authenticate users.

###Follow Along

If you want to check out the source from Part 1 so you can follow along, you can use Git to get the exact revision from last week:

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 2a8517e
{% endhighlight %}

###Required Libraries

Before progressing, download the following libraries to `app/js/lib/`:

* [Underscore.js](http://underscorejs.org/underscore-min.js)
* [Backbone.js](http://backbonejs.org/backbone-min.js)

Open `app/js/main.js` and edit the `shim` property under `requirejs.config` to load Underscore.js and Backbone.js:

{% highlight javascript %}
requirejs.config({
  baseUrl: 'js',

  paths: {
  },

  shim: {
    'lib/underscore-min': {
      exports: '_'
    },
    'lib/backbone-min': {
      deps: ['lib/underscore-min']
    , exports: 'Backbone'
    },
    'app': {
      deps: ['lib/underscore-min', 'lib/backbone-min']
    }
  }
});

require([
  'app'
],

function(App) {
  window.bTask = new App();
});
{% endhighlight %}

This looks weird, but remember we're using [RequireJS](http://requirejs.org/) to load scripts as modules.  RequireJS "shims" allow dependencies to be expressed for libraries that aren't implemented using AMD.

###Loading the Tasks API

The basic pattern for loading the Google Tasks API is:

1. Load the Google API client library: `https://apis.google.com/js/client.js`
2. Call `gapi.client.load` to load the "tasks" API
3. Set the API key using `gapi.client.setApiKey()`

To implement this, you'll need a place to put the necessary credentials.  Create a file called `app/js/config.js` and add the API key and Client ID to it:

{% highlight javascript %}
define([], function() {
  var config = {};
  config.apiKey = 'your API key';
  config.scopes = 'https://www.googleapis.com/auth/tasks https://www.googleapis.com/auth/userinfo.profile';
  config.clientId = 'your client ID';
  return config;
});
{% endhighlight %}

This file can be loaded by our custom Google Tasks API/Backbone.sync implementation.

Now create a new file called `app/gapi.js`:

{% highlight javascript %}
define(['config'], function(config) {
  function ApiManager() {
    this.loadGapi();
  }

  _.extend(ApiManager.prototype, Backbone.Events);

  ApiManager.prototype.init = function() {
  };

  ApiManager.prototype.loadGapi = function() {
  };

  Backbone.sync = function(method, model, options) {
    options || (options = {});

    switch (method) {
      case 'create':
      break;

      case 'update':
      break;

      case 'delete':
      break;

      case 'read':
      break;
    }
  };

  return ApiManager;
});
{% endhighlight %}

This skeleton module shows the overall layout of our Google Tasks API loader and `Backbone.sync` implementation.  The `ApiManager` is a standard constructor, and I've used Underscore.js to inherit from `Backbone.Events`.  This code will be asynchronous, so event handling will be useful later.

The `loadGapi` method loads Google's JavaScript using RequireJS.  Once the `gapi` global object has been found, it will do the rest of the configuration by calling the `init` method:

{% highlight javascript %}
ApiManager.prototype.loadGapi = function() {
  var self = this;

  // Don't load gapi if it's already present
  if (typeof gapi !== 'undefined') {
    return this.init();
  }

  require(['https://apis.google.com/js/client.js?onload=define'], function() {
    // Poll until gapi is ready
    function checkGAPI() {
      if (gapi && gapi.client) {
        self.init();
      } else {
        setTimeout(checkGAPI, 100);
      }
    }
    
    checkGAPI();
  });
});
{% endhighlight %}

All the `init` method needs to do is load the Tasks API with `gapi.client.load`:

{% highlight javascript %}
ApiManager.prototype.init = function() {
  var self = this;

  gapi.client.load('tasks', 'v1', function() { /* Loaded */ });

  function handleClientLoad() {
    gapi.client.setApiKey(config.apiKey);
    window.setTimeout(checkAuth, 100);
  }

  function checkAuth() {
    gapi.auth.authorize({ client_id: config.clientId, scope: config.scopes, immediate: true }, handleAuthResult);
  }

  function handleAuthResult(authResult) {
  }

  handleClientLoad();
};
{% endhighlight %}

The `config` variable was one of the dependencies for this file, and contains the credentials required by Google's API.

###Loading the API Manager

Now open `app/js/app.js` and make it depend on `gapi`, then create an instance of `ApiManager`:

{% highlight javascript %}
define([
  'gapi'
],

function(ApiManager) {
  var App = function() {
    this.connectGapi();
  };

  App.prototype = {
    connectGapi: function() {
      this.apiManager = new ApiManager();
    }
  };

  return App;
});
{% endhighlight %}

If you want to check this works by running the tests, you'll need to change `test/setup.js` to flag `gapi` as a global:

{% highlight javascript %}
var assert = chai.assert;

mocha.setup({
  ui: 'tdd'
, globals: ['bTask', 'gapi', '___jsl']
});
{% endhighlight %}

However, I don't intend to load the API remotely during testing -- this will effectively be mocked.  I'll come onto that in a later tutorial.

###Results

![gapi loaded](/images/posts/gapi-loaded.png)

If you run the app or tests and open a JavaScript console, a `gapi` global object should be available.  Using Google's APIs with RequireJS and Backbone.js seems like a lot of work, but most of this stuff is effectively just configuration, and once it's done it should work solidly enough, allowing you to focus on the app design and development side of things.

###Full Source Code

[Commit 9d09a6](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/9d09a66b1f722ebf80198a8db76dd32a7b4a6923).

###References

* [Using OAuth 2.0 for Client-side Applications](https://developers.google.com/accounts/docs/OAuth2UserAgent)

