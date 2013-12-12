---
layout: post
title: "JavaScript Developer Survey 2013: Results"
author: Alex Young
categories:
- community
- surveys
---

The JavaScript Developer Survey has now closed.  As always the results are available to the community for further analysis:

* [Summary](http://dailyjs.com/files/2013-survey-summary.pdf)
* [Raw spreadsheet data](http://dailyjs.com/files/2013-survey-data.zip) (zipped CSV)
* [Results for 2012](http://dailyjs.com/2012/12/24/javascript-survey-results/)

<div class="image">
  <img src="/images/posts/2013-survey-type.png" alt="" />
  <small>Most people write client-side code.</small>
</div>

51% of readers write client-side code, while 28% said they write server-side code.  Last year client-side was at 98%, so I imagine this is partly due to a changing audience on DailyJS, but it's interesting how strong server-side development is becoming.

Where do you write JavaScript?  54% said "at work", and 45% said "side projects".  This is probably a case of people doing both -- I find it's common for programmers to be both hobbyists and professionals.

The majority of readers have been writing JavaScript for three to five years (34%).  I can't help but feel this is thanks to the growth of Node -- people rediscovering JavaScript after using other languages for server-side web development, or the growth of client-side frameworks like AngularJS and Backbone.js.  I can't imagine doing design without some JavaScript skills.

78% of readers said they don't use a language that compiles to JavaScript.  I've noticed some of the influential members of the Node community are vocal about these languages, so it seems like our readers agree.  I try to keep some coverage of these languages on the blog, but in general the focus is on JavaScript.

CoffeeScript was the most popular "compile-to" language (64%), and TypeScript was up from last year to 19%.

The style question caused much confusion.  Semicolons, commas at the end, and methods with one space were popular options.  It's interesting to see 9% using tabs and 11% using spaces.  Unlike some languages, JavaScript can survive a little bit of variance in tab size, so I'm not too bothered either way.  Client-side veterans seem to use four spaces, though, and 8% of respondents selected this option.

The results for testing amused me:

* Yes: 25%
* No: 26%
* Sometimes / Not enough / Not too much / When needed: 50%

I like your honesty.  "Not enough" could be just modesty, so I'm going to read this as "a lot of readers write tests but think they could be doing better".

Jasmine is hugely popular, with 30%.  I still think tap is the best approach, but it only received 2% of your clicks.  Mocha's doing well with 27%, and QUnit is down to 16%.  I think this is more evidence of a large number of Node developers doing the survey, but it could also be the fact that people see Mocha as a browser/Node module, and QUnit as something just for jQuery (which it isn't really).

CI servers?  36% said yes.  Node is definitely CI server friendly -- I've recently been setting up a TeamCity server for Objective-C projects and it's surprisingly hard work.  Compared to switching on Travis CI for an open source Node project it's a joke.  However, Jenkins is the most popular CI server (44%), and TeamCity got 13%, so perhaps people find it easy to slot client-side or Node tests into an existing CI server in companies that use multiple languages.

<div class="image">
  <img src="/images/posts/2013-survey-amd.png" alt="" />
  <small>AMD is extremely popular.</small>
</div>

It turns out people like AMD!  However, if we break down the stats for CommonJS, we see 17% using CommonJS and 12% using Browserify.  For a long time I advocated CommonJS, but substack's Browserify argument is convincing...

Grunt is winning at build scripts (60%).  Fortunately, "npm scripts" had a good response (17%), which is encouraging because I feel like lots of tasks are simple enough to work that way, rather than needing a confusing 200 line Gruntfile.

I was surprised to see AngularJS and Backbone.js both get 25% for client-side frameworks.  They have mindshare, but I can't help but feel they solve very different problems.

The common wisdom seems to be IE support should start at IE 8 (37%).  I'm going to guess that's to support corporates, which has been the bane of my web development existence for over a decade now.

Do you use ES6 features?  85% said "No", so you're OK if you don't.  I probably only do to write DailyJS articles, but we'll see this start to grow over the next year.

PHP is the most popular primary development language (24%), and C# got 17%.  Hello .Net folks!

Thanks to everyone who took part in the survey!  If you can use the data for something cool, [I'd love to hear about it](http://contact.dailyjs.com/general).
