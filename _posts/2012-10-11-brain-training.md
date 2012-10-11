---
layout: post
title: "Brain Training Node"
author: "Alex Young"
categories: 
- node
- tutorials
- statistics
---

![Game scraper](/images/posts/brain-game-scraper.png)

The other day a friend asked me about the validity of video game review scores.  There was an accusation of payola against a well-known games magazine, and the gaming community was trying to work out how accurate the magazine's scores were.  My programmer's brain immediately thought up ways to solve this -- would a naive Bayesian classifier be sufficient to predict review scores given enough reviews?

The answer to that particular question is beyond the scope of this article.  If you're interesting in statistical tests for detecting fraudulent data, then [Benford's law](http://en.wikipedia.org/wiki/Benford's_law) is a better starting point.

Anyway, I couldn't help myself from writing some Bayes experiments in Node, and the result is this brief tutorial.

This tutorial introduces naive Bayes classifiers through the [classifier](https://npmjs.org/package/classifier) module by Heather Arthur, and uses it to classify article text from the web through the power of scraping.  It's purely educational rather than genuinely useful, but if you write something interesting based on it let me know in the comments and I'll check it out!

###Prerequisites

To complete this tutorial, the following things are required:

* A working installation of [Node](http://nodejs.org/)
* Basic Node and npm knowledge
* [Redis](http://redis.io/)

###Goals

Completing this tutorial will teach you:

* The basics of Bayesian classification
* How to use the classifier module
* Web scraping

###Getting Started

Like all Node projects, this one needs a `package.json`.  Nothing fancy, but enough to express the project's dependencies:

{% highlight javascript %}
{
  "author": "Alex R. Young"
, "name": "brain-training"
, "version": "0.0.1"
, "private": true
, "dependencies": {
    "classifier": "latest"
  , "request": "latest"
  , "cheerio": "latest"
  }
, "devDependencies": {
    "mocha": "latest"
  },
  "engines": {
    "node": "0.8.8"
  }
}
{% endhighlight %}

The [cheerio](https://npmjs.org/package/cheerio) module implements a subset of jQuery, and a small DOM model.  It's a handy way to parse web pages where accuracy isn't required.  If you need a more accurate DOM simulation, the popular choice is [JSDOM](https://npmjs.org/package/jsdom).

###Core Module

The classifier module has an extremely simple API.  It can work with in-memory data, but I wanted to persist data with Redis.  To centralise this so we don't have to keep redefining the Redis configuration, the classifier module can be wrapped up like this:

{% highlight javascript %}
var classifier = require('classifier')
  , bayes
  ;

bayes = new classifier.Bayesian({
  backend: {
    type: 'Redis'
  , options: {
      hostname: 'localhost'
    , port: 6379
    , name: 'gamescores'
    }
  }
});

module.exports = {
  bayes: bayes
};
{% endhighlight %}

Now other scripts can load this file, and run `train` or `classify` as required.  I called it `core.js`.

###Naive Bayes Classifiers

The classifier itself implements a [naive Bayes classifier](http://en.wikipedia.org/wiki/Naive_Bayes_classifier).  Such algorithms have been used as the core of many spam filtering solutions since the mid-1990s.  Recently a book about Bayesian statistics, [Think Bayes](http://www.greenteapress.com/thinkbayes/), was featured on Hacker News and garnered a lot of praise from the development community.  It's a free book by Allen Downey and makes a difficult subject relatively digestible.

The spam filtering example is probably the easiest way to get started with Bayes.  It works by assigning each word in an email a probability of being _ham_ or _spam_.  When a mail is marked as spam, each word will weighted accordingly -- this process is known as _training_.  When a new email arrives, the filter can add up the probabilities of each word, and if a certain threshold is reached then the mail will be marked as spam.  This is known as classification.

What makes this type of filtering _naive_ is that each word is considered an independent "event", but in reality the position of a word is important due to the grammatical rules of the language.  Even with this arguably flawed assumption, naive classifiers perform well enough to help with a wide range of problems.

The Wikipedia page for [Bayesian spam filtering](http://en.wikipedia.org/wiki/Bayesian_spam_filtering) goes into more detail, relating spam filtering algorithms to the formulas required to calculate probabilities.

###Training

Create a new file called `train.js` as follows:

{% highlight javascript %}
var cheerio = require('cheerio')
  , request = require('request')
  , bayes = require('./core').bayes
  ;

function parseReview(html) {
  var $ = cheerio.load(html)
    , score
    , article
    ;

  article = $('.copy .section p').text();
  score = $('[typeof="v:Rating"] [property="v:value"]').text();
  score = parseInt(score, 10);

  return { score: score, article: article };
}

function fetch(i) {
  var trained = 0;

  request('http://www.eurogamer.net/ajax.php?action=frontpage&page=' + i + '&type=review', function(err, response, body) {
    var $ = cheerio.load(body)
      , links = []
      ;

    $('.article a').each(function(i, a) {
      var url;
      if (a.attribs) {
        url = 'http://www.eurogamer.net/' + a.attribs.href.split('#')[0];
        if (links.indexOf(url) === -1) {
          links.push(url);
        }
      }
    });

    var left = links.length;

    links.forEach(function(link) {
      console.log('Fetching:', link);
      request(link, function(err, response, body) {
        var review = parseReview(body)
          , category
          ;

        if (review.score > 0 && review.score <= 5) {
          category = 'bad';
        } else if (review.score > 5 && review.score <= 10) {
          category = 'good';
        }

        if (category) {
          console.log(category + ':', review.score);
          bayes.train(review.article, category);
          trained++;
        }

        left--;

        if (left === 0) {
          console.log('Trained:', trained);
        }
      });
    });
  });
}

fetch(1)
{% endhighlight %}

This code is tailored for [Eurogamer](http://www.eurogamer.net/).  If I wanted to write a production version, I'd separate out the scraping code from the training code.  Here I just want to illustrate how to scrape and train the classifier.

The `parseReview` function uses the cheerio module to pull out the review's paragraph tags and extract the text.  This is pretty easy because cheerio automatically operates on arrays of nodes, so `$('.copy .section p').text()` will return a block of text for each paragraph without any extra effort.

The `fetch` function could be adapted to call Eurogamer's article paginator recursively, but I thought if I put that in there they'd get angry if enough readers tried it out!  In this example, `fetch` will download each article from the first page.  I've tried to ensure unique links are requested by creating an array of links and then calling `Array.prototype.indexOf` to see if the link is already in the array.  It also strips out links with hash URLs, because Eurogamer includes an extra `#comments` link.

Once the unique list of links has been generated, each one is downloaded.  It's worth noting that I use Mikeal Rogers' [request](https://npmjs.org/package/request) module here to simplify HTTP requests -- Node's built-in HTTP client library is fine, but Mikeal's module cuts down a bit of boilerplate code.  I use it in a lot of projects, from web scrapers to crawlers, and interacting with RESTful APIs.

The scraper code in `parseReview` tries to pull out the score from the HTML.  If a score between 0 and 5 is found, then the article is categorised as 'bad', and anything else is 'good'.

###Classification

To actually classify other text, we need to find some other text and then call `bayes.classify` on it.  This code expects review URLs from Edge magazine.  For example: [Torchlight II review](http://www.edge-online.com/review/torchlight-ii-review/).

{% highlight javascript %}
var request = require('request')
  , cheerio = require('cheerio')
  , bayes = require('./core').bayes
  ;

request(process.argv[2], function(err, request, body) {
  if (err) {
    console.error(err);
  } else {
    var $ = cheerio.load(body)
      , text = $('.post-page p').text()
      ;

    console.log(text);

    bayes.classify(text, function(category) {
      console.log('category:', category);
    });
  }
});
{% endhighlight %}

Again, cheerio is used to pull out article text, and then it's handed off to `bayes.classify`.  Notice that the call to `classify` looks asynchronous -- I quite like the idea of building a simple reusable asynchronous Node Bayes classifier service using Redis.

This script can be run like this:

{% highlight text %}
node classify.js http://www.edge-online.com/review/liberation-maiden-review/
{% endhighlight %}

###Conclusion

I've combined my interest in computer and video games with Node to attempt to use a naive Bayes classifier to determine if text about a given game is _good_ or _bad_.  Of course, this is a lot more subjective than the question of _ham_ or _spam_, so the value is limited.  However, hopefully you can see how easy the classifier module makes Bayesian statistics, and you should be able to adapt this code to work with other websites or plain text files.

Heather Arthur has also written [brain](https://npmjs.org/package/brain), which is a neural network library.  We've featured this module before on DailyJS, but as there's only three dependents on npm I thought it was worth brining it up again.
