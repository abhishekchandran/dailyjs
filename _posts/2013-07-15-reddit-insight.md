---
layout: post
title: "Reddit Insight, dropstore-ng"
author: Alex Young
categories:
- node
- mongodb
- express
- apps
- AngularJS
---

###Reddit Insight

![Reddit Insight](/images/posts/redditinsight.png)

Patrick Stapleton sent in [Reddit Insight](http://www.redditinsight.com/) (GitHub: [gdi2290 / RedditInsight](https://github.com/gdi2290/RedditInsight/), License: _MIT_), a project for tracking and visualising statistics about [reddit](http://www.reddit.com/).  It can track posts, users, and display interactive charts for words and topics.  There's also a frequency analysis of nouns, and a graph for comments per-post and average karma per-post.

If you want to install it, check the code out from GitHub and install the Node dependencies:

{% highlight sh %}
git clone https://github.com/gdi2290/RedditInsight.git
cd RedditInsight
npm install
{% endhighlight %}

If you don't have `nodemon` installed you can install that too -- the authors use it to automatically reload the code when server-side code changes:

{% highlight sh %}
npm install -g nodemon
npm start
{% endhighlight %}

I haven't yet figured out where they got the data from -- the post and user trackers call reddit's APIs, but the clusters have locally cached JSON files.

###dropstore-ng

![dropstore-ng](/images/posts/dropboxdatastore.png)

More AngularJS bindings!  [dropstore-ng](https://github.com/AnalogJ/dropstore-ng) by Jason Kulatunga is a wrapper around [Dropbox Datastore](https://www.dropbox.com/developers/datastore).  Dropbox's API has bindings for iOS, Android, and JavaScript -- this library allows you to fit it into an AngularJS-style workflow.  You can DI it, authenticate with Dropbox, then add datastore items to the current `$scope`:

{% highlight javascript %}
...
.then(function(datastore){
  var taskTable = datastore.getTable('tasks');
  $scope.tasks =  taskTable.query();
});
{% endhighlight %}

And display them as you might expect:

{% highlight javascript %}
<ul>
  <li ng-repeat="task in tasks">
    {{task.get('taskname')}}
  </li>
</ul>
{% endhighlight %}

I haven't yet used the Dropbox Datastore API, but this looks like idiomatic AngularJS to me.  There are no directives as far as I can see, but I can't think of any that would make sense...
