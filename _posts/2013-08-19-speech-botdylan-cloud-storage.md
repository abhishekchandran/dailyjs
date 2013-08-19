---
layout: post
title: "Speech Router, Botdylan, Google Cloud Storage"
author: Alex Young
categories:
- api
- storage
- speech
- chrome
- github
---

###Speech Router

Speech Router (GitHub: [lukasolson / speech-router](https://github.com/lukasolson/speech-router), License: _MIT_) is a router that wraps around [Chrome's Web Speech API](http://www.google.com/intl/en/chrome/demos/speech.html).  It's based around a constructor function that accepts a `routes` object:

{% highlight javascript %}
new SpeechRouter({
  routes: {
    'search google for *query': function(query) {
      window.open('https://google.com/search?q=' + query);
    }
  }
});
{% endhighlight %}

If you haven't seen the Web Speech API before, it's worth checking out.  At least the results seem quite good with my accent and Chrome --  your mileage may vary!

###Botdylan

Botdylan (GitHub: [botdylan / botdylan](https://github.com/botdylan/botdylan), License: _MIT_) by Pau Ramon is a [Hubot](https://github.com/github/hubot)-inspired GitHub automation system:

> We use GitHub heavily. There are some repetitive tasks that were taking away our time to hack on a better product. Since we are in the productivity space we decided to stop doing things manually and start to have a more productive environment to work with.

It can do things like add labels to issues based on events, integrate with a CI server, talk to chat rooms, and so on.  It runs as a daemon, and can execute tasks periodically in the background.

###Google Cloud Storage

[Google Cloud Storage](https://www.youtube.com/watch?v=8ytpvQJNOU8), sent in by Jonathan Simon, is a screencast that demonstrates a JavaScript application that talks to [Google's Cloud Storage platform](https://cloud.google.com/products/cloud-storage).  The source code is here: [storage-getting-started-javascript](https://github.com/GoogleCloudPlatform/storage-getting-started-javascript).

> This demonstration covers getting started with Google Cloud Storage using JavaScript. See the process of setting up the sample application, running the sample and using it to try out Cloud Storage API commands like 'list buckets'.

