---
layout: post
title: "fake-identity, Leaflet.FreeDraw"
author: "Alex Young"
categories:
- modules
- libraries
- testing
- graphics
- maps
---

###fake-identity

[fake-identity](http://travishorn.github.io/fake-identity/) (GitHub: [travishorn / fake-identity](https://github.com/travishorn/fake-identity), License: _MIT_, npm: [fake-identity](https://www.npmjs.org/package/fake-identity)) by Travis Horn is a library for generating fake identities.  You can use `Identity.generate` to create a single fake object, or `Identity.generate(n)` to get an array of `n` objects.

Here's an example of the output:

{% highlight javascript %}
{
  firstName: "Amelia",
  lastName: "Wright",
  emailAddress: "awright@example.com",
  phoneNumber: "(555) 555-0155",
  street: "7327 Central Avenue",
  city: "Oxford",
  state: "TX",
  zipCode: "75045",
  dateOfBirth: Fri Jul 20 1962 00:00:00,
  sex: "female",
  company: "Contoso Pharmaceuticals",
  department: "Legal"
}
{% endhighlight %}

I find I have to do this quite often for testing.  I usually use [Faker](https://www.npmjs.org/package/Faker) to make users -- in fact, I had to do this very task today!  I think fake-identity would have made my job easier in this case, because the schema I'm using is similar.

###Leaflet.FreeDraw

![Leaflet.FreeDraw](/images/posts/leafletfreedraw.png)

[Leaflet.FreeDraw](http://freedraw.herokuapp.com/) (GitHub: [Wildhoney / Leaflet.FreeDraw](https://github.com/Wildhoney/Leaflet.FreeDraw), License: _MIT_) by Adam Timberlake is a library for [Leaflet](http://leafletjs.com/) that adds support for creating polygons.

> Use Leaflet.draw for drawing pre-defined polygons and linear shapes – Leaflet.FreeDraw's selling point is that it allows you to freely draw a polygon like Zoopla. Hulls are also supported to normalise polygons when users draw an insane polygon – currently Leaflet.FreeDraw supports Brian Barnett's Graham Scan module and my adaptation of the concave hull algorithm.

The readme is pretty solid, and explains how to handle polygon mutation, intersection, and elbow creation.  The demo allows you to draw and edit polygons, with planes flying over the map.

I actually saw a similar polygon drawing UI widget on [Ikea's solar panel quote page](http://www.hanergy.co.uk/go-solar/) today.  You can draw a polygon over your house so it can use the shape to estimate how well solar panels should work for your property.
