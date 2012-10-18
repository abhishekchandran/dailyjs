---
layout: post
title: "Totally Testacular"
author: Alex Young
categories: 
- libraries
- testing
- node
- browser
---

<blockquote class="twitter-tweet"><p>We are now 100% relying on @<a href="https://twitter.com/testacularjs">testacularjs</a>. Finally! <a href="https://t.co/LJv3Z07Q" title="https://plus.google.com/110323587230527980117/posts/44VHjmyuvXD">plus.google.com/11032358723052…</a></p>&mdash; AngularJS (@angularjs) <a href="https://twitter.com/angularjs/status/258886450601394176" data-datetime="2012-10-18T11:05:14+00:00">October 18, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8">
</script>

Vojta Jina created [Testacular](http://vojtajina.github.com/testacular/) (GitHub: [vojtajina / testacular](https://github.com/vojtajina/testacular/), License: _MIT_, npm: [testacular](https://npmjs.org/package/testacular)) to write better tests for [AngularJS](http://angularjs.org/), Google's client-side library that's rapidly gaining support from the wider web development community.

While established projects like [Selenium](http://seleniumhq.org/) are currently more complete than Testacular, the goal of bringing 100% of Angular's tests to Testacular is an important milestone that should bring more attention to the project.

![Testacular diagram](/images/posts/testacular-diagram.png)

The design of Testacular itself is actually fairly lightweight.  It uses a built-in Node-powered web server to send a test harness to a browser, and then [Socket.IO](http://socket.io/) is used for communication between the browser and client.  A special page, `/context.html`, is used to contain tests, and a Node file watcher automatically runs tests when the associated test files change.

A configuration file is used to pull all of this together.  It's basically JavaScript, but uses special variables to set configuration options.  For example, `files` is an array that holds a list of files to load in the browser, and `reporters` controls how test results are displayed.

Testacular automatically runs a browser instance when `testacular start` is invoked on the command-line.  The entire workflow is optimised around development, so you shouldn't have to leave your editor to see results.  Also, a new instance of a browser is loaded -- if you set up Chrome to run tests then your existing Chrome session won't be interfered with.

Browsers are scripted through "launcher" files.  The [Chrome launcher](https://github.com/vojtajina/testacular/blob/master/lib/launchers/Chrome.js) includes command-line invocations suitable for Linux, Windows, and Mac OS.  It's also possible to use Internet Explorer and [PhantomJS](http://phantomjs.org/).

Testing cross-platform is also supported through custom launcher files.  I found a [custom browser example](https://github.com/vojtajina/testacular/blob/master/docs/user/browsers.rst) by digging through the project's documentation.  This is intended for invoking browsers through a virtual machine on a Continuous Integration (CI) server, but this could be adapted for local development.  In fact, supporting [Travis CI](https://travis-ci.org/) was one of Vojta's initial goals for the project.

###Trying Testacular

The [Testacular readme](https://github.com/vojtajina/testacular/blob/master/README.md) has some details on how to get started writing Testacular tests.  It'll work with both [Jasmine](http://pivotal.github.com/jasmine/) and [Mocha](http://visionmedia.github.com/mocha/).  Let's say you're using Jasmine to test an existing project, and have added `testacular` to your `package.json` or installed it.  All you need to do is run `testacular init` to create a configuration file, edit it with suitable values for your project, and then start up the Testacular server with `testacular start`.

Assuming you've created a Jasmine Testacular config file, change the `files` argument as follows:

{% highlight javascript %}
files = [
  JASMINE,
  JASMINE_ADAPTER,
  'test/*.js'
];
{% endhighlight %}

And then add a test file to `test/`, anything will do:

{% highlight javascript %}
describe('Array', function(){
  describe('#indexOf()', function(){
    it('should return -1 when the value is not present', function(){
      expect([1, 2, 3].indexOf(5)).toEqual(-1);
    });
  });
});
{% endhighlight %}

Now running `testacular start` will start up the tests.  You should see something like the following screenshot -- if not, check your `basePath`.

![Testacular running on a Mac with Chrome](/images/posts/testacular.png)

###Conclusion

It's good to see interesting spin-offs coming from MVC projects.  Vojta has been working on Testacular for a while now, and it seems like his original plans are coming to fruition.  If you're frustrated with Selenium and work with Node, it might be a natural fit.

<em>P.S. Writing this article without accidentally typing "testicular" was a formidable challenge.</em>
