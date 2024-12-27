---
layout: post
title:  "Let's Learn Rust 9 - Structs"
date:   2024-12-17 17:22:08 +0700
categories: jekyll update
---
Diving deeper into structs.
```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // To instantiate
    let user1 = {
        active: true,
        username: String::from("username123"),
        email: String::from("example@email.com"),
        sign_in_count: 1,
    }

    // Instance can be mutable but the entire field must be mutable.
}
```

## Struct Update Syntax
We can create a new instance of a struct from another instance.
```rust
fn main() {
    let user2 = {
        email: String::from("another@email.com"),
        ..user1
    }

    // ..user1 must come last to specify that any remaining fields
    // should get their value from user1
}
```

## Methods
Methods are functions defined within the context of a struct. `impl` block is used to define a function.
Everything inside `impl` block will be associated with the struct.
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // &self is equivalent to self: &Self
    // In this case, it's rectangle: &Rectangle
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

## Associated functions
Associated functions are functions that are defined on a type.
Methods are associated functions that are called on a particular instance of a type.
```rust
struct Point {
    x: f64,
    y: f64,
}

impl Point {
    fn origin() -> Point {
        Point { x: 0.0, y: 0.0 }
    }

    fn new(x: f64, y: f64) -> Point {
        Point { x: x, y: y }
    }
}

fn main() {
    let p1 = Point::origin();
    let p2 = Point::new(1.0, 1.0);
}
```