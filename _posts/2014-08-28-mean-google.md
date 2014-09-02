---
layout: post
title: "Google Get MEAN"
author: "Alex Young"
categories:
- node
- services
- google
---

![Google MEAN](/images/posts/googlemean.png)

Melissa from [Linnovate](http://www.linnovate.net/), the company behind [MEAN.IO](http://mean.io/), wrote in to say [Google have announced support for MEAN](http://googlecloudplatform.blogspot.co.il/2014/08/click-to-deploy-mean-development-stack-on-google-compute-engine.html) on Google Compute Engine.

Normally when I think of Google I think Java and Python.  Other services including Heroku and Azure support a wide range of platforms, including Node, so it's exciting to see Google offering MEAN.

The developer guide is here: [MEAN development stack on Google Compute Engine](https://developers.google.com/cloud/mean/), but it's worth noting that the MEAN stack can be brought up with click-to-deploy.  That means you can get MongoDB, Express, and Angular running in minutes, using a web-based wizard.

I'm not exactly sure how the pricing works with MongoDB, because [SQL database pricing](https://developers.google.com/cloud-sql/pricing) is different from [Compute Engine](https://developers.google.com/compute/pricing).  I created a click-to-deploy MEAN project and it seemed to show all the resources under Compute Engine, so I think that means all prices are based on CPU/disk usage.

I make a lot of Express apps, and Google's developer tools (including the web console) seem compelling even next to Heroku and Azure, so I'd definitely like to try this for a real project soon!
