---
layout: post
title: "Wallaby.js Updates, Jasmine ES6 Tests, Chakram"
image: "/images/posts/typescriptwallaby.gif"
author: Alex Young
categories:
- sponsored-content
- testing
- coverage
- es6
- rest
---

###Wallaby.js Updates

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

I recently wrote about [Wallaby.js](http://wallabyjs.com/), and the authors have just released a major update that adds support for ES6, RequireJS, Browserify, and webpack.  I'm a fan of Browserify so I was excited to see this -- you can get it at [hwallabyjs/wallabify](https://github.com/wallabyjs/wallabify).  The webpack postprocessor is available here: [jeffling/wallaby-webpack](https://github.com/jeffling/wallaby-webpack).

Other updates include the news that a [full-time developer has joined the project](http://dm.gl/2015/03/03/wallaby-first-developer-and-investors/), and a tutorial that introduces the idea of [live editing with testing](http://dm.gl/2015/03/05/JavaScript-live-editing-and-testing/).

Wallaby.js is an intelligent test runner for JavaScript projects, and has some cool features like editor-integrated code coverage reporting, and parallel test execution.  It supports React JSX, popular test frameworks like Jasmine and Mocha, and even works with TypeScript and CoffeeScript.

<img src="/images/posts/typescriptwallaby.gif" width="530" />

Wallaby.js is a commercial product, but it's currently free during the preview.  The site has more details on how to sign up for the preview: <http://wallabyjs.com/>.

###Jasmine ES6 Tests

We're used to using transpilers for client-side code and sometimes Node projects, but what about tests?  If ES6 really makes code more readable and maintainable, then I definitely want to use these language features to make my tests better!  Torgeir Helgevold sent in a tutorial about [writing Jasmine tests with ES6](http://www.syntaxsuccess.com/viewarticle/5532c5c0873cb5f0449ffcc5).  The basic idea is to add preprocessors to a `karma.config.js` file that includes settings for Babel.

[Karma](http://karma-runner.github.io) is the test runner used by AngularJS, and it's test framework agnostic, so you could adapt this technique to work with Mocha as well.

Because Karma can easily be used to manipulate your test files before they execute, then it makes sense for people who want to use transpilers.  I haven't done this before (my tests are usually very vanilla Mocha/assert tests), but it seems like a reasonable solution.

###Chakram API Testing

[Chakram](http://dareid.github.io/chakram/) (GitHub: [dareid/chakram](https://github.com/dareid/chakram), License: _MIT_, npm: [chakram](https://www.npmjs.com/package/chakram)) by Dan Reid is an API testing framework, based on promises.  It includes Mocha and Chai, but instead of calling `done` callbacks you can use the `wait` method:

{% highlight javascript %}
var chakram = require('chakram');
var expect = chakram.expect;

describe('Minimal example', function() {
  it('should provide a simple async testing framework', function() {
    var request = chakram.get('http://httpbin.org/get');
    expect(request).to.have.status(200);
    expect(request).not.to.have.header('non-existing-header');
    return chakram.wait();
  });
});
{% endhighlight %}

There's a [list of extended chai expectations](http://dareid.github.io/chakram/module-chakram-expectation.html), and methods for HTTP and promises in the [Chakram module documentation](http://dareid.github.io/chakram/module-chakram.html).  This includes methods for HTTP verbs, so you can do `chakram.patch` and `chakram.put`.
