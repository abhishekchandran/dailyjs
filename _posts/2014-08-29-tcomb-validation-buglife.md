---
layout: post
title: "tcomb-validation, Bug Life"
author: "Alex Young"
categories:
- node
- validation
- data
- github
- graphs
---

###tcomb-validation

[tcomb-validation](https://gcanti.github.io/resources/tcomb-validation/playground/playground.html) (GitHub: [gcanti / tcomb-validation](https://github.com/gcanti/tcomb-validation), License: _MIT_) by Giulio Canti is a general purpose validation library that can be used with (or without) React and Backbone.

It's based on the [tcomb](https://github.com/gcanti/tcomb) library which is a runtime type checking library.

Using the plain JavaScript API, you can check types like this:

{% highlight javascript %}
var t = require('tcomb-validation');
var validate = t.addons.validation.validate;

validate(1, t.Str).isValid();
validate('a', t.Str).isValid();
{% endhighlight %}

If you call `firstError`, you'll get an `Error` object with a description of what failed the validation.  You can combine validators using the `struct` method, and these can be passed to `validate` so you can validate forms.  You can even pass a JSON schema to `validate`.

The Backbone integration works by calling `validate` like this:

{% highlight javascript %}
var Model = Backbone.Model.extend({
  validate: function (attrs, options) {
    return validate(attrs, Attrs).errors;
  }
});
{% endhighlight %}

###Bug Life

![Bug Life](/images/posts/buglife.png)

[Bug Life](http://9-volt.github.io/bug-life/) was created for [the GitHub Data Challenge](https://github.com/blog/1864-third-annual-github-data-challenge), and displays a chart derived from issue data.  It includes the labels and issue life cycle events, so you can see what the common labels are and how long it takes to close issues.

The screenshot I included was of Backbone, and generating it required authorisation with the GitHub API.  Bug Life handles this quite well -- once the API limit was hit I just had to click Authorize and that was pretty much it.

The author has included some explanations of the charts on the project's demo page:

> This is a popular repo on github - backbone. It has a rich history, well organized labels and release cycles. On version 0.9.0, when backbone reached a relatively stable state, many issues were closed. Before this release there were other important ones, for example 0.5.0.

> After 0.9.0 backbone lived through 3 other important milestones: 0.9.9, 1.0.0 and 1.1.0. Each of these releases was focused on different aspects. Right before version 0.9.9 most open issues were of type change, while before version 1.1.0 most open issues were of type bug.


