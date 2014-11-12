---
layout: post
title: "Node Roundup: Eskimo, Serve-Me, Google BigQuery and Cloud Pub/Sub"
author: "Alex Young"
image: "/images/posts/eskimo.png"
categories:
- node
- libraries
- modules
- google
- frameworks
---

###Eskimo

![Eskimo](/images/posts/eskimo.png)

[Eskimo](http://eskimo.io/) (GitHub: [niftylettuce/eskimo](https://github.com/niftylettuce/eskimo), License: _MIT_, npm: [eskimo](https://www.npmjs.org/package/eskimo)) by niftylettuce is a framework for Node web applications.  It has a command-line tool that is used to manage projects, known as _igloos_.  You can add new models, views, and controllers, or create all three with `mvc`.

Once you've installed Eskimo with npm, you can generate a new app with `eskimo create projectname`.  Projects use Express, the [electrolyte](https://www.npmjs.org/package/electrolyte) dependency injection module, and MongoDB.  You'll need to run `npm install` from the freshly created project to get the dependencies required for running the tests.

The authors have put sensible commands in `package.json` for `npm start` and `npm test`, so it works like most Node web applications.  It also has a Vagrant file, so you should be able to test out deploying your applications without too much hassle.

Initially the documentation made me think it was an alternative to Yeoman, but it's actually an MVC web framework based on Express.  The documentation and examples currently need expanding, but I found some [cool tutorials](http://niftylettuce.com/posts/nodejs-auth-google-facebook-ios-android-eskimo/) on niftylettuce's blog.

###Serve-Me

[Serve-Me](https://github.com/muit/serveMe) (GitHub: [muit/serveMe](https://github.com/muit/serveMe), License: _MIT_, npm: [serve-me](https://www.npmjs.org/package/serve-me)) by Muitxer is a small web framework that's a bit like a mix of a static server and Sinatra.  You can quickly configure it serve static pages, then add server-side route handlers with `ServeMe.Routes.add('name', fn)`.  The function has to return a string, which is why it's more like Sinatra than Express.

The reason I liked Serve-Me is it has no dependencies -- the author has used Node's core modules for everything.  The source is quite short, so you might find it interesting if you're learning Node's core modules.

###Google Cloud Platform Updates

Google's Cloud Platform Node module now has support for BigQuery and Cloud Pub/Sub.  I read about this on [Jonathan Beri's Google+ account](https://plus.google.com/u/0/+JonathanBeri/posts/KfqweWxPsBw):

> gcloud-node, the Google Cloud Client Library for Node.js, has added support for BigQuery and Cloud Pub/Sub. These Cloud APIs join Cloud Datastore and Cloud Storage. Grab it with 'npm install --save gcloud' or check out the source on GitHub.

The module is available at [GoogleCloudPlatform/gcloud-node](https://github.com/GoogleCloudPlatform/gcloud-node) on GitHub.  There's a full [TodoMVC example](https://github.com/GoogleCloudPlatform/gcloud-node-todos) that demonstrates some of the module's features.
