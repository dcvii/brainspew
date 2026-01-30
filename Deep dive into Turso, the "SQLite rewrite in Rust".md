---
title: "Deep dive into Turso, the \"SQLite rewrite in Rust\""
source: "https://kerkour.com/turso-sqlite"
author:
  - "[[Sylvain Kerkour]]"
published: 2026-01-27
created: 2026-01-29
description: "I love Rust and I love SQLite, so you can guess. Iwas pretty excited when I lerned that \"SQLite was rewritten in Rust\" What is SQLite, actually? 2 things: a"
tags:
  - "clippings"
---
I love Rust and I love SQLite, so you can imagine that I was pretty excited when I learned that "SQLite was being rewritten in Rust": [Turso](https://github.com/tursodatabase/turso).

[SQLite is probably the most deployed database in the world](https://kerkour.com/sqlite-for-servers), with dozens of databases on any of your devices and is probably one of the most reliable piece of software in existence, with 590 times more tests than code (I know that tests are code, it's to simplify): [~92,053,100 lines of tests vs ~155,800 lines of code](https://sqlite.org/testing.html).

Furthermore, there are SQLite bindings for virtually any programming language, so why would anybody want to rewrite it in Rust?

## What is SQLite, anyway?

When we talk about SQLite, most people first think about the C library, its reliability, legendary test coverage and ease of embedding.

But, SQLite can also be seen as a specification for a single-file database format, and this is where things become interesting. A SQLite database is mostly an ultra-optimized collection of B+Trees stored on disk (or in memory) with a schema and some metadata.

What if we had other database engines that could talk this file format? This is exactly what Turso is: a new database engine that is (mostly, with very few exceptions such as the MVCC mode) compatible with the SQLite database file format but is completely different on the architectural side.

The user experience is also the same, at least in Rust, here is a Hello World:

```
use turso::{Builder, EncryptionOpts};

#[tokio::main]
async fn main() -> Result<(), anyhow::Error> {
    let db = Builder::new_local("test.db").build().await?;
    let conn = db.connect()?;

    let rows = conn.query("SELECT * FROM users", ()).await?;

    return Ok(());
}
```

## SQLite is great, but has many problems

Indeed, while it is a piece of art, SQLite also has many problems biting unsuspecting developers.

First, there is the fact that the SQLite test suite is not open source, thus people who would want to modify it can't do it with the same peace of mind as the original developers.

Second, the SQLite developers don't really accept external contributions. On one hand you can report bugs which will be fixed promptly and request features, but it may not be enough for your situation.

Finally, SQLite is written in C which makes it prone to easily-avoidable bugs as can attest the [changelog](https://sqlite.org/changes.html), and also makes it really hard to maintain and add new features due to C's poor type system and unsafe memory management.

Among other things, SQLite doesn't (officialy) support concurrent writes, SQLite's columns are by default weakly typed, which is not what you can expect from a database, and schema changes [can be a pain in the ars](https://sqlite.org/lang_altertable.html) where you need to copy the entire table yourself for some operations.

## ... most of which can be fixed by a rewrite in Rust

In [*Why Is SQLite Coded In C*](https://sqlite.org/whyc.html), D. Richard Hipp hints that Rust would be the best candidate to rewrite SQLite, but that it currently doesn't meet all the requirements because SQLite is deployed in really exotic places where Rust code can't be deployed today.

I see this situation trhough the prism of the innovator's dilemma: the incumbent is not willing to sacrifice a part of its market to evolve, so we need a new player to come and innovate.

Turso innovates: even before reaching v1.0, they already have fixed most of the long-standing pain points experienced by developers using SQLite that have been covered in [*Optimizing SQLite for servers*](https://kerkour.com/sqlite-for-servers):

- [Built-in encryption](https://github.com/tursodatabase/turso/blob/main/core/storage/encryption.rs), which is table stake in 2020+
- [MVCC and concurrent writes support](https://github.com/tursodatabase/turso/blob/main/core/mvcc/mod.rs)
- [Async I/O with io\_uring](https://github.com/tursodatabase/turso/blob/main/core/io/io_uring.rs)

And this is before talking about all the other perks provided by Rust such as memory safety and high-level code with clean abstractions.

## An in-process database that can scale to multiple machines

One of the most misunderstood features of Turso is that it has been designed to be used as an in-process database, but also as a networked database like PostgreSQL, so the company behind it can sell a cloud hosted solution.

![In-process vs networked database](https://kerkour.com/assets/2026/01/in_process_vs_networked_database.png)

As a developer and entrepreneur, this is my dream database: out of 10 projects, 9 will never need more than a single VM so the in-process model of SQLite / Turso is a great fit. But then, for the single project that gets traction and needs to scale, [as I've previously covered](https://kerkour.com/sqlite-for-servers), SQLite is a bad fit as it doesn't support concurrent writes, and porting an application from SQLite to Postgres is not a great use of your precious time when you are scaling a project.

That's why most projects start directly with PostgreSQL, "just in case", which adds friction during development and operations, especially when you need to manage extensions, upgrade the database's version or manage backups.

A database that can scale from in-process to networked is badly needed, but very few people know that they need a car / train instead of a faster horse.

This is especially true in the agentic era where agents work in their own sandboxes and you don't want the overhead of having to spin a new database for each session, or for projects that need both an embedded database for a local application and a database for the backend.

## Extensions

One of SQLite's best features is how easy it is to build and load custom extensions. Take a look at my previous article [*Building SQLite extensions in Rust*](https://kerkour.com/sqlite-extension-rust) to learn why and how to build fast and secure SQLite extensions in Rust.

Turso already supports extensions and provides [an SDK to write extensions in Rust](https://crates.io/crates/turso_ext).

Here is a short snippet from [https://github.com/tursodatabase/turso/blob/main/extensions/crypto/src/lib.rs](https://github.com/tursodatabase/turso/blob/main/extensions/crypto/src/lib.rs) to show you how easy it is to build extensions for Turso.

```
#[scalar(name = "crypto_sha256", alias = "crypto_sha256")]
fn crypto_sha256(args: &[Value]) -> Value {
    if args.len() != 1 {
        return Value::error(ResultCode::Error);
    }

    let Ok(hash) = sha256(&args[0]) else {
        return Value::error(ResultCode::Error);
    };

    Value::from_blob(hash)
}
```

## Closing Thoughts

Turso is the database I've been waiting for a long time! I don't know them, but the team looks solid, so I wish them good luck and I'm (im)patiently waiting for a v1.0.

With [DuckDB](https://duckdb.org/) for analytical data and time series, and Turso for transactional data, I feel that we are finally back to sanity, after many years of distributed systems craze.

The timing is great for them as embedded databases are the perfect fit for AI agents, so I hope that they will be able to pull it in time and make good money by themselves so they don't need to sell the company, which is often a risk for VC-backed companies.

If you want to learn backend development with Rust, take a look at my article [Architecting and building medium-sized web services in Rust with Axum, SQLx and PostgreSQL](https://kerkour.com/rust-web-services-axum-sqlx-postgresql). If you want to learn embedded development, take a look at [Introduction to embedded development with Rust: Overview of the ecosystem](https://kerkour.com/introduction-to-embedded-development-with-rust).

If you want to learn how to do black-wizard things such as applied cryptography, security engineering, how to write secure and production-ready Rust code, take a look at my book **[Black Hat Rust](https://kerkour.com/black-hat-rust)** where, among other things, you will build an end-to-end encrypted Remote Access Tool, exploits and a web server in Rust.

**Tags:**

---

[![Black Hat Rust cover](https://kerkour.com/assets/books/black-hat-rust/black_hat_rust_cover.svg)](https://kerkour.com/black-hat-rust)

[Want to learn Rust, offensive security and applied cryptography? Take a look at my book **Black Hat Rust** where, among other things, you will build your own end-to-end encrypted protocol, a Remote Access Tool, craft shellcodes and exploits and many other applied projects to get your hands dirty.  
Special Promotion: ~~50 €~~ 30 € Special Promotion: ~~$50~~ $30  
0d 23h 52m 16s](https://kerkour.com/black-hat-rust)