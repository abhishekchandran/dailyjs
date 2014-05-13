---
layout: post
title: "Wordchain: An AngularJS/Firebase Word Game"
author: "Alex Young"
categories:
- games
- firebase
- angular
---

<div class="image">
  <img src="/images/posts/wordchain.png" />
  <small>Wordchain</small>
</div>

[Wordchain](http://sonnylazuardi.github.io/wordchain/#/login) (GitHub: [sonnylazuardi / wordchain](https://github.com/sonnylazuardi/wordchain), License: _MIT_) by Sonny Lazuardi is a multiplayer word game made with Firebase, AngularJS, the Google Dictionary API, and the Wikitionary API.  It allows you to sign in with Facebook, and complete words in a crossword-like manner.

[The code](https://github.com/sonnylazuardi/wordchain/tree/gh-pages/js) is all modular, dependency-injected Angular classes, so it's fairly easy to see how it fits together.  The main game logic is in [js/controllers.js](https://github.com/sonnylazuardi/wordchain/blob/gh-pages/js/controllers.js).  Here's the dictionary API search:

{% highlight javascript %}
$scope.search = function() {
  angular.element('.loader').fadeIn(1000);
  $.get('https://www.googleapis.com/scribe/v1/research?key=AIzaSyDqVYORLCUXxSv7zneerIgC2UYMnxvPeqQ&dataset=dictionary&dictionaryLanguage=en&query='+$scope.word, function(data) {
    console.log(data);
    angular.element('.loader').fadeOut(1000);
    $scope.definitions = data.data[0].dictionary.definitionData;
    $scope.$apply();
  }, 'jsonp');
};
{% endhighlight %}

The readme has some details on running it locally, once you've got set up with [Firebase](https://www.firebase.com/).
