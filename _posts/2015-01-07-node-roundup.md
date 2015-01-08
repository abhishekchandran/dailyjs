---
layout: post
title: "Node Roundup: no-sequence, CodeOnMobile, app-notify"
author: Alex Young
image: "/images/posts/codeonmobile.png"
categories:
- node
- modules
- libraries
- security
- mobile
- sms
---

###no-sequence

If you've got a corporate policy for enforcing strong passwords, then you might want to look at what npm modules can help validate passwords rather than rolling your own.  Eric Douglas sent in no-sequence (GitHub: [thothJS/no-sequence](https://github.com/thothJS/no-sequence, License: _MIT_, npm: [no-sequence](https://www.npmjs.com/package/no-sequence)), which checks to ensure passwords do not contain sequential characters:

{% highlight javascript %}
var noSequence = require('no-sequence').checkSequence;
var assert = require('assert');
var password = '123456';
var minSize = 6;

assert.equal(noSequence(password, minSize), false);
{% endhighlight %}

The repository has examples and tests which show it working with character sequences and minimum and maximum sizes.

###CodeOnMobile

Daishi Kato has been working on a new project that allows you to write code on phones and tablets.  He notes that this is good for holiday hacking, when you're stranded without a desktop/laptop.

![CodeOnMobile](/images/posts/codeonmobile.png)

It works with GitHub accounts, and there's a live demo here: [codeonmobile.axlight.com](http://codeonmobile.axlight.com/#/home).  The source is available at GitHub under [dai-shi/codeonmobile](https://github.com/dai-shi/codeonmobile) with a BSD license, and uses [Codeship](https://codeship.com/) to deploy your app to Heroku.

###app-notify

app-notify (GitHub: [chovy/app-notify](https://github.com/chovy/app-notify), License: _ISC_, npm: [app-notify](https://www.npmjs.com/package/app-notify)) by Anthony Ettinger is a module for sending SMS messages.  You can use promises, or callbacks:

{% highlight javascript %}
notify.sms({
  message: 'Hello world'
})
.then(function(data){
  console.log(data);
})
.catch(function(err){
  console.error(err);
});
{% endhighlight %}

It requires Twilio credentials for SMS, and can also send email (with nodemailer).
