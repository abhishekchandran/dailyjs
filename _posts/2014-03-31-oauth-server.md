---
layout: post
title: "Building a Node OAuth2 Server"
author: Alex Young
categories:
- node
- oauth2
- authentication
---

Most of you have probably written an OAuth2 client using Node.  I've used the [passport](https://www.npmjs.org/package/passport) module for Express and found it worked very nicely.  But what about creating an OAuth2 server?

Writing a server takes more work, but as long as you're clear about the authorisation flows that you want to use then it's certainly possible.  [Erica Salvaneschi](https://twitter.com/EricaLeCat) wrote [Building a Node OAuth2 server](http://blog.papersapp.com/oauth-server-in-node-js/), a post about our experiences building an OAuth2 service for a commercial project we're working on at Papers:

> This article is a walkthrough of Papers' test-driven implementation of an OAuth server using Node.
> We decided to go for what's known as resource owner password flow and chose node-oauth2-server to build our server.

The sample code was written using test-driven development, and depends on Express, Mongoose, bcrypt, and Mocha and SuperAgent for testing.  We've kept the issues open on the sample code so you can give us feedback, which we're interested in seeing as we're new to OAuth2.
