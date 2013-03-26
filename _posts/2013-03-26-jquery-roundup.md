---
layout: post
title: "jQuery Roundup: Individual Memberships, Bootstrap Tag Autocomplete, CDNJS"
author: Alex Young
categories:
- jquery
- plugins
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery Foundation Individual Memberships

The jQuery Foundation has allowed corporations to become members for a year now, and they've just [opened up the programme](http://blog.jquery.com/2013/03/19/join-the-jquery-foundation/) to individuals.  If you're interested in effectively sponsoring the jQuery Foundation, the [jquery.com/join](https://jquery.org/join/) page has details on pricing and rewards.

Each pricing tier includes a gift, starting with a t-shirt, and the top $400 tier also includes "access to individual members only benefits at jQuery Foundation events".  I'm not sure what these _individual benefits_ are, but where I come from $400 gets you a lot of benefits for your buck, so consider me cautiously intrigued.

###Bootstrap Tag Autocomplete

When you're writing Bootstrap-based projects, including any old jQuery plugin sometimes requires a bit of extra work to tailor the required markup and CSS to fit in with Bootstrap's defaults.  That means Bootstrap plugins are in demand from developers and designers.  Nada Aldahleh recently sent in [Bootstrap Tag Autocomplete](http://sandglaz.github.com/bootstrap-tagautocomplete/) (GitHub: [Sandglaz / bootstrap-tagautocomplete](https://github.com/Sandglaz/bootstrap-tagautocomplete), License: _Apache 2.0_), which is a Bootstrap and jQuery UI component for creating Twitter-like autocomplete interfaces.

It's built on [Bootstrap's Typeahead](http://twitter.github.com/bootstrap/javascript.html#typeahead) library, and includes its own [caret position](https://github.com/Sandglaz/bootstrap-tagautocomplete/blob/master/deps/caret-position.js) library for getting and setting the caret position.

QUnit tests have been included, and the project's website includes documentation and code samples.

###CDNJS

Ryan Kirkman sent in [CDNJS](http://cdnjs.com/), which is an open source CDN.  They're looking for feedback on which libraries should be included -- there are currently 325 listed.  The code that runs the project is available on GitHub at [cdnjs / cdnjs](https://github.com/cdnjs/cdnjs), and it's based on Node.

Scripts can be added to the CDN by forking the GitHub project and following the instructions in the readme file.  The general rule of thumb is that projects must have over 100 watchers on GitHub, but as long as sufficient popularity can be demonstrated the authors will consider including a new project.  That means the list of libraries on [cdnjs.com](http://cdnjs.com/) is useful for finding high quality scripts.

