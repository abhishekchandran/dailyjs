---
layout: post
title: "Backbone.js Tutorial: Authenticating with OAuth2"
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
  <li><a href="http://dailyjs.com/2012/12/13/backbone-tutorial-3/"><strong>Part 3: Authenticating with OAuth2</strong></a></li>
  <li><a href="http://dailyjs.com/2012/12/20/backbone-tutorial-4/">Part 4: Backbone.sync</a></li>
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/">Part 5: List Views</a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
</ul>

In [Part 2: Google's APIs](http://dailyjs.com/2012/12/06/backbone-tutorial-2/), I laid the groundwork for talking to Google's JavaScript APIs.  Now you're in a position to start talking to the `todos` API, but first a user account is required.

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `9d09a66b1f`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 9d09a66b1f
{% endhighlight %}

###Google's OAuth 2.0 Client-side API

Open `app/js/gapi.js` and take a look at [lines 11 to 25](https://github.com/alexyoung/dailyjs-backbone-tutorial/blob/9d09a66b1f722ebf80198a8db76dd32a7b4a6923/app/js/gapi.js#L11-L25).  There's a method, provided by Google, called `gapi.auth.authorize`.  This uses the "Client ID" and some scopes to attempt to authenticate.  I've already set the scopes in `app/js/config.js`:

{% highlight javascript %}
config.scopes = 'https://www.googleapis.com/auth/tasks https://www.googleapis.com/auth/userinfo.profile';
{% endhighlight %}

This tells the authentication system that our application would like to access the user's profile and Gmail tasks.  Everything is almost ready to work, but two things are missing: an implementation for `handleAuthResult` and an interface.

###Templates

RequireJS can load templates by using the [text](https://github.com/requirejs/text) plugin.  Download [text.js](https://raw.github.com/requirejs/text/master/text.js) from GitHub and save it to `app/js/lib/text.js`.

This is my preferred technique for handling templates.  Although this application could easily fit into a monolithic `index.html` file, breaking up projects into smaller templates is more manageable in the long run, so it's a good idea to get used to doing this.

Now open `app/js/main.js` and add the `text` plugin to the `paths` property of the RequireJS configuration:

{% highlight javascript %}
paths: {
  text: 'lib/text'
},
{% endhighlight %}

Finally, add this to `app/js/config.js`:

{% highlight javascript %}
_.templateSettings = {
  interpolate: /\{\{(.+?)\}\}/g
};
{% endhighlight %}

This tells Underscore's templating system to use double curly braces for inserting values, otherwise known as interpolation.

The app needs some directories to store template-related things:

* `app/js/views` -- This is for Backbone.js views
* `app/js/templates` -- Plain HTML templates, to be loaded by the views
* `app/css`

The `app/index.html` file needs to load the CSS, so add a `link` tag to it:

{% highlight javascript %}
<link rel="stylesheet" href="css/app.css">
{% endhighlight %}

And create a suitable CSS file in `app/css/app.css`:

{% highlight css %}
#sign-in-container, #signed-in-container { display: none }
{% endhighlight %}

The application will start up by hiding both the sign-in button and the main content.  The oauth API will be queried for existing user credentials -- if the user has already logged in recently their details will be stored in a cookie, so the views need to be configured appropriately.

###Templates

The templates aren't particularly remarkable at this stage, just dump this into `app/js/templates/app.html`:

{% highlight html %}
<div class="row-fluid">
  <div class="span2 main-left-col" id="lists-panel">
    <h1>bTask</h1>
    <div class="left-nav"></div>
  </div>
  <div class="main-right-col">
    <small class="pull-right" id="profile-container"></small>
    <div>
      <div id="sign-in-container"></div>
      <div id="signed-in-container">
        <p>You're signed in!</p>
      </div>
    </div>
  </div>
</div>
{% endhighlight %}

This template shows some things that we won't be using yet, just ignore it for now and focus on `sign-in-container` and `signed-in-container`.

Next, paste the following into `app/js/templates/auth.html`:

{% highlight html %}
<a href="#" id="authorize-button" class="btn btn-primary">Sign In with Google</a>
{% endhighlight %}

The `auth.html` template will be inserted into `sign-in-container`.  It's very simple at the moment, I only really included it for an excuse to create extra Backbone.js views so you can see how it's done.

###Backbone Views

These templates need corresponding Backbone.js views to manage them.  This part demonstrates how to load templates with RequireJS and render them.  Create a file called `app/js/views/app.js`:

{% highlight javascript %}
define([
  'text!templates/app.html'
],

function(template) {
  var AppView = Backbone.View.extend({
    id: 'main',
    tagName: 'div',
    className: 'container-fluid',
    el: 'body',
    template: _.template(template),

    events: {
    },

    initialize: function() {
    },

    render: function() {
      this.$el.html(this.template());
      return this;
    }
  });

  return AppView;
});
{% endhighlight %}

The `AppView` class doesn't have any events yet, but it does bind to an element, `body`, and load a template: `define(['text!templates/app.html']`.  The `text!` directive is provided by the RequireJS "text" plugin we added earlier.  The template itself is just a string that contains the corresponding HTML.  It's rendered by binding it to the `Backbone.View`, and then calling jQuery's `html()` method which replaces the HTML within an element: `this.$el.html(this.template());`.

The `AuthView` is a bit different.  Create a file called `app/js/views/auth.js`:

{% highlight javascript %}
define(['text!templates/auth.html'], function(template) {
  var AuthView = Backbone.View.extend({
    el: '#sign-in-container',
    template: _.template(template),

    events: {
      'click #authorize-button': 'auth'
    },

    initialize: function(app) {
      this.app = app;
    },

    render: function() {
      this.$el.html(this.template());
      return this;
    },

    auth: function() {
      this.app.apiManager.checkAuth();
      return false;
    }
  });

  return AuthView;
});
{% endhighlight %}

The `app` object is passed to `initialize` when `AuthView` is instantiated (with `new AuthView(this)` later on).  The reason I've done this is to allow the view to call the required authentication code from `ApiManager`.  This could also be handled with events, or many other ways -- I just wanted to show that we can initialise views with values just like any other class.

###App Core

The views need to be instantiated and rendered.  Open `app/js/app.js` and change it to load the views using RequireJS:

{% highlight javascript %}
define([
  'gapi'
, 'views/app'
, 'views/auth'
],

function(ApiManager, AppView, AuthView) {
  var App = function() {
    this.views.app = new AppView();
    this.views.app.render();

    this.views.auth = new AuthView(this);
    this.views.auth.render();

    this.connectGapi();
  }
{% endhighlight %}

The rest of the file can remain the same.  Notice that the order these views are rendered is important -- `AuthView` won't work unless it has some of `AppView`'s tags available.  A better way of modeling this might be to move `AuthView` inside `AppView` so the dependency is reflected.  You can try this yourself if you want to experiment.

###Authentication Implementation

The `app/js/gapi.js` file still doesn't have the `handleAuthResult` function, so nothing will work yet.  Here's the code to handle authentication:

{% highlight javascript %}
function handleAuthResult(authResult) {
  var authTimeout;

  if (authResult && !authResult.error) {
    // Schedule a check when the authentication token expires
    if (authResult.expires_in) {
      authTimeout = (authResult.expires_in - 5 * 60) * 1000;
      setTimeout(checkAuth, authTimeout);
    }

    app.views.auth.$el.hide();
    $('#signed-in-container').show();
  } else {
    if (authResult && authResult.error) {
      // TODO: Show error
      console.error('Unable to sign in:', authResult.error);
    }

    app.views.auth.$el.show();
  }
}

this.checkAuth = function() {
  gapi.auth.authorize({ client_id: config.clientId, scope: config.scopes, immediate: false }, handleAuthResult);
};
{% endhighlight %}

The trick to a smooth sign-in flow is to determine when the user is already signed in.  If so, then authentication should be handled transparently, otherwise the user should be prompted.

The `handleAuthResult` function is called by `gapi.auth.authorize` from the `checkAuth` function, which isn't displayed here (it's before `handleAuthResult` in the source file if you want to check it).  The `this.checkAuth` _method_ is different -- this is a public method that calls `gapi.auth.authorize` with `immediate` set to `false`, while the other invocation calls it with `true`.

The `immediate` option is important because it determines whether a popup will be displayed or not.  I've used it to check if the user is already signed in, otherwise it's called again with `immediate: false` and will display a suitable popup so the user can see what permissions the app wants to use:

![Authentication process](/images/posts/google-auth-backbone.png)

I designed it this way based on the [Google APIs Client Library for JavaScript](http://code.google.com/p/google-api-javascript-client/wiki/Authentication) documentation:

> "The standard `authorize()` method always shows a popup, which can be a little jarring if you are just trying to refresh an OAuth 2.0 token. Google's OAuth 2.0 implementation also supports "immediate" mode, which refreshes a token without a popup. To use immediate mode, just add "immediate: true" to the login config as in the example above."

I've also changed the `ApiManager` class to store a reference to `App`:

{% highlight javascript %}
// Near the top of gapi.js
var app;

function ApiManager(_app) {
  app = _app;
  this.loadGapi();
}
{% endhighlight %}

###Summary

In this tutorial you've seen how to use Google's APIs to sign into an app you've previously registered with the Google API Console (documented in part 2).  It might seem like a lot of work to get RequireJS, Backbone.js, and Google OAuth working together, but think about what this has achieved: 100% client-side scripting that can authenticate with existing Google accounts.

If I've missed anything here, you can check out the full source from [commit c1d5a2e7c](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/c1d5a2e7ccadf82289676e6dd4fead9b1e311435).
