---
layout: post
title:  "Let's Learn Rust 7 - Flow of Control"
date:   2024-12-15 14:36:05 +0700
categories: jekyll update
---
## if/else
```rust
let n = 1;

if n < 0 { }
else if n > 0 { }
else { }
```
## loop
```rust
let mut n = 1;
loop {
    // To skip the rest of this iteration
    // continue;

    // To break out of loop
    // break;

    // loop can return a value
    // break n * 2;
}
// n is now 2
```

Labeled loop
```rust
'outer:loop {
    'inner:loop {
        // Only break inner loop
        // break;

        // break outer loop
        break 'outer;
    }
}
```
## while
```rust
let n = 1;
while n < 100 {
    n += 1;
}
```
## for range
```rust
for n in 1..100 {
    println!("{}", n);
}
// to include 100,
// for n in 1..=100 {

let names = vec!["Alice", "Bob", "Charlie"];
for name in names.iter() {
    println!("Hello {}", name);
}

// Does not work of into_iter()
println!("names: {:?}", names);

// iter() borrows each element for each iteration
// into_iter() consumes the data for each iteration. Canno
// iter_mut() borrow each element and allows modification
```
## match
Similar to C `switch` statement
```rust
let n = 13;

match n {
    1 => println!("One"),
    2 | 3 | 5| 7 | 11 => println!("Prime"),
    13..=19 => println!("Teen"),
    _ => println!("Not special")
}
```
For more info about destructuring using match, read [this][destructuring].

## if let
Usually for matching enums
```rust
enum Foo {
    Bar,
    Baz,
    Qux(u32)
}

fn main() {
    // Create example variables
    let a = Foo::Bar;
    let b = Foo::Baz;
    let c = Foo::Qux(100);
    
    // Variable a matches Foo::Bar
    if let Foo::Bar = a {
        println!("a is foobar");
    }

    if let Foo::Qux(value) = c {
        println!("c is {}", value);
    }
}
```
## let else
```rust
use std::str::FromStr;

fn get_count_item(s: &str) -> (u64, &str) {
    let mut it = s.split(' ');
    let (Some(count_str), Some(item)) = (it.next(), it.next()) else {
        panic!("Can't segment count item pair: '{s}'");
    };
    let Ok(count) = u64::from_str(count_str) else {
        panic!("Can't parse integer: '{count_str}'");
    };
    (count, item)
}

// The first let-else is equivalent to
let (count_str, item) = match (it.next(), it.next()) {
    (Some(count_str), Some(item)) => (count_str, item),
    _ => panic!("Can't segment count item pair: '{s}'"),
};

// The second one is equivalent to
let count = if let Ok(count) = u64::from_str(count_str) {
    count
} else {
    panic!("Can't parse integer: '{count_str}'");
};
```
## while let
Similar to if-let
```rust
fn main() {
    // Make `optional` of type `Option<i32>`
    let mut optional = Some(0);
    
    // This reads: "while `let` destructures `optional` into
    // `Some(i)`, evaluate the block (`{}`). Else `break`.
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ Less rightward drift and doesn't require
        // explicitly handling the failing case.
    }
    // ^ `if let` had additional optional `else`/`else if`
    // clauses. `while let` does not have these.
}
```
[destructuring]: https://doc.rust-lang.org/stable/rust-by-example/flow_control/match/destructuring.html