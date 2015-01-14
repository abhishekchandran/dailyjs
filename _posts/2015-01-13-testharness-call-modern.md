---
layout: post
title: "ngTestHarness, call-n-times, modern.IE Automation"
author: Alex Young
image: "/images/posts/modernietest.png"
categories:
- testing
- libraries
- scripts
- angular
---

###ngTestHarness

David Posin sent in [ngTestHarness](http://randomjavascript.blogspot.co.uk/2015/01/ngtestharness-strap-in-with-this-new.html), a test harness for Angular scopes, controllers, and providers.  It helps to reduce the amount of boilerplate needed for dependency injection during testing.

By default it loads the `ng`, `ngMock`, and `ngSanitize` modules.  By using the `ngHarness` API, tests can be as simple as:

{% highlight javascript %}
describe('Test the note-editor directive', function() {
  var harness = new ngHarness(['noteEditor']);

  it('Adds the container div', function() {
    expect(harness.compileElement('<my-note></my-note>').html()).toBe('<div class="editor-container"></div>');
  });
});
{% endhighlight %}

The `ngHarness` object manages the required dependency injections for each test context.  The [API documentation](https://github.com/gaikai/ngTestHarness/blob/master/api.md) covers the `ngTestHarness` class and each method that it implements.

David notes that the project was the result of work at Team Titan at Gaikai, owned by Sony Entertainment.

###call-n-times

call-n-times by Shahar Or (GitHub: [mightyiam/call-n-times](https://github.com/mightyiam/call-n-times), License: _MIT_, npm: [call-n-times](https://www.npmjs.com/package/call-n-times)) came about when the author was trying to make test code cleaner.  Given a function, this module will synchronously run it the specified number of times:

{% highlight javascript %}
var assert = require('assert');
var call = require('call-n-times');

function logAndReturn() {
  console.log('foo');
  return 'foo';
}

var returns = call(logAndReturn, 3);
assert.equal(returns.length, 3);
assert.equal(returns[0], 'foo');
{% endhighlight %}

Shahar wondered if there's a built-in JavaScript way to do this, something closer to how it would work if you used an array and `forEach`.  Does anyone know?

###modern.IE, VirtualBox, Selenium

I expect many readers use modern.IE for testing.  Wouldn't it be nice if you could quickly create new instances so you can trash old ones, or use them as part of a test suite?  Denis Suckau sent in a script called [mkvm.sh](https://github.com/conceptsandtraining/modernie_selenium) (License: _MIT_) for automatically creating VirtualBox virtual machines with Modern IE Windows images.  It's a shell script that supports various configuration options, like the Selenium and Java environmental variables, VM memory usage, and so on.

The readme has details on how to configure it, and the background behind the project:

> As the modern.ie-Machines refuses to run more than 30-90 Days (at least for more than an hour) we remove the machines on a regular basis and recreate the original Appliance with all changes needed to run Selenium.
>
> Use it with your favored test runner (maybe Karma or Nightwatch.js) to automate JavaScript tests in real browsers on your own Selenium Grid. Other WebDriver language bindings (Python, Java) should work as well.

If you wanted to install IE 6, then you could run `mkvm.sh VMs/IE6\ -\ WinXP.ova`.  It also supports deleting a VM, so you can delete and recreate IE 6 with `mkvm.sh VMs/IE6\ -\ WinXP.ova --delete "IE6 - WinXP"`.

