---
layout: post
title: "Angular Grid, React Native Introduction"
image: "/images/posts/angulargrid.png"
author: Alex Young
categories:
- react
- react-native
- angular
- ui
---

###Angular Grid

![Angular Gird](/images/posts/angulargrid.png)

Niall Crosby sent in [Angular Grid](http://www.angulargrid.com) (GitHub: [ceolter/angular-grid](https://github.com/ceolter/angular-grid/), License: _MIT_), a library for managing tables of data with Angular.  It supports sorting, filtering, column resizing, CSS themes, and search.  There's even an example that extends the cell renderer to show a file browser view.

Like other data tables, you can specify the columns with JSON and then fetch JSON data from the server to populate the table.  Here's a short Angular example that uses `$http` to fetch the JSON:

{% highlight javascript %}
module.controller('tableController', function($scope, $http) {
  var columnDefs = [
    { displayName: 'Athlete', field: 'athlete', width: 150 },
    { displayName: 'Age', field: 'age', width: 90 },
    { displayName: 'Country', field: 'country', width: 120 },
    { displayName: 'Year', field: 'year', width: 90 },
    { displayName: 'Total', field: 'total', width: 100}
  ];

  $scope.gridOptions = {
    columnDefs: columnDefs,
    rowData: []
  };

  $http.get('olympicWinners.json')
    .then(function(res){
      $scope.gridOptions.rowData = res.data;
      $scope.gridOptions.api.onNewRows();
    });
});
{% endhighlight %}

There are more examples available in the [documentation for Angular Grid](http://www.angulargrid.com/documentation.php).

###React Native Introduction Tutorial

John Wu has written an introduction to [using React Native with iOS apps](http://blog-en.leapoahead.com/post/use-react-native-in-existing-ios-app).  It includes details on how to use it with CocoaPods, and how to wire up the JavaScript view code.

If you're new to Objective-C and just want to get React Native up and running, then this should help because it walks through all of the necessary setup details.  Installing CocoaPods isn't too hard (it's an Objective-C package manager), so as long as you can compile and run basic iOS apps you should be good to go.  There's also a [sample application on GitHub](https://github.com/tjwudi/EmbededReactNativeExample).
