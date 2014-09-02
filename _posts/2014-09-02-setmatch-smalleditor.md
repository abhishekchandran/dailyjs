---
layout: post
title: "Backbone setMatch, Smalleditor"
author: "Alex Young"
categories:
- components
- ui
- libraries
- angularjs
---

###Backbone setMatch

Backbone setMatch (GitHub: [joshbambrick / setMatch](https://github.com/joshbambrick/setMatch), License: _MIT_) by Joshua Bambrick allows you to match models in a collection based on attributes other than the `id`.  This is applied whenever `set` is called on a collection, both explicitly and internally by Backbone.

The `setMatch` property can be used with arrays, so you can pass a set of names to match.  If you pass it an object you can set options, including the `id` option which controls what happens when `set` is called.  When it's set to `inherit` and incoming models have an id, then match models in the collection will inherit that id, but using `retain` will keep the original value instead.

###Smalleditor

[Smalleditor](http://jdkanani.com/smalleditor/) (GitHub: [jdkanani / smalleditor](https://github.com/jdkanani/smalleditor), License: _MIT_, Bower: `smalleditor`) by Jaynti Kanani is a WYSIWYG editor inspired by Medium.  It requires AngularJS, and features revision tracking.

Deltas can be applied to revisions to get the next revision:

{% highlight javascript %}
angular.module('smalleditorDemo', ['ngRoute', 'smalleditor'])
.controller('EditorController', ['$scope', function($scope) {
  $scope.$watch('editorApi', function(editor) {
    // Get current data model
    var baseDataModel = editor.dataModel();

    // After editing for a while get new data model
    var currentDataModel = editor.dataModel();

    // Compute delta between baseDataModel and currentDataModel
    var delta = editor.computeDelta(baseDataModel, currentDataModel);

    // Apply that delta to any revision to get next revision
    editor.applyDelta(nRevision, nDelta);
  });
}]);
{% endhighlight %}

The author cites [MediumEditor](https://github.com/daviferreira/medium-editor), which is a similar project that is more focused on the UI and less on the revision tracking aspect.

Yet another alternative is the [Pen Editor](https://github.com/sofish/pen) -- the nice thing about Pen is it supports Markdown.
