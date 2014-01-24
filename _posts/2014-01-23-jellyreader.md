---
layout: post
title: "JellyReader: Dropbox/Google Drive Feed Reader"
author: Alex Young
categories:
- angularjs
- jquery
- apps
- services
---

Ray Wang sent in [JellyReader](http://jellyreader.com/) (GitHub: [NimbusBase / jellyreader](https://github.com/NimbusBase/jellyreader/), License: _MIT_), an entirely client-side feed reader that is powered by Google Drive and Dropbox.  [NimbusBase](http://nimbusbase.com/) has been used to unify access to Google Drive and Dropbox, so the data is ultimately stored as flat files.

JellyReader itself is implemented with jQuery and AngularJS.  It allows you to add feeds, view entries, toggle the read state, and you can also star your favourite items.  I tried it out with my Dropbox account, and Dropbox states that the application only has access to an "app" folder:

![Dropbox](/images/posts/jelly_dropbox_auth.png)

I added DailyJS to it:

![Jelly add feed](/images/posts/jelly_add_feed.png)

And the stories are rendered as you might expect:

![Jelly feed view](/images/posts/jelly_feeds.png)

After playing around with the web interface for a while, I wondered what the files on Dropbox looked like.  Each data collection is serialised in a directory, and there is a file per item.  So feeds have a directory, and stories do as well.  UUIDs are used to ensure the filenames don't clash.

![Dropbox](/images/posts/jelly_dropbox.png)

Presumably NimbusBase data has the same structure on Google Drive.

The JellyReader source uses lots of third party components, including [jFeed](https://github.com/NimbusBase/jellyreader/blob/gh-pages/js/jquery.jfeed.js) which I haven't seen for a few years.  I actually like the flat file approach for personal, self-hosted applications like this, although it would be interesting to see a comparison with a [Dropbox Datastore](https://www.dropbox.com/developers/datastore/tutorial/js) implementation.

