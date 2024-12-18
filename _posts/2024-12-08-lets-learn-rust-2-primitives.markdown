---
layout: post
title:  "Let's Learn Rust 2 - Primitives"
date:   2024-12-08 07:06:58 +0700
categories: jekyll update
---
There are two types of primitives in Rust:
1. Scalar
2. Compound

## Scalar
* Signed Integers: `ix` (x = 8,16,32,64,128,size)
* Unsigned Integers: `ux` (x = 8,16,32,64,128,size)
* Floats: `fx` (x = 32,64)
* `char`: `'a'`
* `bool`: `true` or `false`
* The unit type `()`. Only possible value is an empty tuple `()`

## Compound
* Tuples: `(1, true)`
* Arrays: `[1, 2, 3]`
* Slices: `&[1, 2, 3]`

### Tuples
A collection of values of different types.
```rust
let long_tuple = (1u8, 2u16, 3u32, 4u64,
                    -1i8, -2i16, -3i32, -4i64,
                    0.1f32, 0.2f64,
                    'a', true);

// Accessing tuple
println!("Long tuple first value: {}", long_tuple.0);
println!("Long tuple second value: {}", long_tuple.1);
```

### Arrays
A collection of objects of the same type.
```rust
let xs: [i32; 5] = [1, 2, 3, 4, 5];

// All elements can be initialized to the same value.
let ys: [i32; 500] = [0; 500];

// Accessing array
println!("First element of the array: {}", xs[0]);
println!("Second element of the array: {}", xs[1]);
```

### Slices
Reference to elements in a collection.
```rust
let numbers = [1, 2, 3, 4, 5];

let slice = &array[1..3];
```

## Annotation
```rust
// Annotation

// let name: type = val;
let logical: bool = true; // Regular

// let name = valtype;
let an_integer = 5i32; // Suffix

// let name = val
let default_float = 3.0; // Default
```

[rust-by-example]: https://doc.rust-lang.org/stable/rust-by-example/
[install-rust]: https://www.rust-lang.org/tools/install
[cargo-reference]: https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/cargo/guide/creating-a-new-project.html