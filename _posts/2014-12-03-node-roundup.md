---
layout: post
title: "Node Roundup: Mailman, trayballoon, unembed"
author: "Alex Young"
image: "/images/posts/trayballoon.gif"
categories: 
- node
- libraries
- modules
- email
- windows
- scraping
---

###Mailman

Mailman (GitHub: [vdemedes/mailman](https://github.com/vdemedes/mailman), License: _MIT_, npm: [mailman](https://www.npmjs.org/package/mailman)) by Vadim Demedes is a module for sending emails that supports generators.  It uses [nodemailer](https://www.npmjs.org/package/nodemailer) for sending email, and [consolidate.js](https://github.com/tj/consolidate.js) for templates, which means it supports lots of different template languages.

Generators are used for sending emails, so you can do this:

{% highlight javascript %}
var mail = new UserMailer({ to: 'vadim@example.com' }).welcome();
yield mail.deliver();
{% endhighlight %}

Mailman expects a specific directory layout for views, but the added level of structure might help if you've got a big mess of email-related code in your current projects.

###trayballoon

![trayballoon](/images/posts/trayballoon.gif)

trayballoon (GitHub: [sindresorhus/trayballoon](https://github.com/sindresorhus/trayballoon), License: _MIT_, npm: [trayballoon](https://www.npmjs.org/package/trayballoon)) by Sindre Sorhus is a module for showing system tray balloons in Windows.  You can set the text and image to display, and a callback that will run when the balloon disappears:

{% highlight javascript %}
trayballoon({
  text: 'Unicorns and rainbows'
  icon: 'ponies.ico',
  timeout: 20000
}, function() {
  console.log('Trayballoon disappeared');
});
{% endhighlight %}

It also has a command-line tool which you could use to display notifications when things like tests fail.  trayballoon works by bundling an executable called `nircmdc.exe` which is called with `child_process.spawn`.

###unembed

Given some "embed code" for sites like YouTube and Vimeo, unembed (GitHub: [colearnr/unembed](https://github.com/colearnr/unembed), License: _MIT_, npm: [unembed](https://www.npmjs.org/package/unembed)) by Prabhu Subramanian will extract the markup and produce a JSON representation.  This might be useful if you're scraping sites that use embed codes, like blogs and forums.

I've never thought of applying the tiny modules philosophy to scraping, but it seems like a great way of sharing all of those hacks we use to extract data in a more structured way.
