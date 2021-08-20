---
description: Get Beginner to Advanced Level Resources for Rust Programming Language
---

# Rust Learning Resources

![](../../.gitbook/assets/rust-programming-language.png)

[**Rust**](https://www.rust-lang.org/learn) is a multi-paradigm programming language designed for performance and safety, especially safe concurrency. Rust achieves memory safety without garbage collection, and reference counting is optional.  
The concrete syntax of Rust is similar to C and C++, with blocks of code delimited by curly brackets, and control flow keywords such as `if`, `else`, `while`, and `for`, although the specific syntax for defining functions is more similar to Pascal. Not all C or C++ keywords are implemented, however, and some Rust functions \(such as the use of the keyword `match` for pattern matching\) will be less familiar to those versed in these languages.

Rust is intended to be a language for highly concurrent and highly safe systems, which makes it a natural choice for blockchain programming - both in terms of writing protocols and smart contracts.

Following these resources will present you with ample opportunity to learn the language and put it into practice. There will be specific guides aimed at the Proof of Stake networks which utilize Rust added to this list soon.

The Rust Language Cheat Sheet has a good section of [Coding Guides](https://cheats.rs/#coding-guides) and overall is quite useful.

## Beginner

* [Ferrous Teaching Material](https://ferrous-systems.github.io/teaching-material/) - Covers Beginner to Advanced topics with slideshows
* [Rust 101](https://www.ralfj.de/projects/rust-101/main.html) Guide and Tutorial
* [Video](https://youtu.be/agzf6ftEsLU) - Intro to the Rust programming language
* [Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/intro.html) 
* [The Rust Book](https://doc.rust-lang.org/stable/book/) - Important and relevant piece of Rust documentation, from beginner to advanced.
* [Tour of Rust](https://tourofrust.com/index.html) - Step by step guide through the features of the Rust programming language
* [Rust by Example](https://doc.rust-lang.org/rust-by-example/) \(RBE\) is a collection of runnable examples that illustrate various Rust concepts and standard libraries.
* [Writing Rust in Easy English](https://dhghomon.github.io/easy_rust/Chapter_3.html), a Complete Beginner to Intermediate Rust Guide
* [A Gentle Introduction to Rust](https://stevedonovan.github.io/rust-gentle-intro/) - Steve Donovan covers Beginner to Intermediate Rust
* [24 Days Of Rust](http://zsiciarz.github.io/24daysofrust/index.html) - An older resource from 2014 - 2016 but still worth a read
* [What is Rust and why Rust?](https://www.oreilly.com/content/why-rust/) by O'Reilly
* [This Week in Rust](https://this-week-in-rust.org/) - curated newsletter with latest articles, news and updates from the Rust community.
* [The Rust subreddit](https://www.reddit.com/r/rust/) - a place for all things Rust: from beginner questions to advanced low level concepts, game development, wasm, web frameworks, etc.;

## Intermediate

* Introduction to Rust by Ryan Levick - [Part 1](https://youtu.be/WnWGO-tLtLA) & [Part 2](https://youtu.be/lLWchWTUFOQ)
* The Rust Programming Language by Knowledge Hub - [Video Series Playlist](https://youtube.com/playlist?list=PL7Y5Yox90r8M9yVblJ2ey_2RHo0frcUsX)
* Introduction to Rust from basic to advanced by Tensor Programming - [Video Series Playlist](https://youtube.com/playlist?list=PLJbE2Yu2zumDF6BX6_RdPisRVHgzV02NW)
* Rust Programming Tutorials by dcode - [Video Series Playlist](https://youtube.com/playlist?list=PLVvjrrRCBy2JSHf9tGxGKJ-bYAN_uDCUL)
* Learn the fundamentals of the Rust language in this[ Rust Crash Course](https://www.youtube.com/watch?v=zF34dRivLOw) by Traversy Medi[a ](https://www.youtube.com/watch?v=zF34dRivLOw)
* [Crust of Rust](https://youtube.com/playlist?list=PLqbS7AVVErFiWDOAVrPt7aYmnuuOLYvOa) is a video series which makes intermediate Rust concepts understandable by diving into real examples and working code
* An introduction to the Rust programming language through[ implementing a hashmap](https://youtu.be/DWNyZXUC1u4)
* [Michael F. Bryan](https://adventures.michaelfbryan.com/tags/rust/)'s articles on Rust
* Cheat sheet for [common types and what they convert into](https://upsuper.github.io/rust-cheatsheet/)

## Advanced

* How to build a blockchain-based cryptocurrency using Rust - [Video Series Playlist](https://youtube.com/playlist?list=PLwnSaD6BDfXL0RiKT_5nOIdxTxZWpPtAv)
* Learning Rust: [Let's Build a Parser!](https://codeandbitters.com/lets-build-a-parser/)
* Building a DNS server in Rust, check on [GitHub](https://github.com/EmilHernvall/dnsguide)
* Building a Rust Web Browser - [Check Here](https://joshondesign.com/tags/browser)
* [PNGme](https://picklenerd.github.io/pngme_book/): An Intermediate Rust Project
* [Hecto](https://www.philippflenker.com/hecto/): Build your own text editor in Rust
* Writing a file system from scratch in Rust - [Check Here](https://blog.carlosgaldino.com/writing-a-file-system-from-scratch-in-rust.html)
* [Good Practices](https://pascalhertleif.de/artikel/good-practices-for-writing-rust-libraries/) for Writing Rust Libraries
* So You Want to Build a Language VM - [Check Here](https://blog.subnetzero.io/post/building-language-vm-part-00/)

## Network Specific

* Solana : [Developing with Rust](https://docs.solana.com/developing/on-chain-programs/developing-rust)
  * Uses the `bpfel-unknown-unknown` target triple, compiles to Berkeley Packet Format `.so` 
  * Check out the [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)
  * Learn more about [parameter de-serialization](https://docs.solana.com/developing/on-chain-programs/developing-rust#parameter-deserialization) & data types
  * [Example programs](https://github.com/solana-labs/solana-program-library/tree/master/examples/rust) for further study 
* NEAR : [Getting Started](https://docs.near.org/docs/develop/contracts/rust/intro#getting-started)
  * Uses the `wasm32-unknown-unknown` target triple, compiles to WebAssembly `.wasm`
  * Check out the[ NEAR CLI](https://docs.near.org/docs/tools/near-cli)
  * Learn more about the [NEAR SDK](https://docs.near.org/docs/develop/contracts/rust/near-sdk-rs) \(see also: [docs.rs](https://docs.rs/near-sdk/3.1.0/near_sdk/)\)
  * Check out the Learn tutorial - [Write and deploy a smart contract in Rust](https://learn.figment.io/network-documentation/near/tutorials/write-and-deploy-a-smart-contract-on-near)

