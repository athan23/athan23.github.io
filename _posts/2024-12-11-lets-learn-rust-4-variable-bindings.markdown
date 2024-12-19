---
layout: post
title:  "Let's Learn Rust 4 - Variable Bindings"
date:   2024-12-11 15:02:08 +0700
categories: jekyll update
---
## Mutability
```rust
let _immutable_binding = 1;
let mut mutable_binding = 1;

// Ok
mutable_binding += 1;

// Error
_immutable_binding += 1;
```

## Scope and Shadowing
Variable bindings have a scope. They are constrained to live in a *block*. A block is a collection of statements enclosed by braces `{}`.
```rust
let outer_binding = 1;
let shadowed_binding = 1;

{
    let inner_binding = 2;
    println!("inner: {}", inner_binding);

    println!("before being shadowed: {}", shadowed_binding);
    // This binding *shadows* the outer one
    let shadowed_binding = "abc";
    println!("shadowed in inner block: {}", shadowed_binding);
}

// Error! inner_binding doesn't exist in this scope
// println!("inner: {}", inner_binding);
println!("outer: {}", outer_binding);

println!("outside inner block: {}", shadowed_binding);
// This binding *shadows* the previous binding
let shadowed_binding = 2;
println!("shadowed in outer block: {}", shadowed_binding);
```

## Declare
You can declare variables and assign them values later
```rust
let a_binding;
a_binding = 1;
println!("a binding: {}", a_binding);

{
    let x = 2;

    // Initialize the binding
    a_binding = x * x;
}

println!("a binding: {}", a_binding);
```

## Freezing
You can freeze variable by binding the same name. Frozen variables cannot be modified until they go out of scope.

```rust
let mut _mutable_integer = 7i32;
{
    // Shadowing by immutable `_mutable_integer`
    let _mutable_integer = _mutable_integer;

    // Error! `_mutable_integer` is frozen in this scope
    // _mutable_integer = 50;
}

// Ok! `_mutable_integer` is not frozen in this scope
_mutable_integer = 3;
```