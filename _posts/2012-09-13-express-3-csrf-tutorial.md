---
layout: post
title: "Express 3 Tutorial: Contact Forms with CSRF"
author: "Alex Young"
categories:
- express
- tutorials
- bootstrap
---

This tutorial is a hands on, practical introduction to writing Express 3 applications complete with CSRF protection.  As a bonus, it should be fairly easy to install on Heroku.

###Prerequisites

A working Node installation is assumed, and basic knowledge of Node and the command-line.

###Getting Started

Create a new directory, then create a new file called `package.json` that looks like this:

{% highlight javascript %}
{
  "author": "Alex R. Young"
, "name": "dailyjs-contact-example"
, "version": "0.0.1"
, "private": true
, "dependencies": {
    "express": "3.0"
  , "jade": "0.27.2"
  , "validator": "0.4.11"
  , "sendgrid": "latest"
  }
, "devDependencies": {
    "mocha": "latest"
  },
  "engines": {
    "node": "0.8.9"
  }
}
{% endhighlight %}

Express has a built-in app generator, but I want to explain all the gory details.  If you want to try it out, try typing `express myapp` in the terminal.

Back to the `package.json` file.  The author and name can be changed as required.  The `private` flag is set so we don't accidentally publish this module to [npmjs.org](https://npmjs.org/).  The dependencies are as follows:

