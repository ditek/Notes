# Rust
<!-- MarkdownTOC -->

- [General](#general)
- [Preludes and Imports](#preludes-and-imports)
- [Variables](#variables)
- [Functions](#functions)
    - [Function Pointers](#function-pointers)
    - [Macros](#macros)
- [Types](#types)
    - [Numeric types](#numeric-types)
    - [Enums](#enums)
    - [Arrays](#arrays)
    - [Vectors](#vectors)
    - [Tuples](#tuples)
    - [Strings](#strings)
- [Flow Control](#flow-control)
    - [Match](#match)
    - [If](#if)
    - [Loops](#loops)
- [Handling Errors](#handling-errors)
- [Sample Code](#sample-code)

<!-- /MarkdownTOC -->

# General
- The start point of a Rust program is `main()`.
- `main()` could return an error.

```rust
fn main() {}
fn main() -> Result<(), String> {Ok(())}
```

- References are immutable by default. Hence, to get a mutable reference, we need to write `&mut var`, rather than `&var` even if `var` is mutable.
- Almost everything is an expression. Omitting the semicolon returns that expression.

# Setup
After installing Rust you can run `cargo init` in an empty folder to create a new package with the folder name as its name.

# Preludes and Imports
The prelude is the list of things that Rust automatically imports into every Rust program. This means (among other things) that Rust inserts `extern crate std;` into the root of every crate.

To use an external symbol it must be either imported using `use` or used with its absolute path, i.e. in the example bellow we would need to write `std::cmp::Ordering` every time if we don't use `use`.

```rust
use std::cmp::Ordering;
let result = 1.cmp(&2);
assert_eq!(Ordering::Less, result);

// Multiple items
use std::f64::consts::{PI,TAU}

// From parent module
use super::*;
```

## Modules
To specify that a module depends on another, we write:

```rust
mod foo;
```

The declaration above will look for a file named `foo.rs` or `foo/mod.rs`.

For referencing modules, the following keywords can be used:
- `crate` - the root module of your crate
- `super` - the parent module of your current module
- `self` - the current module

### Inline Module
A sub-module can be written directly within a module's code. This is common for unit tests. 

```rust
#[cfg(test)]
mod tests {
    // Use parent module
    use super::*;
    ...
}
```

# Testing
Tests are usually added as an inline sub-module.

```rust
// Remove module when not in test mode
#[cfg(test)]
mod tests {
    // Use parent module
    use super::*;
    ...
}
```

# Variables
- Variables are immutable by default.
- A variable can be redefined with the same or different type. This is called variable shadowing.
- Constants are directly replaced with their value at compile time.
- Constants must always have explicit types.

```rust
let foo = 5;            // Immutable
let mut bar = 5;        // Mutable
let guess: u32 = 10;    // Specifying type
let guess = 10u32;      // Specifying type
const MY_CONST: f32 = 3.14

let sum = {
    let a = 1;
    let b = 2;
    a + b
};
```

# Functions
- Drop `return` and the semicolon to return an expression.
- Functions can return multiple values by returning a tuple.
- A function that returns nothing actually returns a unit or an empty tuple.
- Hint: if you define a function, the data it accepts are called parameters. If you call that function and pass data to it, then it's called arguments.

```rust
fn increase(x: i32) -> i32 { x+1 }
fn increase(x: i32) -> i32 { return x+1; }
fn swap(x: i32, y: i32) -> (i32, i32) { (x, y) }

// The following two functions are equivalent; returning a unit
fn ret_nothing() {}
fn ret_nothing() -> () { return (); }
```

## Function Pointers
```rust
fn plus_one(i: i32) -> i32 { i + 1 }
let f: fn(i32) -> i32 = plus_one;   // Without type inference
let f = plus_one;                   // With type inference
let six = f(5);
```

## Macros
```rust
println!("{:?}", var);
panic!("{:?}", var);
```

# Types

## Overview
- Integers - `i`, `i8`, `i16`, `i32`, `i64`, `u`, `u8`, `u16`, `u32`, `u64` (default `i32`)
- Pointer size - `isize`, `usize`
- Floating point - `f32`, `f64` (default `f32`)
- Tuple - `(value, value, ...)` for passing fixed sequences of values on the stack
- Array - `[value, value, ...]` a collection of similar elements with fixed length known at compile time
- Slice - a collection of similar elements with length known at runtime
- String slice - `str` text with a length known at runtime


## Type Conversion
```rust
// Using `as` between compatible types
10u8 as u32     // 10u32
true as u8      // 1u8

```

## Arrays and Slices

```rust
let a = [1, 2, 3]; // a: [i32; 3]
let a = [0; 20]; // a: [i32; 20]. Each element will be initialized to 0
a.len()     // The length of `a`
println!("{:?}", a);

/* Slices */
let a = [0, 1, 2, 3, 4];
let complete = &a[..]; // A slice containing all of the elements in `a`.
let middle = &a[1..4]; // A slice of `a`: only the elements `1`, `2`, and `3`.
```

## Vectors
- Vectors are heap-allocated data structures
- A vector starts with a default capacity which is increased with a reallocation when needed
- `iter()` creates an iterator allowing using the vector in loops

```rust
let v: Vec<i32> = Vec::new();
// vec! macro can be used to construct a vector from an array
let v: Vec<i32> = vec![];
let v = vec![1, 2, 3, 4, 5];
let v = vec![0; 10]; // ten zeroes
v.push(3);
let two = v.pop();

for x in v.iter() {
    println!("{}", x)
}
```

## Tuples
A tuple is an ordered list of fixed size

```rust
let x = (1, "hello");
let x: (i32, &str) = (1, "hello");
// You can assign one tuple into another, if they have the same contained types and length
let mut x = (1, 2); // x: (i32, i32)
let y = (2, 3); // y: (i32, i32)
x = y;
// You can access the fields in a tuple through a destructuring let
let (x, y, z) = (1, 2, 3);
// Single-element tuples have a comma:
x = (0,);
// Tuple Indexing
let tuple = (1, 2, 3);
let x = tuple.0;
let y = tuple.1;
```

## Strings
Rust has two main types of strings: `&str` and `String`. Let’s talk about &str first. These are called ‘string slices’. A string slice has a fixed size, and cannot be mutated. It is a reference to a sequence of UTF-8 bytes.

`String` on the other hand is a struct that can change at runtime.

```rust
/******************** str ********************/
let greeting = "Hello there."; // Type: &'static str
let lines = "hello\nworld".lines();

str.trim()
str.parse()         // Convert a string to number (supports `expect`)

var.cmp(&target_var)            // Can be called on anything that can be compared. Returns `Ordering` type

/******************** String ********************/
let mut s = String::new();
String::new()       // Returns an empty string
let s = String::from("Hello world!");

std::io::stdin()    // Retruns  handle to the standard input 
    .read_line(&mut String) // Place stdin contents in a string
    .expect(String msg)     // Called on the returned io::Result. It `panic!`s if unsuccessful.

s.len()
```

## Enums
- `None` can be provided to represent the absence of an item

```rust
enum Color {
    Red,
    Blue,
    None,
};
let x = Color::Red;

// elements can also have one or more data types
enum Shape {
    Circle(i32, Color),
    Square(i32, Color),
}
let y = Shape::Circle(2, Color::Red)
```

## Struct
- Tuple-like Structs can be defined in a more concise syntax and used like tuples.
- Static methods are called with `::` while instance methods are called with `.`

```rust
struct Animal {
    name: String,
    height: i32,
}
let a = Animal{name: String::from("Bob"), height: 7}

// Tuple-like struct
struct Point(i32, i32);
let p = Point(1, 2);
println!("{}, {}", p.0, p.1);

// Unit-like struct (rarely used)
struct Marker;
```

### Methods
- Methods may have immutable instance reference `&self` or a mutable reference `&mut self`.
- By default, fields and methods are private. `pub` can be used to make them public.

```rust
struct Square {
    length: i32,
}
impl Square {
    pub fn get_length(&self) -> &i32 {
        &self.length
    }
}
```

## Traits
- Traits are like interfaces in other languages. They associate a set of methods with a struct type.
- When a struct implements a trait, we can interact directly with it through the trait without having to know the real type.
- Traits can have implemented methods. Although they don't have access to struct fields, they can implement useful common functionality.
- Traits can inherit methods from other traits.
- Dynamic dispatch is calling a function that takes a trait argument, i.e. the exact type is not know. It's recommended to use the `dyn` keyword to indicate this.

```rust
trait Plotter {
    fn draw_plot(&self);
    fn plot_common(&self) {...}
}
impl Plotter for Square {
    fn draw_plot(&self) {...}
}
// Trait inheritance
trait ShapePlotter: Plotter {
    fn plot_shape(&self) {
        self.draw_plot();
    }
}
// Dynamic dispatch
fn do_stuff(plotter: &dyn Plotter){
    plotter.draw_plot();
}
```

## Generic Types
- Generic types allow us to partially define generic structs or enums who can fully defined at compile time.
- The compiler tries to infer the type or we can specify it using the _turbofish_ operator `::<T>`.

```rust
struct MyType<T> {
    item: T,
}
impl<T> MyType<T> {...}
// Restrict allowed types
let x = MyType::<i32> { item: 3};
let y = MyType { item: 1.2 };       // inferred f32
```

We can restrict which types can be used by specifying traits they must implement.

```rust
struct MyType<T>
where
    T: MyTrait,
{
    item: T,
}

fn func<T>(x: T)
where
    T: MyTrait,
{...}
// OR
fn func(x: impl MyTrait) {...}
```


### Option and Result
- Rust has a built in generic enum called `Option` that allows us to represent nullable values,
- `unwrap` allows getting the value in a dirty manner panicking on None.

```rust
// Internal definition
enum Option<T> {
    None,
    Some(T),
}

struct MyType<T> {
    item: Option<T>,
}
let x = MyType { item: None };
if x.item.is_none() {...}
let y = MyType { item: Some(10) };
if y.item.is_some() {...}
match x.item {
    Some(v) => println!("{}", v),
    None => println!("not found"),
}

// Dirty handling: the following are equivalent
my_option.unwrap()
match my_option {
    Some(v) => v,
    None => panic!("error!"),
}

```

## Result
- Result allows us to return a value that has the possibility of failing.
- `?` operator can simplify handling the result by getting the value or returning on error.
- `unwrap` allows getting the value in a dirty manner panicking on error.

```rust
// Internal definition
enum Result<T, E> {
    Ok(T),
    Err(E),
}

fn is_even(i:i32) -> Result<bool,String> {
    if i % 2 {
        Ok(true)
    } else {
        Err(String::from("not even"))   
    }
}
let result = is_even(12);
match result {
    Ok(v) => println!("success {}", v),
    Err(e) => println!("Error: {}",e),
}

// Using `?`: the following two constructs are equivalent
let result = is_even(12)?
let result = match is_even(12) {
    Ok(v) => v,
    Err(e) => return Err(e),
}

// Dirty handling: the following are equivalent
my_result.unwrap()
match my_result {
    Ok(v) => v,
    Err(e) => panic!("error!"),
}

```

# Flow Control
## Match
- `match` is exhaustive so all cases must be handled.

```rust
match guess.cmp(&secret_number) {
    Ordering::Less    => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal   => {println!("You win!"); break;}
}
match number {
    // Match a single value (braces are optional)
    1 => {
        println!("One!")
    },
    // Match several values
    2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
    // Match an inclusive range
    13..=19 => println!("A teen"),
    // Bind the matched number to a variable
    matched_num @ 20..30 => println!("{}", matched_num);
    // Handle the rest of cases
    _ => println!("Ain't special"),
}

// Match is an expression
let is_one = match number {
    1 => true,
    _ => false,
}
```

## If
Logical operators: ==, !=, <, >, <=, >=, !, ||, &&.

```rust
if x == 5 {
    println!("x is five!");
} else if x == 6 {
    println!("x is six!");
} else {
    println!("x is not five or six :(");
}

let y = if x == 5 { 10 } else { 15 }; // y: i32
```

## Loops
```rust
// infinite loop
loop {
    break;
    continue;
}
// loop can break and return at once
let found = loop {
    if condition {
        break true
    }
}

while !done {}

for x in 0..10 {}       // up to and not including 10
for x in 0..=10 {}      // up to and including 10

// Loop labels
for (index, value) in (5..10).enumerate() {}
'outer: for x in 0..10 {
    'inner: for y in 0..10 {
        if x % 2 == 0 { continue 'outer; } // Continues the loop over `x`.
        if y % 2 == 0 { continue 'inner; } // Continues the loop over `y`.
    }
}
```

# Handling Errors
Functions that can fail like `parse()` can be handled in several ways:

```rust
// 1.
let num: u32 = str.parse()
                  .expect("Invalid Number")

// 2.
let num: u32 = match str.parse(){
    Ok(num) => num,     // Set the name `num` to the unwrapped `Ok` value and return it
    Err(_) => continue; // `_` is used to catch all errors
};
```

# Ownership
- When assigning a value to a variable, that variable becomes the resource _owner_.
- When an owner is passed as an argument to a function, ownership is moved to the function parameter and the variable can no longer be used in the original function unless the resource is returned.
- Another variable can borrow access to a resource by getting a reference to it using `&`.
- To borrow mutable access, we use `&mut`. A resource owner cannot be moved or modified while mutably borrowed.
- Given a mutable reference, we can set the owner's value or get a copy of the value using the `*` operator.

_References rules_

- There can only be one mutable reference or multiple non-mutable references but not both.
- A reference must never live longer than its owner.

```rust
struct Square {l: i32}
fn area(s: Square) {...}
fn main() {
    /*********************/
    let s = Square {l: 1};
    area(s);
    s.l = 2;    // ERROR! s can no longer be used in this function
    /*********************/
    let mut s1 = Square {l: 1};
    let s2 = &mut s1;
    area(s1);   // ERROR - cannot be moved while mutably borrowed
    s1.l = 2;   // ERROR - cannot be modified while mutably borrowed
    println!("{}", s2.x);   // Last usage of s2
    area(s1);               // s1 can be used again
    /*********************/
    let s2 = &mut s1;
    let s3 = *s2;       // a copy of the owner's value

}
```

_Explicit Lifetimes_

Function signature can specify which parameters and return values share the same lifetime. Lifetime specifiers start with a `'` (e.g. `'a`).
We can have static lifetime resources that don't drop by using hte `'static` specifier.

```rust
struct Square {l: i32}
// s2 and the returned value share the same life time
fn area<'a, 'b>(s1: &'a Square, s2: &'b Square) &'b i32 {...}

// Struct members can have lifetime specifiers
struct Circle<'a> {c: &'a i32}
```

# Compiler Directives

```rust
#![allow(dead_code)] // allow unused functions

```

# Sample Code

```rust
//extern crate ascii;

pub fn hex_to_bytes(hex: String) -> String {
    let mut bytes=String::new();
    for i in 0..(hex.len()) {
        let res = u8::from_str_radix(&hex[i..i+1], 16).unwrap();
        bytes += &format!("{:04b}", res);
    }
    bytes
}

fn bytes_to_base64(ascii_bits: String) -> Vec<u8> {
    let mut base64_vec :Vec<u8> = vec![];
    for i in 0..(ascii_bits.len()/6){
        let ch_bits = u8::from_str_radix(&ascii_bits[i*6..i*6+6], 2).unwrap();
        base64_vec.push(base64_to_ascii(ch_bits));
        println!("{}", ch_bits);
    }
    base64_vec
}

fn base64_to_ascii(base64: u8) -> u8{
    match base64 {
        0...25 => base64+65,
        26...51 => base64 + 71,
        52...61 => base64 - 4,
        _       => base64
    }
}

fn main() {
    let input = "49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d";
    let bits = hex_to_bytes(String::from(input));
    println!("{}", bits);
    let base64_vec= bytes_to_base64(bits);
    let x = String::from_utf8(base64_vec);
    println!("{}", x.unwrap());
}
```