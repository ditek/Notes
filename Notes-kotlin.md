# Kotlin

<!-- TOC -->

- [Variables](#variables)
- [Functions](#functions)
    - [Unit](#unit)
    - [Varargs](#varargs)
    - [Infix notation](#infix-notation)
    - [Lambdas](#lambdas)
- [Classes](#classes)
- [Types](#types)
    - [Strings](#strings)
        - [Definition](#definition)
        - [String Templates](#string-templates)
        - [String Methods](#string-methods)
    - [Collections](#collections)
        - [List (Imutable)](#list-imutable)
        - [Map (Imutable)](#map-imutable)
        - [MutableList](#mutablelist)
        - [Collection Methods](#collection-methods)
    - [Type Checks](#type-checks)
    - [Nullable Values](#nullable-values)
        - [Accessing properties of nullable values](#accessing-properties-of-nullable-values)
- [Flow Control](#flow-control)
    - [If](#if)
    - [When](#when)
    - [With](#with)
    - [Loops](#loops)
        - [Break and Continue Labels](#break-and-continue-labels)
        - [Return at labels](#return-at-labels)
- [IO](#io)
    - [Read File](#read-file)

<!-- /TOC -->

# Variables

```kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 3       // deferred assignment
var x = 5 // Mutable variable
```

# Functions
Functions with block body must always specify return types explicitly, unless it's intended for them to return `Unit`.

```kotlin
fun name(a: Int): Int { return a + 1 }
fun name(a: Int) = a + 1    // Function with an expression body and inferred return type
fun name(a: Int) { println("$a") }  // Returns `Unit`, which is optional to mention
fun name(a: Any) if (a is String) true else false  // Arg type not specified
// Default and named args
fun foo(arg1: String = "1", arg2: String): String
s = foo(arg2="1")
```

## Unit
- If a function does not return any useful value, its return type is `Unit`. 
- `Unit` is a type with only one value - `Unit`.

```kotlin
fun printHello(): Unit {
    println("Hello")
    // `return Unit` or `return` is optional
}
// This is equivalent to:
fun printHello() {}
```

## Varargs
- A parameter of a function (normally the last one) may be marked with `vararg` modifier allowing a variable number of arguments to be passed
- Inside a function a `vararg`-parameter of type `T` is visible as an array of `T` (`Array<out T>`).
- We can pass `vararg` arguments one-by-one, or we pass an array with the spread operator (prefix the array with `*`)

```kotlin
fun <T> asList(vararg ts: T): List<T> {
    for (t in ts) // ts is an Array
    {...}
}
val list = asList(1, 2, 3)
val a = arrayOf(1, 2, 3)
val list = asList(-1, 0, *a, 4)
```

## Infix notation
Functions can also be called using infix notations when:  
- They are member functions or extension functions;
- They have a single parameter;
- They are marked with the infix keyword.

```kotlin
// Define extension to Int
infix fun Int.shl(x: Int): Int {...}
// call extension function using infix notation
1 shl 2
// is the same as
1.shl(2)
```

## Lambdas
```kotlin
fruits
.filter { it.startsWith("a") }
.sortedBy { it }
.map { it.toUpperCase() }
.forEach { println(it) }
```

# Classes
```kotlin
class Country(val country: String, val continent: String)
```

---------------------------------------
# Types

## Strings

### Definition
- Kotlin has two types of string literals: escaped strings that may have escaped characters in them and raw strings (Ex1).
- A raw string is delimited by a triple quote (`"""`), contains no escaping and can contain newlines and any other characters (Ex2).
- You can remove leading whitespace with `trimMargin()` function (Ex3). By default `|` is used as margin prefix.

```kotlin
// Ex1
val s = "Hello, world!\n"
// Ex2
val text = """
    for (c in "foo")
        print(c)
"""
// Ex3
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    """.trimMargin()
```

### String Templates
```kotlin
val a = 1
val s1 = "a is $a"  // Returns "a is 1"
val s2 = "${s1.replace("is", "was")}"   // Returns "a was 1"
```

### String Methods
```kotlin
// String list to int list
val result = strings.map { it.toInt() }
// Split at a delimiter
val str = "1 = 2 - 3 - 4"
val separate1: List<String> = str.split(" = "," - ")   // ("1", "2", "3", "4")
val separate2: List<String> = str.split("\\s".toRegex())   // ("1", "=", "2", ...)
```

---------------------------------------
## Collections

### List (Imutable)
```kotlin
val list = emptyList()
val list = listOf("a", "b", "c")
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
val map = mapOf(Pair("a", 1), Pair("b", 2), Pair("c", 3))
```

### Map (Imutable)
```kotlin
class Country(val country: String, val capital: String)
val countries = listOf(Country("UK", "London"), Country("Norway", "Oslo"))
// Map from list fields
val map = countries.associateBy({ it.country }, { it.capital })
```

### MutableList
```kotlin
var myList: MutableList<Int> = mutableListOf<Int>()
myList.add(10)
myList.remove(10)
```

### Collection Methods
```kotlin
fun joinToString(separator: String = ", ", prefix: String = "", postfix: String = ""): String
// Filtering a list
val positives = list.filter { x -> x > 0 }
val positives = list.filter { it > 0 }
// Extracting elements 
class Country(val country: String, val capital: String)
val countries = listOf(Country("UK", "London"), Country("Norway", "Oslo"))
val capitals = countries.map{ it.capital }

```

---------------------------------------
## Type Checks
- The `is` operator checks if an expression is an instance of a type.
- If an immutable local variable or property is checked for a specific type, it is cast implicitly.

```kotlin
// Ex1
fun getStringLength(obj: Any): Int? {
    if (obj is String) 
        return obj.length
    // `obj` is still of type `Any` outside of the type-checked branch
    return null
}
// Ex2
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null
    // `obj` is automatically cast to `String` in this branch
    return obj.length
}
// Ex3
fun getStringLength(obj: Any): Int? {
    // `obj` is automatically cast to `String` on the right-hand side of `&&`
    if (obj is String && obj.length > 0)
        return obj.length
    return null
}
```

---------------------------------------
## Nullable Values
A reference must be explicitly marked as nullable with a `?` when `null` value is possible.

```kotlin
var a: String = "abc"
a = null // compilation error
var b: String? = "abc"
b = null // ok
```

If you call a method or access a property on `a`, it's guaranteed not to cause an NPE. But if you want to access the same property on `b`, that would not be safe, and the compiler reports an error

```kotlin
val l = a.length    // Valid
val l = b.length    // error: variable 'b' can be null
```

### Accessing properties of nullable values
#### Checking for null in conditions
```kotlin
val l = if (b != null) b.length else -1
```

#### Safe Calls
```kotlin
b?.length
```
This returns `b.length` if b is not null, and `null` otherwise. The type of this expression is `Int?`.

```kotlin
fun parseInt(str: String): Int? {...}
```

Variables are automatically cast to non-nullable after null check

```kotlin
val x = parseInt(arg1)
// Using `x * 5` yields error because it may hold nulls.
if (x != null)
    println(x * 5)
// OR
if (x == null)
    return
println(x * 5)
```

Using Elvis operator

```kotlin
val l: Int = if (b != null) b.length else -1
val l = b?.length ?: -1
```

---------------------------------------
# Flow Control

## If
- `if` is an expression, i.e. it returns a value.
- If you're using `if` as an expression rather than a statement (returning its value or assigning it to a variable), the expression is required to have an `else` branch.

```kotlin
if (a > b) {
    return a
} else {
    return b
}

if (a > b) max = a
max =  if (a > b) a else b
max = if (a > b) {
    print("Choose a")
    a
} else {
    print("Choose b")
    b
}
```

## When
- `when` replaces the switch operator of C-like languages.
- If no argument is supplied, the branch conditions are simply boolean expressions (see Ex3).

```kotlin
when (x) {
    1 -> print("x == 1")
    2,3 -> print("x is 2 or 3")
    in 4..6 -> print("...")
    !in 7..9 -> print("...")
    in myList -> print("...")
    else -> { // Note the block
        print("x is neither 1 nor 2")
    }
}
// Ex2
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")
    else -> false
}
// Ex3
when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
}
```

## With
Useful for calling multiple methods on an object instance

```kotlin
with(myObj) {
    penDown()
    for(i in 1..4) 
        forward(100.0)
}
```

## Loops
```kotlin
for (item in collection) {}
for ((k, v) in map) {}
for (index in array.indices) {}
for ((index, value) in array.withIndex()) {}
for (item:Int in ints) {}
for (x in 1..5) {}  // Includes 5
for (i in 1 until 100) { } // does not include 100
for (x in 1..10 step 2) {}
for (x in 9 downTo 0 step 3) {}
while (x > 0) { x-- }
do {
    val y = retrieveData()
} while (y != null) // y is visible here!
```

### Break and Continue Labels
```kotlin
// Break and Continue Labels
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (...) break@loop
    }
}
```

### Return at labels
```kotlin
// nonlocal return from inside lambda directly to the caller of foo()
fun foo() {
    ints.forEach {
        if (it == 0) return
        print(it)
    }
}
// Return only from the lambda expression
fun foo() {
    ints.forEach lit@ {
        if (it == 0) return@lit
        print(it)
    }
}
// An implicit label, which has the same name as the function, can be used
fun foo() {
    ints.forEach {
        if (it == 0) return@forEach
        print(it)
    }
}
```

---------------------------------------
# IO

## Read File
```kotlin
val stringList = File("input.txt").readLines();
File("input.txt").useLines { lines -> lines.forEach { lineList.add(it) }}
```
