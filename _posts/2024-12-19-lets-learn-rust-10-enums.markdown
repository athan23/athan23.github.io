---
layout: post
title:  "Let's Learn Rust 10 - Enums"
date:   2024-12-19 23:48:17 +0700
categories: jekyll update
---
More on enums.
```rust
enum IpAddrKind {
    V4,
    V6,
}
```
We can create instances of enums
```rust
fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;
}
```
We can define a function that takes any IpAddrKind
```rust
fn route(ip_kind: IpAddrKind) {}
```
We can attach data to each variant of the enum
```rust
struct Ipv8Addr {}

enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
    V8(Ipv8Addr),
}

let v4 = IpAddr::V4(127, 0, 0, 1);
let v6 = IpAddr::V6(String::from("::1"));
let v8 = IpAddr::V6(Ipv8Addr::new());
```
Similar to struct, we can define methods on enums.
```rust
impl IpAddr {
    fn call(&self) {

    }
}

let v4 = IpAddr::V4(127, 0, 0, 1);
v4.call();
```

## [`Option`][option-enum] Enum
A value could be something or nothing.
Rust doesn't have `Null` value.
[`Option`][option-enum] enum encodes the concept of a value being present or absent.
```rust
let some_number = Some(5);
let some_char = Some('e');

let absent_number: Option<i32> = None;
```
[option-enum]: https://www.rust-lang.org/tools/install