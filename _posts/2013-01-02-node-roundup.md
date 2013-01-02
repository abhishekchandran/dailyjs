---
layout: post
title: "Node Roundup: 0.9.5, juxt, email-templates"
author: "Alex Young"
categories: 
- node
- modules
- email
- express
- functional
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.9.5

[Node 0.9.5](http://blog.nodejs.org/2012/12/29/node-v0-9-5-unstable/) (unstable) is out, and Isaac said weekly releases will be the norm for the near future:

> For the next month at least, the primary focus will be on bug fixing and performance.  Expect nearly-weekly releases until v0.10 is ready.

Amongst the raft of bug fixes, the updated stream module has some tweaks as well:

* stream: fix to emit end event on http.ClientResponse (Shigeki Ohtsu)
* stream: fix event handler leak in readstream pipe and unpipe (Andreas Madsen)

###juxt

[juxt](https://github.com/azer/juxt.js) (License: _WTFPL_, npm: [juxt](https://npmjs.org/package/juxt)) by Azer Koculu is a small module that takes in functions and outputs a new function that stitches them together:

{% highlight javascript %}
function inc1(n) { return n+1 };
function inc2(n) { return n+2 };
function inc3(n) { return n+3 };

juxt(inc1, inc2, inc3)(314); // returns [315, 316, 317]
{% endhighlight %}

It also has an asynchronous API, and will intelligently collate arguments into arrays or objects.

###email-templates

[email-templates](https://github.com/niftylettuce/node-email-templates) (License: _MIT_, npm: [email-templates](https://npmjs.org/package/email-templates)) by Nick Baugh is a module for rendering email templates using ejs and "email-friendly" inline CSS.  When I make Node web applications, I usually treat emails as an afterthought, rendering them with Jade or ejs.  However, there are times when more attention to design is required, and this is made difficult in email due to the way certain major email clients treat CSS.

[Juice](https://github.com/LearnBoost/juice) from LearnBoost is used to generate suitable `style` attributes based on your CSS, making the task of inlining CSS less messy.  The module will also generate a text version of the email if a suitable template is provided.  The author has provided a full example with [Nodemailer](https://github.com/andris9/Nodemailer).

Nick also sent in a few of his other interesting modules, including [express-cdn](http://niftylettuce.github.com/express-cdn/) (GitHub: [niftylettuce / express-cdn](https://github.com/niftylettuce/express-cdn), License: _MIT_, npm: [express-cdn](https://npmjs.org/package/express-cdn)) which automatically optimises assets in Express applications.  The assets will be delivered using Amazon S3 and CloudFront, so you can create your own CDN.

