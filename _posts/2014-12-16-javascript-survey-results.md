---
layout: post
title: "JavaScript Developer Survey 2014: Results"
author: Alex Young
categories:
- community
- surveys
---

The JavaScript Developer Survey has now closed.  As always the results are available to the community for further analysis:

* [Summary](http://dailyjs.com/files/2014-survey-summary.pdf)
* [Raw spreadsheet data](http://dailyjs.com/files/2014-survey-data.csv.gz) (gzipped CSV)
* [Results for 2013](http://dailyjs.com/2013/12/12/javascript-survey-results/)
* [Results for 2012](http://dailyjs.com/2012/12/24/javascript-survey-results/)

<div class="image">
  <img src="/images/posts/2014-survey-graph-1.png" alt="" />
  <small>Browser-based developers are still the majority.</small>
</div>

97% of readers write client-side code, while 56% said they write server-side code.  Last year server-side development was at 28%.  I'd like to think that the interest and adoption of technologies like Node will contribute to the direction of ECMAScript, because some proposals seem to go against the strides that have already been made in the Node community (the module system, for example).

The DailyJS readership is very experienced (27% said 5-10 years), so perhaps I should do more to cover advanced topics?

78% of readers said they don't use a language that compiles to JavaScript -- both this year and last year.  I've written more about technologies like TypeScript this year, partly because I respect that project in particular, but Dart is also compelling.  However, Dart was one of the least popular compile-to languages (1%).  TypeScript is more popular (5%), but CoffeeScript is still the most popular (16%).

It turns out most people like semi-colons.  I think they're going to stick around in the JavaScript community because they're used in so many other languages, but it's always possible that styles will change over time.  According to the survey results, the stylistic choices are actually similar to some of the more popular JavaScript style guides.

ES6 features are getting popular: 24% said they use ES6.  I suspect that more people actually do use them, because `'use strict'` is something I've seen in lots of JavaScript best practice articles.  Also, Node frameworks like [Koa](http://koajs.com/) use cool features like generators quite well, so I think this figure will grow over the next year.

Testing: 29% said they write tests.  I was interested to see that PhantomJS is a very popular test environment (38%).  I've mentioned many times on DailyJS that I struggle a little bit when it comes to this type of testing, because the tests seem to become brittle and break over time.  However, the number of people that use PhantomJS is close to Node, so presumably most people have found a way to make it work well enough.

Jasmine and Mocha are still the most popular test frameworks, and Karma is gaining on them now as well.

61% use JSHint for static analysis.  That's 2608 people, which surprised me because I don't often use a linter.  I think it might be down to people verifying open source client-side JavaScript, but it would be interesting to find out exactly why people are motivated to lint JavaScript.

Gulp (35%) is already almost as popular as Grunt (47%).  It's amazing how quickly Gulp has been adopted, although I've found I can understand Gulp more readily than Grunt scripts.

When it comes to client-side dependencies, CommonJS with Browserify is at 20%, with plain old files at 30%. I think that's interesting because Browserify is my preferred solution, but I often use plain old files because I'm working on a legacy project where Browserify is a luxury we don't have time for.

AngularJS is strangely popular (49%).  I've noticed that many in the JavaScript community regard React (16%) as the latest hot framework and see it as an alternative to Angular, but they do different things so I prefer to use the appropriate tool for each project.  Meteor is a lot less popular than the hype had me believe (6%), but it's possible that DailyJS readers don't like Meteor.  It's worth noting that Backbone.js is popular, with 31%.

SublimeText won the editor wars, although a fair few readers use IDEs like IntelliJ and Visual Studio.

The most popular minimum IE is IE 9.  I find that's interesting because I still get asked to support 8 for corporate networks that can't seem to untangle themselves from web-based legacy software (do any readers use ADP for example?)

Here are the top "other" programming languages:

1. PHP
2. Java
3. C#/.NET

I still find it strange that PHP is so popular, although it's 6 on the [TIOBE](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html) index, and this is primarily a web development blog after all.

Thanks to everyone who took part in the survey!  If you'd like me to run another rather than waiting for a whole year, then [get in touch with your ideas](http://contact.dailyjs.com/general).
