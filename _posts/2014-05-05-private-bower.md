---
layout: post
title: "Private Bower"
author: Alex Young
categories:
- bower
- build-tools
---

![Private bower](/images/posts/private-bower.png)

If you've ever wanted to set up a private [Bower](http://bower.io/) repository, private-bower (GitHub: [Hacklone/private-bower](https://github.com/Hacklone/private-bower), License: _MIT_, npm: [private-bower](https://www.npmjs.org/package/private-bower)) by Barna Tóth might be what you're looking for.

You can install it with `npm install -g private-bower`, and then run it with `private-bower`.  It accepts some command-line options to change what port it listens on, but all you really need to do is add some lines to your `.bowerrc` file:

{% highlight javascript %}
{ "registry": "http://localhost:5678" }
{% endhighlight %}

That changes the repository Bower will use.  Now whenever Bower attempts to fetch a package, it will check your private server.

`private-bower` itself will serve packages if they've been downloaded, otherwise it will fall over to the public repository.  It's built using Express, and the author has put the API methods in the readme so you can see how it works.
