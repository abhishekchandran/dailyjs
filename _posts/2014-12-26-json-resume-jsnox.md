---
layout: post
title: "Dynamic-json-resume, JSnoX"
author: Alex Young
categories:
- react
- json
- careers
---

###Dynamic-json-resume

I don't know about you, but I hate putting together my résumé.  I start to focus too much on the presentation even though you're meant to keep it simple.  [Dynamic-json-resume](http://jrm2k6.github.io/dynamic-json-resume/) (GitHub: [jrm2k6/dynamic-json-resume](https://github.com/jrm2k6/dynamic-json-resume), License: _MIT_, npm: [json-resume-dynamic](https://www.npmjs.com/package/json-resume-dynamic)) by Jeremy Dagorn is a module for generating résumés from a simple JSON format.  You can output PDFs, and use it with a Node application.

Because your CV is now represented by a structured data format, you can reuse it in other places.  For example, your personal website could render it in a sidebar.

James Long's article, [Removing User Interface Complexity, or Why React is Awesome](http://jlongster.com/Removing-User-Interface-Complexity,-or-Why-React-is-Awesome), inspired the project.  React seems like the perfect way to manipulate and render your JSON CV.

###JSnoX

What do you do if you like React but dislike JSX?  Shawn Price sent in his coworker's project, JSnoX (GitHub: [af/JSnoX](https://github.com/af/JSnoX), License: _MIT_, npm: [jsnox](https://www.npmjs.com/package/jsnox)), which provides a simple React markup API that works in pure JavaScript:

{% highlight javascript %}
var d = require('jsnox')(React)
var LoginForm = React.createClass({
  submitLogin: function() { ... },

  render: function() {
    return d('form[method=POST]', { onSubmit: this.submitLogin }, [
      d('h1.form-header', 'Login'),
      d('input:email[name=email]', { placeholder: 'Email' }),
      d('input:password[name=pass]', { placeholder: 'Password' }),
      d(MyOtherComponent, { myProp: 'foo' }),
      d('button:submit', 'Login')
    ]);
  }
});
{% endhighlight %}

This API sidesteps the issue of JavaScript's lack of multiline string handling for embedded templates, while not requiring too much fiddly syntax for handling DOM attributes.
