---
layout: post
title:  "Let's Learn Rust 3 - Custom Types"
date:   2024-12-09 12:45:14 +0700
categories: jekyll update
---
## Structures
Three types of structures
1. Tuples
2. C structs
3. Unit structs

```rust
// Unit struct
struct Unit;

// Tuple
struct Pair(i32, f32);

// C struct
struct Point {
    x: f32,
    y: f32,
}

struct Rectangle {
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Instantiate a tuple struct
    let pair = Pair(1, 0.1);

    let point: Point = Point { x: 5.2, y: 0.4 };
    let another_point: Point = Point { x: 10.3, y: 0.2 };

    // Instantiate a C struct
    let _rectangle = Rectangle {
        top_left: Point { x: point.x, y: point.y },
        bottom_right: another_point,
    };

    // Instantiate a unit struct
    let _unit = Unit;
}
```

## Enums
An enum is just a type consisting of a set of named constants
```rust
enum Direction {
    North,
    East,
    South,
    West,
}
```

## Constants
Two types of constants
1. `const` unchangeable value
2. `static` possibly mutable

```rust
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn main() {
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
}
```