* `express`: The web framework we're using, version 3 has been specified
* `jade`: The template language, you could convert this project to [ejs](https://npmjs.org/package/ejs) or something else if desired
* `validator`: The [validator](https://github.com/chriso/node-validator) library will be used to validate user input
* `sendgrid`: [SendGrid](http://sendgrid.com/) is a commercial email provider that's easy to use with Heroku

The `engines` section has been included because it's a good idea to be specific about Node versions when deploying to Heroku.

###Configuration

Although I typically encourage breaking up Express projects into multiple files, this project will use a single JavaScript file for brevity.

First, the modules are loaded, and an Express app is instantiated.  Users of Express 2.x will notice that there is no longer a `createServer()` method call:

{% highlight javascript %}
var express = require('express')
  , app = express()
  , SendGrid = require('sendgrid').SendGrid
  , Validator = require('validator').Validator
  ;
{% endhighlight %}

The `Validator` object is just one way to work with the node-validator module.  The author has also provided [Express middleware](https://github.com/ctavan/express-validator) for directly validating data in requests.  I didn't use it here because I was concerned it might not work with Express 3, and I'm writing to a deadline, but it's worth taking a look at it.  In general, I like to avoid tying too much code into Express in case I want to migrate to another framework, so that's worth considering as well.

The next few lines are application configuration:

{% highlight javascript %}
app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'jade');
  app.use(express.cookieParser());
  app.use(express.session({ secret: 'secret goes here' }));
  app.use(express.bodyParser());
  app.use(app.router);
  app.use(express.csrf());
  app.use(express.static(__dirname + '/public'));
});
{% endhighlight %}

When you're writing Express configuration, avoid copying and pasting lines from examples without fully understanding what each line does -- it will get you into trouble later!  You should understand what every single line does here, because changing the order of `app.use` lines can impact the way requests are processed and result in frustrating errors.

With that in mind, here's what each line does:

* `app.set('views', __dirname + '/views')`: Use `./views` as the default path for the client-side templates
* `app.set('view engine', 'jade')`: Automatically load `index.jade` files just by passing `index`
* `app.use(express.cookieParser())`: Parse the HTTP `Cookie` header and create an object in `req.cookies` with properties for each cookie
* `app.use(express.session...`: Use a session store -- this is needed for the CSRF middleware
* `app.use(express.bodyParser())`: Parse the request body when forms are submitted with `application/x-www-form-urlencoded` (it also supports `application/json` and `multipart/form-data`)
* `app.use(app.router)`: Use the actual router provided by Express
* `app.use(express.csrf())`: The [CSRF](http://www.senchalabs.org/connect/csrf.html) protection middleware
* `app.use(express.static(__dirname + '/public'))`: Serve static files in the `./public` directory


Next follows configuration for development and production environments:

{% highlight javascript %}
app.configure('development', function() {
  app.use(express.errorHandler({ dumpExceptions: true, showStack: true }));
  app.locals.pretty = true;
  sendgrid = {
    send: function(opts, cb) {
      console.log('Email:', opts);
      cb(true, opts);
    }
  };
});

app.configure('production', function() {
  app.use(express.errorHandler());
  sendgrid = new SendGrid(process.env.SENDGRID_USERNAME, process.env.SENDGRID_PASSWORD);
});
{% endhighlight %}

The `app.locals.pretty = true` line causes Jade to render templates with indentation and newlines; otherwise it spits out a single line of HTML.  Notice that `app.use` is being called outside of `app.configure` -- this is perfectly fine, and `app.use` can actually be called anywhere.  There was some discussion about removing `app.configure` from Express 3.x, and it isn't technically required.

I've made a mock `sendgrid` object for development mode that just prints out the email and then runs a callback.  The production configuration block uses environmental variables (`process.env.SENDGRID_USERNAME`) to set the SendGrid username and password.  It's a good idea to use environmental variables for passwords, because it means you can keep them out of your source code repository.  Since only specific developers should have access to the deployment environment, then it's potentially safer to store variables there.  Heroku allows such variables to be set with `heroku config:add SENDGRID_USERNAME=example`.

###Helpers

The next few lines are new to Express 3:

{% highlight javascript %}
app.locals.errors = {};
app.locals.message = {};
{% endhighlight %}

The `app.locals` object is passed to all templates, and it's how helpers are defined in Express 3 applications.  I've used these properties so I can write templates without first checking if these objects exist, else a `ReferenceError` would be raised.

###Middleware Callbacks: CSRF Protection

I've mentioned CSRF but haven't fully explained it yet.  It stands for "Cross-Site Request Forgery", and is a class of exploits in web applications where an attacker forces another user to execute unwanted actions on a web site.  In this case it's not particularly useful, but it's good practice to guard against CSRF attacks in production web apps.  The [Open Web Application Security Project has a good article on CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)), which includes example attacks.

{% highlight javascript %}
function csrf(req, res, next) {
  res.locals.token = req.session._csrf;
  next();
}
{% endhighlight %}

The [Connect CSRF middleware](http://www.senchalabs.org/connect/csrf.html) automatically generates the `req.session._csrf` token, and this function maps it to `res.locals.token` so it will be available to templates.  Any route that needs CSRF protection now just needs to include the middleware callback:

{% highlight javascript %}
app.get('/', csrf, function(req, res) {
  res.render('index');
});
{% endhighlight %}

The form in `views/index.jade` has a hidden input:

{% highlight text %}
form(action='/contact', method='post')
  input(type='hidden', name='_csrf', value=token)
{% endhighlight %}

The `token` variable is the one set by the middleware callback in `res.locals.token`.

###Validating Data

The contact form must be validated before an email is sent.  Seeing as database storage isn't necessary for this project, we can use the [node-validator](https://github.com/chriso/node-validator) module to verify user input.  I've put this in a function to abstract it from the corresponding route:

{% highlight javascript %}
function validate(message) {
  var v = new Validator()
    , errors = []
    ;

  v.error = function(msg) {
    errors.push(msg);
  };

  v.check(message.name, 'Please enter your name').len(1, 100);
  v.check(message.email, 'Please enter a valid email address').isEmail();
  v.check(message.message, 'Please enter a valid message').len(1, 1000);

  return errors;
}
{% endhighlight %}

An instance of a `Validator` is created, and I've set a custom error handling function.  This error handling function collects the errors into an array, but there are many other solutions supported by node-validator's API.

Each message property is checked against a single validation, but several could be chained together.

The `validate` function itself expects a `message` object which will come from the posted form later.

###Sending Email

Emails are sent with SendGrid.  Again, I've made a function for this to keep it out of the corresponding Express routes:

{% highlight javascript %}
function sendEmail(message, fn) {
  sendgrid.send({
    to: process.env.EMAIL_RECIPIENT
  , from: message.email
  , subject: 'Contact Message'
  , text: message.message
  }, fn);
}
{% endhighlight %}

I've made it accept a callback so the Express route can handle cases where sending the mail fails.

###Posting the Form

Here is the Express route that handles the form post:

{% highlight javascript %}
app.post('/contact', csrf, function(req, res) {
  var message = req.body.message
    , errors = validate(message)
    , locals = {}
    ;

  function render() {
    res.render('index', locals);
  }

  if (errors.length === 0) {
    sendEmail(message, function(success) {
      if (!success) {
        locals.error = 'Error sending message';
        locals.message = message;
      } else {
        locals.notice = 'Your message has been sent.';
      }
      render();
    });
  } else {
    locals.error = 'Your message has errors:';
    locals.errors = errors;
    locals.message = message;
    render();
  }
});
{% endhighlight %}

It uses the `csrf` middleware callback to generate another token.  This is required because the contact form will always be rerendered.  The form data can be found in `req.body.message` -- I've used form variables like `message[email]`, so these will get translated into a JavaScript object with corresponding properties.

When there are invalid fields, or sending the email fails, the contact form will be rendered again with the original message.  To make the form retain the values, the `value` property of each field must be set:

{% highlight text %}
form(action='/contact', method='post')
  input(type='hidden', name='_csrf', value=token)
  .control-group
    label.control-label(for='message_name') Your Name
    .controls
      input#message_name.input-xxlarge(type='text', placeholder='Name', name='message[name]', value=message.name)
  .control-group
    label.control-label(for='message_email') Email
    .controls
      input#message_email.input-xxlarge(type='text', placeholder='Email', name='message[email]', value=message.email)
  .control-group
    label.control-label(for='message_message') Message
    .controls
      textarea#message_message.input-xxlarge(placeholder='Enter message', rows='6', name='message[message]')=message.message
  button.btn(type='submit') Send Message
{% endhighlight %}

This is quite a chunk of Jade, but the extra markup is there because I've used [Bootstrap](http://twitter.github.com/bootstrap/) to style the project.

The `locals` object I've used gets passed to the `res.render` message and contains the form data when required.

###Download

The full source is available here: [alexyoung / dailyjs-contact-form-tutorial](https://github.com/alexyoung/dailyjs-contact-form-tutorial).
