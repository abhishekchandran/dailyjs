---
layout: post
title: "Node Roundup: Stream Handbook, Screenshot as a Service, captchagen, Suppose"
author: "Alex Young"
categories: 
- node
- modules
- libraries
- security
- unix
- streams
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Stream Handbook

[Stream Handbook](https://github.com/substack/stream-handbook) by the venerable James Halliday is a guide to streams, a commonly overlooked feature of Node that's only just starting to get the attention it deserves.

So far James has written a solid introduction to streams, and he's working on adding more detailed coverage based on Node's related API methods and objects.

###Screenshot as a Service

[Screenshot as a Service](http://dotheweb.posterous.com/screenshot-as-a-service-now-in-beta-test-the) (GitHub: [fzaninotto / screenshot-as-a-service](https://github.com/fzaninotto/screenshot-as-a-service), License: _MIT_) by Francois Zaninotto is a fork of [TJ Holowaychuk's screenshot-app](https://github.com/visionmedia/screenshot-app), which is running at [screenshot.etf1.fr](http://screenshot.etf1.fr/usage.html).  Since forking the app, Francois has worked on making it more robust.  It can be used synchronously or asynchronously:

{% highlight text %}
# Take a screenshot
GET /?url=www.google.com

# Asynchronous call
GET /?url=www.google.com&callback=http://www.myservice.com/screenshot/google
{% endhighlight %}

###captchagen

![captchagen](/images/posts/captchagen.png)

[captchagen](https://github.com/wearefractal/captchagen) (License: _MIT_, npm: [captchagen](https://npmjs.org/package/captchagen)) from the team at Fractal is a CAPTCHA image generator.  It can generate both a PNG and the corresponding audio through eSpeak.

Images are generated based on a custom algorithm and the [Canvas module](https://npmjs.org/package/canvas).  Mocha tests have been included.

###Suppose

[Suppose](http://procbits.com/2012/08/03/like-unix-expect-automate-command-line-programs-in-node-js-with-suppose/) (GitHub: [jprichardson / node-suppose](https://github.com/jprichardson/node-suppose), License: _MIT_, npm: [suppose](https://npmjs.org/package/suppose)) by JP Richardson is a JavaScript version of Expect (`man expect`).  It has a chainable API, so it's easy to create complex expectations with a familiar syntax:

{% highlight javascript %}
suppose('npm', ['init'])
  .debug(fs.createWriteStream('/tmp/debug.txt'))
  .on(/name\: \([\w|\-]+\)[\s]*/).respond('awesome_package\n')
  .on('version: (0.0.0) ').respond('0.0.1\n')
  .on('description: ').respond("It's an awesome package man!\n")
  .on('entry point: (index.js) ').respond("\n")
  .on('test command: ').respond('npm test\n')
  .on('git repository: ').respond("\n")
  .on('keywords: ').respond('awesome, cool\n')
  .on('author: ').respond('JP Richardson\n')
  .on('license: (BSD) ').respond('MIT\n')
  .on('ok? (yes) ' ).respond('yes\n')
.error(function(err){
    console.log(err.message);
})
.end(function(code){
{% endhighlight %}

The author has included Mocha tests and examples in the readme file.
