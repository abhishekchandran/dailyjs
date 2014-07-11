---
layout: post
title: "Route360, ngVideo"
author: "Alex Young"
categories:
- maps
- video
- angularjs
---

###Route360

![Route360](/images/posts/route360.png)

The [Route360 JavaScript API](http://developers.route360.net/) (GitHub: [route360 / r360-js](https://github.com/route360/r360-js), License: _MIT_, Bower: _route360_) by Henning Hollburg and Daniel Gerber is a library for [Leaflet](http://leafletjs.com/) that adds some cool features:

* Generate polygons for reachable areas based on a point on the map
* Supported for walk, car, bike and transit routing
* Map controls: travel time slider, date and time chooser, and travel type chooser
* Routing information from source to destination, including travel time and transit trips
* Support for elevation data

This is a snippet of the polygon API:

{% highlight javascript %}
var cpl = r360.route360PolygonLayer();
map.addLayer(cpl);

var travelOptions = r360.travelOptions();
travelOptions.addSource(marker);
travelOptions.setTravelTimes([300, 600,900, 1200, 1500, 1800]);

r360.PolygonService.getTravelTimePolygons(travelOptions, function(polygons) {
  cpl.addLayer(polygons);
  map.fitBounds(cpl.getBoundingBox()
});
{% endhighlight %}

###ngVideo

[ngVideo](http://ng-video.herokuapp.com/) (GitHub: [Wildhoney / ngVideo](https://github.com/Wildhoney/ngVideo), License: _MIT_) by Adam Timberlake is a set of AngularJS directives for working with video.  Videos are wrapped in an `ng-video` container:

{% highlight html %}
<section class="video" ng-video>
{% endhighlight %}

And should contain a `video` element.  It includes a service which you can use to attach videos:

{% highlight javascript %}
myApp.controller('VideoController', ['$scope', 'video', function($scope, video) {
  video.addSource('mp4', 'http://www.example.com/alice-in-wonderland.mp4');
}]);
{% endhighlight %}

The project includes a lot of other directives for handling buffering, UI controls, data about play position and elapsed time, full screen support, and playlists.
