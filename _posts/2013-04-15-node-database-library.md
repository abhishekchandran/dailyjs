---
layout: post
title: "The State of Node and Relational Databases"
author: "Alex Young"
categories: 
- databases
- node
- modules
- sql
---

Recently I started work on a Node project that was built using [Sequelize](http://www.sequelizejs.com/) with MySQL.  It was chosen to ease the transition from an earlier version written with Ruby on Rails.  The original's ActiveRecord models mapped quite closely to their Sequelize equivalents, which got things started smoothly enough.

Although Sequelize had some API quirks that didn't feel very idiomatic alongside other Node code, the developers have hungrily accepted pull requests and it's emerging as a reasonable ORM solution.  However, like many others in the Node community I feel uncomfortable with ORM.

Why?  Well, some of us have learned how to use relational databases correctly.  Joining an established project that uses ORM only to find there's no referential integrity or sensible indexes is to be expected these days, as programmers have moved away from caring about databases to application-level schemas.  I've had my head down in MongoDB/Mongoose and Redis code for the last few years, but relational databases aren't going away any time soon so either programmers need to get the hang of them or we need better database modules.

This all prompted me to look at alternative solutions to relational databases in Node.  First, I broke down the problem into separate areas:

* *Driver*: The module that manages database connections, sends queries, and responds with data
* *Abstraction layer*: Provide tools for escaping queries to avoid SQL injection attacks, and wrap multiple drivers so it's easy to port applications between MySQL/PostgreSQL/SQLite
* *Validator*: Validates data against a schema prior to sending it to the database.  Aids with the generation of human-readable error messages
* *Query generator*: Generates SQL queries based on a more JavaScript-programmer-friendly API
* *Schema management*: Keep schema up-to-date when fields are added or removed

Some projects won't need to support all of these areas -- you can mix and match them as needed.  I prefer to create simple veneer-like "model" classes that wrap more low-level database operations.  This works well in a web application where it can be make sense to decouple the HTTP layer from the database.

###Database Driver

The [mysql](https://npmjs.org/package/mysql) and [pg](https://npmjs.org/package/pg) modules are actively maintained, and are usually required by "abstraction layer" modules and ORM solutions.

A note about configuration: when it comes to connecting to the database, I strongly prefer modules that support connection URIs.  It makes it a lot easier to deploy web applications to services like Heroku, because a single environmental variable can be set that contains the connection details for your production database.

###Abstraction Layer

This level sits above the driver layer, and should offer lightweight JavaScript sugar.  There are many examples of this, but a good one is transactions.  Transactions are particularly useful in JavaScript because they can help create APIs that are less dependent on heavily nested callbacks.  For example, it makes sense to model transactions as an `EventEmitter` descendent that allows operations to be pushed to an internal stack.

The author of the pg module, Brian Carlson, who occasionally stops by the `#dailyjs` IRC channel on Freenode, recently mentioned his new [relational](https://npmjs.org/package/relational) project that aims to provide a saner approach to ORM in Node.  This module feels more like an abstraction layer API, but it's gunning to be a formidable new ORM solution.

There are some popular libraries that tackle the abstraction layer, including [any-db](https://npmjs.org/package/any-db) and [massive](https://npmjs.org/package/massive).

###Validator

I usually find myself dealing with errors in web forms, so anything that makes error handling easier is an advantage.  Validation and schemas are closely related, which is why ORM libraries usually combine them.

It's possible to treat them separately, and in the JavaScript community we have solutions based on or inspired by [JSON Schema](http://json-schema.org/).  The [jayschema](https://npmjs.org/package/jayschema) module by Nate Silva is one such project.  It's really aimed at validating JSON, but it could be used to validate JavaScript objects spat out by a database driver.

[Validator](https://npmjs.org/package/validator) has some simple tools for validating data types, but it also has optional [Express middleware](https://github.com/ctavan/express-validator) that makes it easy to drop into a web application.  Another similar project is [conform](https://npmjs.org/package/conform) by Oleg Korobenko.

###Query Generator

The [sql](https://npmjs.org/package/sql) module by Brian Carlson is an SQL _builder_ -- it has a chainable API that turns JavaScript into SQL:

{% highlight javascript %}
user
  .select(user.id)
  .from(user)
  .where(
    user.name.equals('boom').and(user.id.equals(1))
  ).or(
    user.name.equals('bang').and(user.id.equals(2))
  ).toQuery();
{% endhighlight %}

He's using this to build the previously mentioned _relational_ module as well.

###Schema Management

[Sequelize](http://www.sequelizejs.com/) has an API for managing database migrations.  It can migrate to a given version and back, and it can also "sync" a model's schema to the database (creating the table if it doesn't exist).

There are also dedicated migration modules, like [db-migrate](https://npmjs.org/package/db-migrate) by Jeff Kunkle.

###Conclusion

The Node community has created a rich set of modules for working with relational databases, and although there's a strong anti-ORM sentiment interesting projects like [relational](https://npmjs.org/package/relational) are appearing.

Although these modules don't address my concerns about the way in which ORM gets used with apathy towards best practices, it's promising to see lower-level modules that can be used as building blocks for more application-specific solutions.

All of this has come at a time when relational database projects are adapting, changing, and even growing in popularity despite the recent attention the NoSQL movement has been given.  PostgreSQL is going from strength to strength, and Heroku provides it as default.  [MariaDB](https://mariadb.org/) is a drop-in replacement for MySQL that has a [non-blocking Node module](https://npmjs.org/package/mariasql).  SQLite is probably technically growing in usage as it backs Core Data in iCloud applications -- Android developers also use SQLite.

Let other readers know how you deal with SQL-backed Node projects in the comments!
