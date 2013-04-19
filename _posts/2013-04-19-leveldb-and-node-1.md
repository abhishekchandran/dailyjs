---
layout: post
title: "LevelDB and Node: What is LevelDB Anyway?"
author: Rod Vagg
categories: 
- node
- leveldb
- databases
---

This is the first article in a three-part series on LevelDB and how it can be used in Node.

This article will cover the LevelDB basics and internals to provide a foundation for the next two articles. The second and third articles will cover the core LevelDB Node libraries: [LevelUP](https://github.com/rvagg/node-levelup), [LevelDOWN](https://github.com/rvagg/node-leveldown) and the rest of the LevelDB ecosystem that's appearing in Node-land.

![LevelDB](/images/posts/leveldb.png)

### What is LevelDB?

LevelDB is an *open-source*, *dependency-free*, *embedded key/value data store*. It was developed in 2011 by Jeff Dean and Sanjay Ghemawat, researchers from Google. It's written in C++ although it has third-party bindings for most common programming languages. Including JavaScript / Node.js of course.

LevelDB is based on ideas in Google's BigTable but does not share code with BigTable, this allows it to be licensed for open source release. Dean and Ghemawat developed LevelDB as a replacement for SQLite as the backing-store for Chrome's IndexedDB implementation.

It has since seen very wide adoption across the industry and serves as the back-end to a number of new databases and is now the recommended storage back-end for Riak.

### Features

 * **Arbitrary byte arrays**: both keys and values are treated as simple arrays of bytes, so content can anything from ASCII strings to binary blobs.
 * **Sorted by keys**: by default, LevelDB stores entries lexicographically sorted by keys. The sorting is one of the main distinguishing features of LevelDB amongst similar embedded data storage libraries and comes in very useful for querying as we'll see later.
 * **Compressed storage**: Google's Snappy compression library is an optional dependency that can decrease the on-disk size of LevelDB stores with minimal sacrifice of speed. Snappy is highly optimised for fast compression and therefore does not provide particularly high compression ratios on common data.
 * **Basic operations: `Get()`, `Put()`, `Del()`, `Batch()`**

### Basic architecture

#### Log Structured Merge (LSM) tree

![LSM](/images/posts/leveldb_simple.png)

All writes to a LevelDB store go straight into a **log** and a "memtable". The log is regularly **flushed** into sorted string table files (SST) where the data has a more permanent home.

Reads on a data store **merge** these two distinct data structures, the log and the SST files. The SST files represent mature data and the log represents new data, including delete-operations.

A configurable <b>cache</b> is used to speed up common reads. The cache can potentially be large enough to fit an entire active working set in memory, depending on the application.

#### String Sorted Table files (SST)

Each SST file is limited to ~2MB, so a large LevelDB store will have many of these files. The SST file is divided internally into 4K **blocks**, each of which can be read in a single operation. The final block is an **index** that points to the start of each data block and its the key of the entry at the start of the block. A **Bloom filter** is used to speed up lookups, allowing a quick scan of an index to find the block that *may* contain the desired entry.

Keys can have **shared prefixes** within blocks. Any common prefix for keys within a block will be stored once, with subsequent entries storing just the unique suffix. After a fixed number of entries within a block, the shared prefix is **"reset"**; much like a keyframe in a video codec. Shared prefixes mean that verbose namespacing of keys does not lead to excessive storage requirements.

#### Table file hierarchy

The table files are not stored in a simple sequence, rather, they are organised into a series of **levels**. This is the *"Level"* in LevelDB.

Entries that come straight from the log are organised in to Level 0, a set of up to 4 files. When additional entries force Level 0 above the maximum of 4 files, one of the SST files is chosen and merged with the SST files that make up Level 1, which is a set of up to 10MB of files. This process continues, with levels overflowing and one file at a time being merged with the (up to 3) overlapping SST files in the next level. Each level beyond Level 1 is 10 times the size of the previous level.

<table>
<tbody>
<tr>
<th style="text-align: right; font-weight: bold;">Log:</th>
<td style="padding-left: 0.5em;">Max size of 4MB (configurable), then flushed into a set of Level 0 SST files</td>
</tr>
<tr>
<th style="text-align: right; font-weight: bold;">Level&nbsp;0:</th>
<td style="padding-left: 0.5em;">Max of 4 SST files, then one file compacted into Level 1</td>
</tr>
<tr>
<th style="text-align: right; font-weight: bold;">Level&nbsp;1:</th>
<td style="padding-left: 0.5em;">Max total size of 10MB, then one file compacted into Level 2</td>
</tr>
<tr>
<th style="text-align: right; font-weight: bold;">Level&nbsp;2:</th>
<td style="padding-left: 0.5em;">Max total size of 100MB, then one file compacted into Level 3</td>
</tr>
<tr>
<th style="text-align: right; font-weight: bold;">Level&nbsp;3+:</th>
<td style="padding-left: 0.5em;">Max total size of 10 x previous level, then one file compacted into next level</td>
</tr>
</tbody>
</table>

0 ↠ 4 SST, 1 ↠ 10M, 2 ↠ 100M, 3 ↠ 1G, 4 ↠ 10G, 5 ↠ 100G, 6 ↠ 1T, 7 ↠ 10T

![Levels](/images/posts/leveldb_levels.png)

This organisation into levels minimises the reorganisation that must take place as new entries are inserted into the middle of a range of keys. Each reorganisation, or "compaction", is restricted to a just a small section of the data store. The hierarchical structure generally leads to data in the higher levels being the most mature data, with the fresher data being stored in the log and the initial levels. Since the initial levels are relatively small, overwriting and removing entries incurs less cost than when it occurs in the higher levels, but this matches the typical database where you have a large set of mature data and a more volatile set of fresh data (of course this is not always the case, so performance will vary for different data write and retrieve patterns).

A **lookup** operation must also traverse the levels to find the required entry. A read operation that requests a given key must first look in the log, if it is not found there it looks in Level 0, moving up to Level 1 and so forth. In this way, a lookup operation incurs a minimum of one read per level that must be searched before finding the required entry. A lookup for a key that does not exist must search every level before a definitive "NotFound" can be returned (unless a Del operation is recorded for that key in the log).
### Advanced features

* **Batch operations**: provide a collection of Put and/or Del operations that are **atomic**; that is, the *whole* collection of operations succeed or fail in a single Batch operation.
* **Bi-directional iterators**: iterators can start at any key in a LevelDB store (even if that key does not exist, it will simply jump to the next lexical key) and can move forward and backwards through the store.
* **Snapshots**: a snapshot provides a reference to the state of the database at a point in time. Read-queries (Get and iterators) can be made against specific snapshots to retrieve entries as they existed at the time the snapshot was created. Each iterator creates an implicit snapshot (unless it is requested against an explicitly created snapshot). This means that regardless of how long an iterator is alive and active, the data set it operates upon will always be the same as at the time the iterator was created.

Some details on these advanced features will be covered in the next two articles, when we turn to look at how LevelDB can be used to simplify data management in your Node application.

If you're keen to learn more and can't wait for the next article, see the [LevelUP](https://github.com/rvagg/node-levelup) project on GitHub as this is the focus of much of the LevelDB activity in the Node community at the moment.
