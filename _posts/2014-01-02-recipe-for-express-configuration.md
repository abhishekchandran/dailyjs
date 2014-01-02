---
layout: post
title: "Recipe for Express Configuration Files"
author: Alex Young
categories:
- node
- express
- configuration
- recipes
---

Express has a few helper methods that support configuration.  There are three pairs of methods: `get` and `set` for setting values, `enable` and `disable` for toggling boolean options, and `enabled` and `disabled` for testing boolean options.  Options can be set based on the current environment by using the `configure` method.

Here's an example of these methods:

{% highlight javascript %}
var express = require('express');
var app = express();
var assert = require('assert');

app.set('title', 'DailyJS');
assert.equal(app.get('title'), 'DailyJS');

app.configure('production', 'staging', function() {
  // 'emails' is an internal setting I've made up
  // It could be used to only send emails from certain environments
  app.enable('emails');
  assert(app.enabled('emails'));
});

app.configure('test', function() {
  app.disable('emails');
  assert(app.disabled('emails'));
});
{% endhighlight %}

The `configure` method is based on `process.env.NODE_ENV`, which is available in `app.get('env')`.  If you access it through `app.get` you'll see a default of `'development'` rather than `undefined`.  When you deploy your application you'll want to make sure the `NODE_ENV` environmental variable is set to `staging` or `production`.  How this is done is based on operating system or cloud provider -- with Heroku it would be `heroku config:add NODE_ENV=production`.

These methods are useful, but sometimes you want to store settings in configuration files.  It depends on the type of project you're working on, but most of the commercial projects I've worked on required configuration files.

I use JSON as the format for these files because it's easy to write and parse in Node projects.  You don't even need to use `JSON.parse`, you can just use `require`.  I like to use a configuration file for each environment, so I usually end up with a directory like this:

{% highlight text %}
config/development.json
config/production.json
config/test.json
{% endhighlight %}

You can load one of these files with `require('config/development.json')`, but you can go a step further by using an `index.js` file:

{% highlight javascript %}
module.exports = {
  development: require('./development.json'),
  production: require('./production.json'),
  test: require('./test.json')
};
{% endhighlight %}

Now you can use `var config = require('./config')` elsewhere in your project.  However, because `process.env.NODE_ENV` gets set, we can simplify that `index.js` file even further:

{% highlight javascript %}
module.exports = require('./' + (process.env.NODE_ENV || 'development') + '.json');
{% endhighlight %}

Now `require('./config')` will return an object that contains the configuration for the current environment.  I use this to do things like turn off AWS emails in my unit tests, but leave them on for the production system.  By exploiting the design of Node's module system you basically get configuration files for free.

This might not be the best solution for every project.  The [config](https://npmjs.org/package/config) module by Loren West supports YAML files, and [nconf](https://npmjs.org/package/nconf) from flatiron is hierarchical -- settings can be passed in as command-line options, from the environment, or from a file, and used based on precedence.  It can also store settings in databases like Redis.

How do you configure your Express projects?
