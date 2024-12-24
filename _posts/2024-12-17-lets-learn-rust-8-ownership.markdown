---
layout: post
title:  "Let's Learn Rust 8 - Ownership"
date:   2024-12-17 12:11:48 +0700
categories: jekyll update
---
*Ownership* is a set of rules that govern how a Rust program manages memory.

## Rules
1. Each value has an *owner*.
2. There can only be one *owner* at a time.
3. When the *owner* goes out of scope, the value will be dropped.

## Memory and Allocation
```rust
{
    let s = String::from("hello"); // s is valid from this point forward
    // requests to allocate an amount of memory on the heap

}   // this scope is now over, and s is no longer valid
    // the memory is automatically returned once the variable that owns it goes out of scope
```

## Data Moving
In Rust, a *move* is similar to *shallow copy* and it invalidates the first variable.
```rust
let s1 = String::from("hello"); // s1 is valid from this point forward

let s2 = s1; // s2 is valid from this point forward. s1 is no longer valid.
             // s1 was moved to s2.

// Error! s1 is not valid
// println!("{s1}");
```

## Copy Trait
Rust has a special annotation called `Copy` trait. If a type implements the `Copy` trait, variables that use it do not move but are trivially copied.

Types that implement `Copy` trait:
1. All integers
2. All floats
3. `bool`
4. `char`
5. Tuples if they only contain types that also implement `Copy`.

```rust
let x = 5;
let y = x;

// Valid
println!("x = {x}, y = {y}");
```


## Ownership and Functions
```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1
    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // s3 goes out of scope and is dropped.
  // s2 was moved, so nothing happens.
  // s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

## Reference
A reference is like a pointer such that it is an address for another value.
```rust
fn main() {
    let s1 = String::from("hello");
    let len = calculate_length(&s1); // &s1 creates a reference to the value of s1.
                                     // Since the reference does not own the value,
                                     // s1 will not be dropped.
    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize { // s is a reference to a String
    s.len()
} // s goes out of scope but because it does not have ownership of what
  // it refers to, it is not dropped.
```

Reference can be mutable
```rust
fn main() {
    let mut s = String::from("hello");
    change(&mut s);

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    // BIG PROBLEM
    // let r3 = &mut s;
    // println!("{}, {}, and {}", r1, r2, r3);

    println!("{r1} and {r2}");
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{r3}");

}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

Reference rule:
1. At any given time, you can have either one mutable reference or any number of immutable references.
2. References must always be valid.