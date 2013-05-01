---
layout: post
title: "Node Roundup: Caterpillar, squel, mongoose-currency"
author: "Alex Young"
categories: 
- node
- modules
- sql
- databases
- mongo
- mongoose
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Caterpillar

Benjamin Lupton sent in Caterpillar (GitHub: [bevry / caterpillar](https://github.com/bevry/caterpillar), License: _MIT_, npm: [caterpillar](https://npmjs.org/package/caterpillar)), which is a logging system.  It supports RFC-standard log levels, but the main reason I thought it was interesting is it's based around the _streams2_ API.

By piping a Caterpillar stream through a suitable instance of `stream.Transform`, you can do all kinds of cool things.  For example, [caterpillar-filter](https://github.com/bevry/caterpillar-filter) can filter out unwanted log levels, and [caterpillar-human](https://github.com/bevry/caterpillar-human) adds fancy colours.

###squel

I was impressed by Brian Carlson's [sql](https://npmjs.org/package/sql) module, and Ramesh Nair sent in squel (GitHub: [hiddentao / squel](https://github.com/hiddentao/squel), License: _BSD_, npm: [squel](https://github.com/hiddentao/squel)) which is a similar project.  This SQL builder module supports non-standard queries, and has good test coverage with Mocha.

Ramesh has included some client-side examples as well, which sounds dangerous but may find uses, perhaps by generating SQL fragments to be used by an API that safely escapes them, or for generating documentation examples.

###mongoose-currency

mongoose-currency (GitHub: [catalystmediastudios / mongoose-currency](https://github.com/catalystmediastudios/mongoose-currency), License: _MIT_, npm: [mongoose-currency](https://npmjs.org/package/mongoose-currency)) by Paul Smith adds currency support to Mongoose.  Money values are stored as an integer that represents the lowest unit of currency (pence, cents).  Input can be a string that contains a currency symbol, commas, and a decimal.

The `Currency` type works by stripping non-numerical characters.  I'm not sure if this will work for regions where numbers use periods or spaces to separate groups of digits -- it seems like this module would require localisation support to safely support anything other than dollars.

Paul has included unit tests written with Mocha, so it could be extended to support localised representations of currencies.
