---
layout: post
title: "VanillaMasker, jsTag"
author: "Alex Young"
categories:
- jquery
- angularjs
- ui
---

###VanillaMasker

[VanillaMasker](http://bankfacil.github.io/vanilla-masker/) (GitHub: [BankFacil / vanilla-masker](https://github.com/BankFacil/vanilla-masker), License: _MIT_) by Caio Ribeiro Pereira is a small library for masking input elements with formats.  It supports money, numbers, and custom patterns.

For example, a simple date mask would look like this:

{% highlight javascript %}
masker.toPattern(12122000, "99/99/9999");
{% endhighlight %}

It doesn't have any dependencies (hence "vanilla"), unless you want to build it locally.

###jsTag

[jsTag](http://eranhirs.github.io/jsTag/) (GitHub: [eranhirs / jsTag](https://github.com/eranhirs/jsTag/), License: _MIT_, Bower: _jsTag_) by Eran Hirsch is an AngularJS library for handling rich tag input fields.  To use it, add a `js-tag` element to your HTML, and then add the `js-tag-options` directive for specifying a placeholder and default tag values.

You can also access it in JavaScript like this:

{% highlight javascript %}
demoApp.controller('CustomizedController', ['$scope', function($scope) {
  // Export jsTag's options
  $scope.jsTagOptions = {
    'texts': {
      'inputPlaceHolder': 'Type text here'
    },
    'defaultTags': ['Default Tag #1', 'Default Tag #2']
  };
}]);
{% endhighlight %}

The documentation includes an example of using it with Twitter's [typeahead.js](https://github.com/twitter/typeahead.js/) project.
