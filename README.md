ozone
=====
Ozone is a pure-[rust](http://www.rust-lang.org/) key/value store based on [BoltDB](https://github.com/boltdb/bolt) and inspired by the language's built-in concept of memory ownership.


Goals
-----
The goal of this project is to build a perfectly idiomatic persistence layer using the standard library's [collections::BTreeMap](https://doc.rust-lang.org/collections/struct.BTreeMap.html) as a model, letting the language itself do as much as possible.

Specific features that will be implemented include:

- single-file databases
- copy-on-write, lock-free MVCC
- recycling of emptied pages

This is my first real Rust project, so any hints, suggestions, and nudges are very welcome.




Proposed API
------------
I'm starting as simple as possible, but this will change 

```rust
// Open a database file (creating if nonexistant)
let db = ozone::open("my.db").unwrap();

// DB is essentially a collections::BTreeMap<&str, Bucket>
let mut bucket : Bucket = db.entry("bucket-name");

// Bucket is essentially a collections::BTreeMap<&str, &str>
let old_value : Option<str> = bucket.insert("key-name", "value");

// Bucket is essentially a collections::BTreeMap<&str, &str>
let value : Option<str>  = bucket.get("key-name");
```



Why The Name?
-------------

Ozone, or O<sub>3</sub> is a powerful oxidant (oxidation/reduction is the chemical process of rusting) that is naturally created from O<sub>2</sub> (the stuff we breathe) when a *bolt* of lightning strikes.



Disclaimer
----------
I'm writing this to glean a deeper understanding of persistant storage techniques and to get more experience with Rust. Don't even think about using this in production :)
