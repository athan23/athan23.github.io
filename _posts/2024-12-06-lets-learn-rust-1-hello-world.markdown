---
layout: post
title:  "Let's Learn Rust 1 - Hello World"
date:   2024-12-06 11:35:43 +0700
categories: jekyll update
---
Welcome to my Let's Learn Rust series. I will be following this guide [Rust By Example][rust-by-example] and summarize what I learn. I will not be touching much on the coding portion since the code is already explained in the website. Without further ado, let's begin! 🚀

First of all, we need to [install rust][install-rust]. `rustc`, `cargo`, and `rustup` will be installed.

* `rustc` is the compiler for Rust. We will not be calling this command since `cargo` calls `rustc`.

* `cargo` is Rust package manager. It downloads package dependencies, compiles packages, makes distributable packages, and uploads them to crates.io.

* `rustup` installs Rust. It allows us to switch compilers versions and keeps them updated.

To create a new Rust project, use `cargo new hello_world`.

To run the program, use `cargo run`.

The program should print out
```sh
Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.05s
     Running `target/debug/hello_world`
Hello, world!
```

For more details about cargo, check this [reference][cargo-reference].

[rust-by-example]: https://doc.rust-lang.org/stable/rust-by-example/
[install-rust]: https://www.rust-lang.org/tools/install
[cargo-reference]: https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/cargo/guide/creating-a-new-project.html