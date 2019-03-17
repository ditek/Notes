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
- References are immutable by default. Hence, to get a mutable reference, we need to write `&mut var`, rather than `&var` even if `var` is mutable.

# Preludes and Imports
The prelude is the list of things that Rust automatically imports into every Rust program. This means (among other things) that Rust inserts `extern crate std;` into the root of every crate.

To use an external symbol it must be either imported using `use` or used with its absolute path.

```rust
use std::io;
use std::cmp::Ordering;
let result = 1.cmp(&2);
assert_eq!(Ordering::Less, result);
```

# Variables
```rust
let foo = 5;            // Immutable
let mut bar = 5;        // Mutable
let guess: u32 = 10;    // Specifying type
```

# Functions
```rust
fn main() {}
fn name(arg: Type) {}
fn name(arg: Type) -> RetType { arg+1 }     // The value in a line without a semicolon is returned
fn name(arg: Type) -> RetType { return arg+1 } // We can also use the `return` keyword
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
## Numeric types
`i`, `i8`, `i16`, `i32`, `i64`, `u`, `u8`, `u16`, `u32`, `u64`, `isize`, `usize`, `f32`, `f64`

## Enums

```rust
enum Foo {
    Bar,
    Baz,
};
let x = Foo::Bar;
```

## Arrays

```rust
let a = [1, 2, 3]; // a: [i32; 3]
let a = [0; 20]; // a: [i32; 20]. Each element will be initialized to 0
a.len()     // The length of `a`
/* Slices */
let a = [0, 1, 2, 3, 4];
let complete = &a[..]; // A slice containing all of the elements in `a`.
let middle = &a[1..4]; // A slice of `a`: only the elements `1`, `2`, and `3`.
```

## Vectors

```rust
let v: Vec<i32> = Vec::new();
let v: Vec<i32> = vec![];
let v = vec![1, 2, 3, 4, 5];
let v = vec![0; 10]; // ten zeroes
v.push(3);
let two = v.pop();
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

```rust
let greeting = "Hello there."; // Type: &'static str
let lines = "hello\nworld".lines();
let mut s = String::new();

/* Functions */
String::new()       // Returns an empty string
str.trim()
str.parse()         // Convert a string to number (supports `expect`)

std::io::stdin()    // Retruns  handle to the standard input 
    .read_line(&mut String) // Place stdin contents in a string
        .expect(String msg)     // Called on the returned io::Result. It `panic!`s if unsuccessful.

var.cmp(&target_var)            // Can be called on anything that can be compared. Returns `Ordering` type
```

# Flow Control
## Match
```rust
match guess.cmp(&secret_number) {
    Ordering::Less    => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal   => {println!("You win!"); break;}
}
match number {
    // Match a single value
    1 => println!("One!"),
    // Match several values
    2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
    // Match an inclusive range
    13...19 => println!("A teen"),
    // Handle the rest of cases
    _ => println!("Ain't special"),
}
```

## If
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
loop {  // Endless loop
    break;
    continue;
}
while !done {}
for x in 0..10 {}    // for (x = 0; x < 10; x++)
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