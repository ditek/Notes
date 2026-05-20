# Rust
<!-- MarkdownTOC -->

- [General](#general)
- [Setup](#setup)
    - [Dependencies](#dependencies)
    - [Cross compilation](#cross-compilation)
        - [Using Cross](#using-cross)
- [Preludes and Imports](#preludes-and-imports)
    - [Modules](#modules)
        - [Inline Module](#inline-module)
- [Testing](#testing)
- [Variables](#variables)
- [Functions](#functions)
    - [Function Pointers](#function-pointers)
    - [Macros](#macros)
    - [Closure \(Lambda\)](#closure-lambda)
- [Types](#types)
    - [Overview](#overview)
    - [Type Conversion and Casting](#type-conversion-and-casting)
    - [Arrays and Slices](#arrays-and-slices)
    - [Vectors](#vectors)
        - [Iterator Methods](#iterator-methods)
            - [filter_map](#filter_map)
    - [Tuples](#tuples)
    - [HashMap](#hashmap)
    - [HashSet](#hashset)
    - [Strings](#strings)
        - [String Parsing](#string-parsing)
            - [IP Parsing](#ip-parsing)
        - [String Formatting](#string-formatting)
    - [Enums](#enums)
    - [Struct](#struct)
        - [Methods](#methods)
    - [Traits](#traits)
        - [Traits for Foreign Types and Deref](#traits-for-foreign-types-and-deref)
    - [Generic Types](#generic-types)
        - [Option](#option)
    - [Result](#result)
- [Flow Control](#flow-control)
    - [Match](#match)
    - [If](#if)
    - [Loops](#loops)
- [Error Handling](#error-handling)
    - [Result](#result-1)
    - [Custom Errors](#custom-errors)
- [Ownership](#ownership)
- [File Management](#file-management)
    - [Paths](#paths)
    - [File Operations](#file-operations)
- [CLI](#cli)
    - [Arguments](#arguments)
    - [Progress Bar](#progress-bar)
    - [Running Commands](#running-commands)
    - [Stdin and User Input](#stdin-and-user-input)
- [Environment Variables](#environment-variables)
- [Compiler Directives](#compiler-directives)
- [Crates and Libraries](#crates-and-libraries)
    - [Clap](#clap)
    - [Indicatif](#indicatif)
    - [Glob](#glob)
    - [Regex](#regex)
    - [Serde](#serde)
        - [Serde Flatten](#serde-flatten)
        - [Serde Options](#serde-options)
        - [Serde JSON](#serde-json)
    - [Time and Date / Chrono](#time-and-date--chrono)
    - [CSV](#csv)
        - [CSV Writing](#csv-writing)
            - [CSV Writer Options](#csv-writer-options)
        - [CSV of Nested Structs](#csv-of-nested-structs)
    - [Serial Port](#serial-port)
    - [Tokio](#tokio)
    - [Influxdb](#influxdb)
    - [Cliff](#cliff)
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
To create a new Rust package:

```sh
cargo init [--name <PKG_NAME>]
```

This creates a `Cargo.toml` file and a `src` folder with a `main.rs` file.

```toml
[package]
name = "my_project"
version = "0.1.0"
edition = "2021"    # Rust version
[dependencies]
# Project dependencies
```

To build the project use `cargo build`. To build and run (without creating an executable) use `cargo run` respectively. To build a release version, use `cargo build --release`.
To run with arguments, use `cargo run -- arg1 arg2`.

## Dependencies
To add a dependency, you can either add the package name and version to the `Cargo.toml` file, or use the `cargo` command to add it.

```bash
cargo add dependency[@version] [--features feature_1,feature_2]
# Not specifying a version will use the latest. Example:
cargo add clap --features derive
```

The resulting `Cargo.toml` file will look like this:

```toml
[dependencies]
clap = { version = "4.5.1", features = ["derive"] }
```

A git dependency can be added using the following syntax:

```toml
[dependencies]
ring = { git = "https://github.com/briansmith/ring", version = "0.12" }
# or
ring = { git = "https://github.com/briansmith/ring", branch = "main" }
```

## Cross compilation
_Note: the recommended method is using Cross. See next section_

First we need to install the target platform and then we specify it when building.
We also need to configure Cargo to use the correct linker. In `.cargo/config.tmol`:

```toml
[target.aarch64-unknown-linux-gnu]
linker = "aarch64-linux-gnu-gcc"
```

```sh
# Install the cross compilation tools
sudo apt install gcc-aarch64-linux-gnu
# See available targets
rustc --print target-list
# Install target
rustup target add aarch64-unknown-linux-gnu
# Compile
cargo build --target=aarch64-unknown-linux-gnu
```

You might get the following error:

```sh
/lib/aarch64-linux-gnu/libc.so.6: version `GLIBC_2.33' not found
```

I this case, you either need to upgrade glibc on the target or compile with an older glibc. Compiling with an older version is done easier with Cross (see next section). For upgrading glibc, do the following:

```sh
# Check current version
ldd --version
# Upgrade
sudo apt ugrade libc6
```

### Using Cross
Cross gives more control over the cross compilation process. To set it up:

```sh
# Install Cross
cargo install cross
# Install Podman
sudo apt install podman
```

Create the configuration file in the project root `Cross.toml`.

```toml
[build]
# glibc version
zig = "2.28"
# Default target if --target is not used
default-target = "aarch64-unknown-linux-gnu"
```

Run the compilation.

```sh
cross build
# You can also perform run and test
cross run
```

___
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

___
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

___
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

___
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

## Closure (Lambda)
```rust
let add_one = |x| x + 1;
let add_one = |x: i32| -> i32 { x + 1 };
let ages = persons.iter().map(|person| person.age).collect();
```

If we want the closure to capture its environment, we use a different syntax.

```rust
let x = 1;
let inc = || x + 1;
// If you want to create a closure and immediately use it, surround it with ()
let is_positive = (|| x > 0)()
```

___
# Types

## Overview
- Integers - `i`, `i8`, `i16`, `i32`, `i64`, `u`, `u8`, `u16`, `u32`, `u64` (default `i32`)
- Pointer size - `isize`, `usize`
- Floating point - `f32`, `f64` (default `f32`)
- Tuple - `(value, value, ...)` for passing fixed sequences of values on the stack
- Array - `[value, value, ...]` a collection of similar elements with fixed length known at compile time
- Slice - a collection of similar elements with length known at runtime
- String slice - `str` text with a length known at runtime


## Type Conversion and Casting
```rust
// Using `as` between compatible types
10u8 as u32     // 10u32
true as u8      // 1u8
// String parsing
my_str.parse::<f64>().unwrap()
my_str.parse::<i32>().unwrap()
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

### Iterator Methods
- `iter()` - returns an iterator over references to the elements of the vector
- `iter_mut()` - returns an iterator that allows modifying each element

```rust
let mut my_vec = vec![1, 2, 3];
/* Mutating elements */
// Method 1
my_vec.iter_mut().for_each(|i| *i *= 2);
// Method 2
for i in &mut my_vec {
    *i *= 2;
}

/* Map */
let doubled: Vec<_> = my_vec.iter().map(|x| x * 2).collect();
```

#### filter_map
- `filter_map` applies a function to each element and returns the elements for which the function returns `Some`.

```rust
let a = ["1", "two", "NaN", "four", "5"];
let mut iter = a.iter().filter_map(|s| s.parse().ok());
// Equivalent to
let mut iter = a.iter().map(|s| s.parse()).filter(|s| s.is_ok()).map(|s| s.unwrap());
```

___
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

## HashMap
```rust
use std::collections::HashMap;

/* Creation */
let user_ages = HashMap::from([
    ("Jon", 4),
    ("Jane", 7),
]);

let user_ages = HashMap::new();
user_ages.insert("Jon", 4);
user_ages.insert("Jane", 7);

/* Methods */
let age = user_ages["Jon"];     // Panics if not found
user_ages.contains_key("Jon");
user_ages.remove("Jon");
match user_ages.get("Jon") {
    Some(user) => println!("found {user}"),
    None => println!("not found")
}

// Iteration
for (name, age) in &user_ages {...}
```

## HashSet
```rust
use std::collections::HashSet;

/* Creation */
let names = HashSet::from(["Jon"]);
let mut names = HashSet::new();
names.insert("Jon");
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

### String Parsing
#### IP Parsing
```rust
use std::net::{AddrParseError, Ipv4Addr};
fn is_valid_ip(ip: &str) -> Result<Ipv4Addr, AddrParseError> {
    ip.parse::<Ipv4Addr>()
}
```

### String Formatting
(The following also applies to `print!` macros)

```rust
format!("Name: {}, Age: {}", name, age)
// Positional arguments
format!("Name: {1}, Age: {0}", age, name)
// Named arguments
format!("Name: {name}, Age: {age}")
// Struct
format!("User info {:?}", info)
format!()

```

__Formatting flags__

Alignment:

    {:<width}: Left-align
    {:^width}: Center-align
    {:>width}: Right-align
    {0:>width}: Right-align, pad with zeroes.
    {0:0>width}: Right-align, pad with zeroes.

Numeric Formatting:

    {:+}: Show number sign including positive values.
    {:.precision}: Decimal precision
    {:0n} - zero padding
    {:b} - binary notation
    {:x} - hex notation
    {:o} - octal notation
    {:#x}: Hex notation with 0x.
    {:#b}: Binary notation with 0b.

String Formatting:

    {:.width}: Number of characters displayed for a string.


___
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
- Static methods are called with `::` while instance methods are called with `.`

```rust
struct Animal {
    name: String,
    height: i32,
}
let a = Animal{name: String::from("Bob"), height: 7}
```

__Tuple Struct__

Structs similar to tuples that don't have names for their fields.

```rust
// Tuple-like struct
struct Point(i32, i32);
fn main(){
    let p = Point(1, 2);
    println!("{}, {}", p.0, p.1);
}
```

__Unit-like Struct__

Useful when you need to implement a trait on some type but don't have any data that you want to store in the type itself.

```rust
struct Marker;
let m = Marker;
```

__Struct update__
A more concise way to take the non-specified fields on struct declaration from another object.

```rust
let user1 = User{
    name: "Jon",
    age: 31,
}
let user2 = User {
    name: "Jane",
    ..user1
}
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

___
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

### Traits for Foreign Types and Deref

```rust
use std::ops::Deref;

type Underlying = [i32; 256];
struct MyArray(Underlying);

impl Deref for MyArray {
    type Target = Underlying;

    fn deref(&self) -> &Self::Target {
        &self.0
    }
}

fn main() {
    let my_array = MyArray([0; 256]);

    println!("{}", my_array[0]); // I can use my_array just like a regular array
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


### Option
The `Option` type is an enum used to represent an optional value: it can either be `Some(T)`, indicating the presence of a value of type `T`, or `None`, indicating the absence of a value.
- Rust has a built in generic enum called `Option` that allows us to represent nullable values,

```rust
// Internal definition
enum Option<T> {
    None,
    Some(T),
}

fn get_option() -> Option<i32> {
    if condition {
        Some(10)
    } else {
        None
    }
}

let x = get_option();

// The following methods are equivalent
// 1
if let Some(v) = x {
    println!("{}", v);
} else {
    println!("not found");
}
// We can evaluate multiple variables
if let (Some(a), Some(b)) = (x, y){...}
// 2
match x {
    Some(v) => println!("{}", v),
    None => println!("not found"),
}
// 3
if x.is_some() {
    println!("{}", x.unwrap());
}
if x.is_none() {
    println!("not found");
}

// Using `?`: the following two constructs are equivalent
let result = get_option()?;
let result = match get_option() {
    Some(v) => v,
    None => return None,
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

___
# Error Handling
## Result
Functions that can fail (i.e. return a `Result`) like `parse()` can be handled in several ways:

```rust
// 1. If the funciton returns an error, panic with the specified message
let num: u32 = str.parse()
                  .expect("Invalid Number")

// 2. Using match
let num: u32 = match str.parse(){
    Ok(num) => num,     // Set the name `num` to the unwrapped `Ok` value and return it
    Err(_) => continue; // `_` is used to if we don't care about the error value
};
// To just use the value within match
match str.parse(){
    Ok(num) => println!("{}", num),
    Err(error) => println!("Error: {}", error),
}

// 3. Using `?` operator. This will return the error if the result is an error. The return type is Result
let num: u32 = str.parse()?;
// This is equivalent to the following:
let num: u32 = match str.parse(){
    Ok(num) => num,
    Err(error) => return Err(error),
}

// 4. Using `unwrap`. This will panic if the result is an error
let num: u32 = str.parse().unwrap();
// This is equivalent to the following:
let num: u32 = match str.parse(){
    Ok(num) => num,
    Err(error) => panic!("Error: {}", error),
}
```

## Custom Errors
We can create a new error type with a custom message:

```rust
#[derive(Debug)]
struct CustomError(String);
fn main() -> Result<(), CustomError> {
    let path = "test.txt";
    let content = std::fs::read_to_string(path)
        .map_err(|err| CustomError(format!("error reading `{}`: {}", path, err)))?;
    Ok(())
}
```

To keep the error context, we can use `anyhow` crate:

```rust
use anyhow::{Context, Result};
fn main() -> Result<()> {
    let path = "test.txt";
    let content = std::fs::read_to_string(path)
        .with_context(|| format!("error reading `{}`", path))?;
    Ok(())
}
```

___
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

___
# File Management

## Paths
```rust
// To handle paths we prefer using `PathBuf` rather than `String`
let path = std::path::PathBuf::from("/home/user/file.txt");

// Build dynamically
let mut path = PathBuf::new();
path.push(r"C:\");
path.push("windows");
path.push("system32");
path.pop();
path.set_extension("dll");
```

## File Operations
```rust
/* Method1: reading file to memory */
let content = std::fs::read_to_string(&path).expect("could not read file");
for line in content.lines() {
    println!("{}", line);
}

/* Method2: reading file line by line via BufReader*/
let f = std::fs::File::open("log.txt")?;
let mut reader = std::io::BufReader::new(f);
let mut line = String::new();
let len = reader.read_line(&mut line)?;
```
___
# CLI
## Arguments
- `std::env::args()` returns an iterator over the command line arguments.
- `std::env::args().collect()` returns a vector of the command line arguments.

```rust
use std::env;
fn main() {
    let arg1 = env::args().nth(1).expect("no argument given");
    let args: Vec<String> = env::args().collect();
    println!("{:?}", args);
}
```

A better option than manual parsing is to use the `clap` crate. See [Clap](#clap) for more details.

## Progress Bar
The `indicatif` crate can be used to create progress bars. See [Indicatif](#indicatif).

## Running Commands
There are multiple ways to spawn a child process and execute a command:

- `output` — runs the program and returns the output (blocking)
- `spawn` — runs the program asynchronously and returns a the child process
- `status` — runs the program and returns the exit code

__output__

```rust
use std::process::Command;
let output = Command::new("ping")
    .arg("-c").arg("128")
    .arg(ip)
    .output()
    .expect("Failed to execute command");
// To specify the args later
let mut cmd = Command::new("ping");
cmd.arg("-c").arg("128");
cmd.arg(ip);
let output = cmd.output().expect("Failed to execute command");
// Getting output
println!("stdout: {}", String::from_utf8_lossy(&output.stdout));
println!("stderr: {}", String::from_utf8_lossy(&output.stderr));
println!("status: {}", output.status);
assert!(output.status.success());
```

__spawn__

```rust
let child = Command::new("ping")
    .arg(ip)
    .stdout(Stdio::piped()) // if we're interested in stdout
    .stderr(Stdio::piped()) // if we're interested in stderr
    .spawn()
    .expect("Failed to execute command");
// Block and return the output
let output = child.wait_with_output().expect("Failed to wait on child");
println!("stdout: {}", String::from_utf8_lossy(&output.stdout));
// Kill the child process
child.kill();
```

## Stdin and User Input
```rust
print!("Do you accept?");
io::stdout().flush().unwrap();
let mut input = String::new();
io::stdin().read_line(&mut input).unwrap();
match input.trim() {
    "" => println!("User accepted"),    // Typed enter
    "no" => println!("User rejected"),
    _ => println!("Invalid input. Try again."),
}
```

___
# Environment Variables
```rust
use std::env;
// Result<String, VarError>
match env::var(name) {
    Ok(v) => println!("{}: {}", name, v),
    Err(e) => panic!("${} is not set ({})", name, e)
}
```

___
# Compiler Directives

```rust
#![allow(dead_code)] // allow unused functions

```

___
# Crates and Libraries
## Clap
Clap is a command line argument parser. It can be used to parse command line arguments and generate help and usage information.

__Dependency__
```bash
cargo add clap --features derive
```
```toml
clap = { version = "4.0", features = ["derive"] }
```

__Usage__

We usually define a struct representing our arguments and then use it to parse the command line arguments.
- Documentation can be included in-line using `///` or `/** */` comments. `--help` is defined automatically.
- `parse()` must be called in `main()`. It will print an error and exit if the arguments are invalid.


_Customizing arguments_

- Named arguments:              `#[arg(short = 'o', long = "output")]`
- Inferred argument names:      `#[arg(short, long)]`
- Boolean argument:             just use `bool` type. No need for `Option`
- Default value (pre-parsed):   `#[arg(default_value="100")]`
- Default value (post-parsed):  `#[arg(default_value_t=100)]`
- Positional arguments:         `#[arg(index = 1)]`
- Multi-line doc comment:       `#[arg(verbatim_doc_comment)]`
- Optional arguments:           use `Option<T>` for the type
- Forbid empty values:          `#[clap(forbid_empty_values = true)]`
- Arg occurrences (-v, -vv)     `#[clap(parse(from_occurrences))]`
- Multiple values ("-x 1 2"):   `#[clap(multiple_values=true, value_delimiter=',')]`

_Top-level customization (before the struct)_

- Require at least one argument: `#[command(arg_required_else_help(true))]`
- Version: `#[command(version)]` 

_Validators_

Some types have built in validation. This includes all the primitive types and additonal ones including:

- Ipv4Addr
- SocketAddrV4

_Custom validator_

```rust
#[derive(Parser)]
struct Cli{
    #[clap(forbid_empty_values = true, validator = validate_package_name)]
    name: String,
}

fn validate_name(name: &str) -> Result<(), String> {
    if name.is_empty() {
        Err(String::from("name cannot be empty"))
    } else {
        Ok(())
    }
}
```

_Subcommands_

```rust
use clap::{Parser, Subcommand};

#[derive(Parser)]
struct Cli{
    #[command(subcommand)]
    cmd: Command,
}
#[derive(Subcommand)]
enum Command {
    /// Perform ping test
    Ping {
        ip: String,
    },
    /// Perform iPerf test
    Speed {
        ip: String,
        #[clap(short, long)]
        duration: Option<i32>,
    },
}

fn main() {
    let args = Cli::parse();
    match &args.cmd {
        Command::Ping { ip } => {/* Do stuff */},
        Command::Speed { ip, duration, } => {/* Do stuff */},
    }
}
```

_Example_

```rust
use clap::Parser;
/// Find a file in a directory
#[derive(Parser)]
struct Cli{
    /// Filename
    name: String,
    /// File size (positional argument)
    #[arg(index=1)]
    size: i32,
    /// The path to read
    #[arg(short='p', long="path")]
    path: std::path::PathBuf,
    /// Number of files (optional argument)
    #[arg(short, long, default_value=1)]
    number: i32,
    /// Verbosity
    #[clap(short, long, parse(from_occurrences))]
    verbosity: usize,
    /// Files
    #[clap(short, long, multiple_values = true)]
    files: Vec<String>,
}

fn main() {
    let args = Cli::parse();
    println!("name: {:?}, path: {:?}", args.name, args.path)
}
```

___
## Indicatif
Indicatif is a crate for creating progress bars.

```rust
use indicatif::{ProgressBar, ProgressStyle};
fn main() {
    let pb = ProgressBar::new(100);
    // Optional: set the style
    pb.set_style(ProgressStyle::default_bar()
        .template("[{elapsed_precise}] {bar:40.cyan/blue} {pos:>7}/{len:7} {msg}")
        .progress_chars("##-"));
    for i in 0..100 {
        pb.set_message(&format!("Processing {}", i));
        pb.inc(1);
    }
    pb.finish_with_message("done");
}
```

## Glob
The `glob` crate can be used to search for files using wildcards.

`glob()` takes a pattern and, if the pattern is valid, returns an iterator over the matching files.

```rust
use glob::glob;
for entry in glob("/home/**/*.txt").expect("Failed to read glob pattern") {
    match entry {
        Ok(path) => println!("{:?}", path.display()),
        Err(e) => println!("{:?}", e),
    }
}
// Get an iterator of the matching files
let files = glob("*.txt").unwarp().filter_map(Result::ok);
```

## Regex
__Single capture__

```rust
use regex::Regex;
let re = Regex::new(r"date (\d+)/(\d+)").unwrap();
if let Some(caps) = re.captures(&output_str) {
    let month: int32 = caps[1].parse().expect("Failed to parse month");
    let year: int32 = caps[2].parse().expect("Failed to parse year");
} else {
    eprintln!("Failed to parse ping output");
}
// Just checking match
let is_match = re.is_match(output_str)
```

__Capture all__

```rust
let haystack = "power?size=500&mode=nsa";
let re = regex::Regex::new(r"(\w+)=(\w+)").unwrap();
let pairs: Vec<(&str, &str)> = re
    .captures_iter(haystack)
    .map(|cap| {
        let (_, [key, value]) = cap.extract();
        (key, value)
    }).collect();
assert_eq!(pairs, vec![("size", "500"), ("mode", "nsa")]);
// We can loop on the captures
for cap in re.captures_iter(haystack) {
    let (_, [key, value]) = cap.extract();
    println!("{}:{}", key, value);
}
// If we don't care about the capturing groups
let pairs: Vec<&str> = re.find_iter(haystack).map(|m| m.as_str()).collect();
assert_eq!(pairs, vec!["size=500", "mode=nsa"]);
```

___
## Serde

### Serde Flatten
This is useful when we want split fields logically into structs in our code, but have them appear inline in the parent struct.
This also works for flattening a `Hashmap` for example.

```rust
use std::collections::HashMap;
use serde::{Serialize, Deserialize};

#[derive(Serialize, Deserialize)]
struct UserInfo {
    id: String,
    username: String,
}

#[derive(Serialize, Deserialize)]
struct User {
    #[serde(flatten)]
    user_info: UserInfo,

    #[serde(flatten)]
    extra: HashMap<String, serde_json::Value>,
}
```

### Serde Options
- Skip serializing
`#[serde(skip_serializing)]`
- Skip deserializing
`#[serde(skip_deserializing)]`
- Skip serializing and deserializing
`#[serde(skip)]`
- Skip serializing optionals if none or a custom condition:
`#[serde(skip_serializing_if = "Option::is_none")]`
`#[serde(skip_serializing_if = "Map::is_empty")]`
`#[serde(skip_serializing_if = "func")]`    // fn(&T) -> bool (see example bellow)
- Use default if value is not present
`#[serde(default)]`
- Flatten the contents of this field into the container it is defined in
`#[serde(flatten)]`

__Examples__

```rust
#[serde(skip_serializing_if = "is_zero")]
...
fn is_zero(n: &u32) -> bool {
    *n == 0
}
```

### Serde JSON
```sh
cargo add serde --features derive
cargo add serde_json
```

__Untyped JSON__

```rust
use serde_json::Value;
let data = r#"
    {
        "name": "John Doe",
        "age": 43,
    }"#;
let v: Value = serde_json::from_str(&data).expect("Failed to string as json");
let name = v["name"]
```

__Typed JSON__
```rust

```

___
## Time and Date / Chrono
```rust
let now = Local::now();
// Formatted string
let timestamp = now.format("%Y-%m-%d_%H-%M-%S").to_string();
// Unix epoch
let epoch = now.timestamp();  
```

___
## CSV
```sh
cargo add csv
```

### CSV Writing
`write_record` is used when writing a simple record that contains string-like data only. On the other hand, `serialize` is used when your data consists of more complex values like numbers, floats or optional values. 

__Without Serde__

```rust
let mut wtr = csv::Writer::from_writer(io::stdout());
// The header record is written just like any other record.
wtr.write_record(&["city", "country", "population"])?;
// The header can be also written like this
let mut header = csv::StringRecord::new();
header.push_field("city");
...
wtr.write_record(&header)?;

wtr.write_record(&["NewYork", "United States", "9686"])?;
wtr.write_record(&["Northbridge", "United States", "14061"])?;
wtr.flush()?;
```

__With Serde__


```rust
use serde::Serialize;
use std::io;

#[derive(Debug, Serialize)]
struct User {
    name: String,
    hobby: Option<String>,
}

let mut wtr = csv::Writer::from_writer(io::stdout());
// When using CSV with Serde, the header row is written automatically.
wtr.serialize(User {
    country: "United States".to_string(),
    hobby: Some(9686),
})?;
wtr.flush()?;
```

__Writing destinations__

```rust
// To stdio
let mut wtr = csv::Writer::from_writer(io::stdout());
// To file
let mut wtr = csv::Writer::from_path("output.csv")
// To string
let mut wtr = WriterBuilder::new().from_writer(vec![]);
let data = String::from_utf8(wtr.into_inner()?)?;
```

#### CSV Writer Options

```rust
let mut wtr = csv::WriterBuilder::new()
    // Disable header
    .has_headers(false);
    // Flexible records (variable num of fields)
    .flexible(true)
    .from_writer(io::stdout());
```

### CSV of Nested Structs
Since the CSV library cannot handle nested structs of Serde flattened structs, we need to flatten the structs ourselves using a tuple struct.
https://stackoverflow.com/questions/78226563/csv-with-nested-structs

```rust
use serde::Serialize;
use std::io;

#[derive(Serialize)]
struct User {
    info: UserInfo,
    origin: UserOrigin,
}

#[derive(Serialize)]
struct UserRow(UserInfo, UserOrigin);

#[derive(Serialize)]
struct UserInfo { name: String, }

#[derive(Serialize)]
struct UserOrigin { origin: String, }

fn main()  -> Result<(), Box<dyn std::error::Error>> {
    let mut wtr = csv::Writer::from_writer(io::stdout());
    wtr.serialize(
    UserRow (
        UserInfo { name: "Jon".to_string(), },
        UserOrigin { origin: "uk".to_string(), },
    ))?;
    wtr.flush()?;
    Ok(())
}
```

___
## Serial Port


__Note on cross compilation__

If compilation fails with the error `pkg-config has not been configured to support cross-compilation`, disable default features in cargo config:

```toml
serialport = {version = "4.0.1", default-features = false}
```

___
## Tokio
```sh
cargo add tokio
# To use async main
cargo add tokio --features macro,rt,rt-multi-thread`
```

___
## Influxdb
```sh

```

```rust
use chrono::Utc;
use futures::prelude::*;
use influxdb2_derive::WriteDataPoint;

#[derive(Default, WriteDataPoint)]
#[measurement = "cpu_load_short"]
struct CpuLoadShort {
    #[influxdb(tag)]
    host: Option<String>,
    #[influxdb(tag)]
    region: Option<String>,
    #[influxdb(field)]
    value: f64,
    #[influxdb(timestamp)]
    time: i64,
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let org = "myorg";
    let bucket = "mybucket";
    let influx_url = "http://129.241.153.51:8186";
    let token = std::env::var("INFLUXDB2_TOKEN").unwrap();

    let client = influxdb2::Client::new(influx_url, org, token);

    let points = vec![
        CpuLoadShort {
            host: Some("server01".to_owned()),
            region: Some("us-west".to_owned()),
            value: 0.64,
            time: Utc::now().timestamp_nanos(),
        },
        CpuLoadShort {
            host: Some("server02".to_owned()),
            region: None,
            value: 0.64,
            time: Utc::now().timestamp_nanos(),
        },
    ];

    client.write(bucket, stream::iter(points)).await?;

    Ok(())
}
```

## Cliff
changelog generator
https://git-cliff.org/

___
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