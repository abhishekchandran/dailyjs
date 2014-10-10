---
layout: post
title: "Google's Cloud Platform Library"
author: "Alex Young"
image: "/images/posts/gcloud.png"
categories:
- google
- modules
- libraries
---

JJ Geewax announced the [gcloud node](http://googlecloudplatform.github.io/gcloud-node/#/) (GitHub: [GoogleCloudPlatform / gcloud-node](https://github.com/GoogleCloudPlatform/gcloud-node), License: _Apache 2.0_, npm: [gcloud](https://www.npmjs.org/package/gcloud)) client library for Node.  It allows you to access things like the Google Cloud Datastore database and Cloud Storage.  You should be able to use it with Google Compute Engine or a Google Developer's service account.

I had a look at this module and there are a few interesting things to note:

* They use Mocha for tests, and there are lots of tests
* The API and code formatting are in line with the Node community
* [The documentation](http://googlecloudplatform.github.io/gcloud-node/#/docs/) looks modern and uses AngularJS (it's generated with [dox](https://www.npmjs.org/package/dox))

There's a blog post about the project here: [gcloud-node - a Google Cloud Platform Client Library for Node.js](http://googlecloudplatform.blogspot.co.uk/2014/09/gcloud-node-google-cloud-platform-client-library-for-nodejs.html) which demonstrates the API.

With a little bit of configuration, getting data from the API is as simple as `dataset.get`:

{% highlight javascript %}
dataset.get(dataset.key(['Product', 'Computer']), function(err, entity) {
  console.log(err || entity);
});
{% endhighlight %}

With cool Node libraries like this, AngularJS, and [MEAN on Google Compute Engine](http://dailyjs.com/2014/08/28/mean-google/), I'm just waiting for someone at Google to bring a first-party Node IDE to my Chromebook!

