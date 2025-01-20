---
layout: post
title:  "Let's Learn Rust 11 - Pattern Matching"
date:   2024-12-21 16:42:52 +0700
categories: jekyll update
---
`match` compares a value against a series of patterns and then execute code based on which pattern matches
```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

Matching with `Option<T>`
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

Catch-all Patterns and `_` Placeholder
```rust
let dice_roll = 9;
match dice_roll {
    3 => add_fancy_hat(),
    7 => remove_fancy_hat(),
    other => move_player(other),

    // _ => reroll(),
    // Not going to use any other value that doesn't match the pattern
    // and run the code

    // _ => (),
    // Not going to use any other value that doesn't match the pattern
    // and not running any code
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
fn reroll() {}
```

`if let` lets you combine `if` and `let` to handle values that match one pattern while ignoring the rest.
```rust
// match examples
let config_max = Some(3u8);
match config_max {
    Some(max) => println!("The maximum is configured to be {max}"),
    _ => (),
}

let mut count = 0;
match coin {
    Coin::Quarter(state) => println!("State quarter from {state:?}!"),
    _ => count += 1,
}


// if let examples
let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}

let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {state:?}!");
} else {
    count += 1;
}

```
