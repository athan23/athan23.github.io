---
layout: post
title:  "Let's Learn Rust 5 - Types"
date:   2024-12-11 16:48:01 +0700
categories: jekyll update
---
## Casting
Rust provides explicit type conversion (casting) by using the `as` keyword.

```rust
let decimal = 65.4321_f32;
let integer = decimal as u8;
let character = integer as char;

println!("Casting: {} -> {} -> {}", decimal, integer, character);
// 65.4321 -> 65 -> A
```
## Literals
Numerical literals can be type annotated by adding the type as a suffix.

```rust
// Suffixed literals, their types are known at initialization
let x = 1u8;
let y = 2u32;
let z = 3f32;

// Unsuffixed literals, their types depend on how they are used
let i = 1;
let f = 1.0;
```
## Inference
Type inference looks at how the variable is used
```rust
let elem = 5u8;
let mut vec = Vec::new();

vec.push(elem);
// Now the compiler knows that `vec` is a vector of `u8`s (`Vec<u8>`)
```
## Aliasing
`type` statement can be used to give a new name to an existing type. Types must have `UpperCamelCase` names.

```rust
type NanoSecond = u64;
type Inch = u64;
type U64 = u64;

fn main() {
    let nanoseconds: NanoSecond = 5 as u64;
    let inches: Inch = 2 as U64;
}
```