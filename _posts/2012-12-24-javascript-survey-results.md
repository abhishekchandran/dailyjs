---
layout: post
title: "JavaScript Developer Survey 2012: Results"
author: Alex Young
categories:
- community
- surveys
---

The JavaScript Developer Survey has now closed.  As always the results are available to the community for further analysis:

* [Summary](https://docs.google.com/spreadsheet/viewform?formkey=dFNDeGZEUTZUZ1ctY0Q2WFZnOVlBV3c6MA)
* [Raw spreadsheet data](https://docs.google.com/spreadsheet/ccc?key=0AooyU9-5EwIVdFNDeGZEUTZUZ1ctY0Q2WFZnOVlBV3c)

<div class="image">
  <img src="/images/posts/survey-2012-type.png" alt="" />
  <small>Meteor seems to be struggling to gain traction.</small>
</div>

98% of readers write client-side JavaScript, which is unchanged from last year.  I included Meteor because it's had so much press this year, but it seems like it's still not very popular, at 2%.

I've always felt like this survey could be useful to those who are looking to create open source projects and even commercial services aimed at the JavaScript community.  With that in mind, it's interesting that 57% of respondents said they don't currently write Node but are interested in learning about it.  Only 9% were not interested.  There are solid educational resources for Node out there, but it seems like people are hungry for more.

71% of respondents don't use a language that compiles to JavaScript.  This surprised me, because this year it certainly felt like more of our project submissions (for both client-side and server-side) were written in CoffeeScript.

Speaking of CoffeeScript, it was the most popular compile-to-JavaScript language, at 82%.  TypeScript was second, at 14%, which is ahead of Dart by 10%.

<div class="image">
  <img src="/images/posts/survey-2012-style.png" alt="" />
  <small>There are plenty of worn out semicolon keys out there.</small>
</div>

I thought the question "What JavaScript stylistic choices do you prefer?" may have resulted in controversy, but thankfully we got some interesting results.  At 85%, most respondents use semicolons.  And, 67% use commas at the end.  53% use spaces, with 39% tabbing instead.  I would have thought spaces were more popular, but I've seen a lot of open source client-side projects that use tabs, so the JavaScript community isn't as settled on tabs vs. spaces as some other popular languages.

My philosophy on this is to always match the style of the project you're working on, and you'll see me doing this in some planned DailyJS eBooks for 2013.

###Testing and Benchmarking

51% of respondents don't write tests -- down from 58% last year.

Jasmine is the most popular testing library, at 45%, with Mocha close behind at 41%.  QUnit is also very popular with 31%.  For reference, these were last year's test library results:

> Jasmine (44%) has edged out QUnit (41%)!  Vows is also doing well with 13%.  Express/Mocha scored 11%, slightly ahead of Nodeunit at 8%.

Vows is now down to 7%, and Mocha has risen by a staggering 30%.  It's natural for some libraries to rank higher if they work in both browsers and Node.

JSLint is down to 56% from 67%, but it's still the most popular static analysis tool.  JSHint is close behind at 55%.

_uglify_ is the most popular minimiser, which isn't surprising given that it's bundled with many other tools.

WebKit Inspector is the most popular debugging tool, at 79%.  500 people said they debug using `node --debug`, which is interesting because this is an area that I still feel needs work when developing with Node.

80% of respondents benchmark with client-side tools (1372 people).  That's probably not surprising, but given the performance-obsessed nature of certain prominent Node developers I'd have expected to see more people ticking "Benchmark scripts using a benchmarking library".

44% of readers also write PHP, down slightly from 46% last year.  C, Java, Python, and Ruby all rank around 20%, with Java edging the others out.  Are there any Android developers out there?

###Loading

RequireJS is the most popular module loading system -- 1237 people use it.  Given the sheer amount of documentation it has and the high quality site, it's not surprising that it's popular.  Others that I didn't mention included YUI, LABjs, and ExtJS.

Google Ajax Libraries is the most popular CDN, and it was interesting to see CloudFlare at 11%.

###Project Hosting

<div class="image">
  <img src="/images/posts/survey-2012-hosting.png" alt="" />
  <small>GitHub dominates when it comes to project hosting.</small>
</div>

At 91%, I wondered if GitHub might be at its peak.  It was at 81% last year.  I know there are many fellow freelancers who appreciate Bitbucket's free private hosting, and at 20% I suspect there are people out there using both for the same reasons as me.  Google Code is at 3%, so Google has got its work cut out if it wants to compete for open source projects.

Also, at 83%, GitHub was the most popular 'project discovery' site.  This is higher than news sites (22%), which surprised me because it seems like there's an interesting JavaScript project on Hacker News every other day.

###Summary

Apart from a few surprises, 2012 has seen similar trends to last year.  The new questions from Todd Bashor, Tyler Larson, and Adam Alexander were excellent, and I'm looking forward to seeing if semicolon use changes over time.

Thanks to everyone who took part in the survey!

