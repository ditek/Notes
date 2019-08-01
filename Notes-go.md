# GO
<!-- MarkdownTOC -->

- [Packages](#packages)
    - [Common Packages](#common-packages)
    - [Exported Names](#exported-names)
- [Variables](#variables)
    - [Types](#types)
    - [Casting and Type Conversion](#casting-and-type-conversion)
    - [Pointers](#pointers)
    - [Data Structures](#data-structures)
        - [Array](#array)
        - [Slice](#slice)
        - [Map](#map)
        - [Set](#set)
    - [Strings](#strings)
        - [Strings Package](#strings-package)
    - [Structs](#structs)
        - [Type Embedding](#type-embedding)
- [Functions](#functions)
    - [Closures](#closures)
    - [Methods](#methods)
    - [Goroutines](#goroutines)
        - [Channels](#channels)
            - [Closing a Channel](#closing-a-channel)
            - [Channel Select](#channel-select)
        - [Syncing Goroutines](#syncing-goroutines)
            - [Syncing with Channels](#syncing-with-channels)
            - [Syncing with WaitGroup](#syncing-with-waitgroup)
        - [Mutex](#mutex)
- [Interfaces](#interfaces)
    - [The Empty Interface](#the-empty-interface)
    - [Type Assertion](#type-assertion)
    - [Type Switch](#type-switch)
    - [Stringers](#stringers)
    - [Readers](#readers)
- [Flow control](#flow-control)
    - [If](#if)
    - [Foreach](#foreach)
    - [For Loop](#for-loop)
    - [While](#while)
    - [Switch](#switch)
    - [Defer](#defer)
- [IO](#io)
    - [Read Stdin](#read-stdin)
    - [Read Files](#read-files)
    - [Print \(fmt\)](#print-fmt)
        - [Format Verbs](#format-verbs)
- [Error Handling](#error-handling)
    - [Error Types](#error-types)
    - [Adding context to an error](#adding-context-to-an-error)
- [Web](#web)
    - [HTTP Library](#http-library)
        - [HTTPS Support](#https-support)
        - [Other HTTP Functions](#other-http-functions)
    - [WebSocket](#websocket)
    - [Network I/O](#network-io)
- [JSON](#json)
- [Reflection](#reflection)
- [Testing](#testing)
    - [Subtests](#subtests)
    - [Helper Functions](#helper-functions)
    - [Examples](#examples)
    - [Benchmarks](#benchmarks)
- [Miscellaneous](#miscellaneous)
    - [Execution Time](#execution-time)
    - [Modules](#modules)
    - [Helpful Tools](#helpful-tools)
        - [StaticCheck](#staticcheck)
    - [To write about](#to-write-about)

<!-- /MarkdownTOC -->

# Packages

## Common Packages

```go
package main

import "fmt"            // String formatting
import "strings"        // String manipulation

import "math/rand"      // Generating random numbers
rand.Intn(x int)        // Return a random int in range 0:x-1
rand.seed(x int64)      // Change seed

import "time"           // Time and date
time.Now()                                  // Current time
time.Now().UnixNano()                       // Convert to int64 value (nanoseconds since 1970)
time.Second                                 // Returns a second
time.Millisecond                            // Returns a millisecond
time.Sleep(1 * time.Millisecond)            // Sleep
tick := time.Tick(100 * time.Millisecond)   // Return a channel on which a timestamp is sent every 100ms
done := time.After(50 * time.Millisecond)   // Return a channel on which a timestamp is sent after 50ms
    select {
    case <-tick:
        fmt.Println("tick")
    case <-done:
        fmt.Println("done")
    }
```

## Exported Names
A package exports a name (makes it accessible in importing code) if it begins with a capital letter. When importing a package, you can refer only to its exported names.

_______________________________________________________________________________
# Variables
```go
// Constants
const Pi = 3.14
const (
    X = 1
    Y = 2
)

// Enumerate constants using iota
const (
    X = iota    // 0
    Y           // 1
    Z           // 2
    A = 5 * iota    // 0
    B               // 5
    C               // 10
)

// Declaration (variable takes a default value)
var num int
var nums []int
// Declaration with assignment
var i, j int = 1, 2
var nums []int = []int{1, 2, 3, 4}
var num int = sum(nums)
// Inferred typing
var nums = []int{1, 2, 3, 4}
var num = sum(nums)
// Inferred typing - short form (available only within functions)
nums := []int{1, 2, 3, 4}
num := sum(nums)
```

## Types
Basic types:

```go
bool
string
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr
byte                // alias for uint8
rune                // alias for int32 - represents a Unicode code point
float32 float64
complex64 complex128
```

Defining a new type:

```go
type MyFloat float64
```

## Casting and Type Conversion
`T(v)` converts the value `v` to the type `T`

```go
// int -> float64
a := float64(4)

// string -> int
a := strconv.Atoi(s)

// int -> string
a := 123
s := string(a)                      // s = "E" (ASCII)
s := strconv.Itoa(a)                // s = "123"
s := fmt.Sprintf("%d", a)           // s = "123"    (uses more resources thatn `Itoa`)

// int64 -> string
var a int64 = 123
s := strconv.FormatInt(a, 10)       // s = "123"

// int64 -> string
var a uint64 = 123
s := strconv.FormatUint(a, 10)      // s = "123"

// int -> []byte
import "encoding/binary"
bytes := make([]byte, 2)
binary.LittleEndian.PutUint16(bytes, uint16(num))
return bytes
```

## Pointers
A pointer holds the memory address of a value. The type `*T` is a pointer to a `T` value. Its zero value is `nil`. Unlike C, Go has no pointer arithmetic.

```go
var ptr *int
i := 42
ptr = &i
*ptr = 21       // i = 21
```

## Data Structures

### Array
An array is a list with a fixed size, which can't be changed at runtime. In other words, arrays are typed by the elements they contain and the number of elements.

```go
var a [4]int                // array of 4 ints
a = [4]int{1, 2, 4, 6}
a = [4]int{}                // all values default to 0's
a = [4]int{1, 2}            // last two values default to 0's
a := [...]int{1, 2, 4, 6}   // The capacity is infered
```

### Slice
Slices are like references to arrays. 
A slice does not store any data, it just describes a section of an underlying array. 
Changing the elements of a slice modifies the corresponding elements of that array.

The length of a slice is the number of elements it contains.

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.

The length and capacity of a slice `s` can be obtained using the expressions `len(s)` and `cap(s)`.

```go
var a [4]int
var b []int                 // b == nil
b = []int{1, 2, 3, 4}
b = a                       // compile error: mismatched array size
b = a[0:len(a)]             // works!
b = a[:]                    // works!

// Make an empty slice
b := make([]int, 3)

// 2D Slice
matrix := make([][]uint8, dy)
for i := range matrix {
    matrix[i] = make([]uint8, dx)
}
for y, row := range matrix {
    for x := range row {
        row[x] = uint8(x * y)
    }
}
```

__Operations on Slices__

```go
var a [4]int
var b []int

// Creating a slice
b = make([]int, 5)     // len(b)=5
b = make([]int, 0, 5)  // len(b)=0, cap(b)=5

// Copy
c := make([]int, len(b))
copy(c, b)

// Append
var b []int
b = append(b, 1)        // b = [1]
b = append(b, 2, 3)     // b = [1, 2, 3]

// Sorting
strs := []string{"c", "a", "b"}
sort.Strings(strs)
ints := []int{7, 2, 4}
sort.Ints(ints)
isSorted := sort.IntsAreSorted(ints)

// Compare (Beware! This is not type safe)
isEqual := reflect.DeepEqual(b, []int{1, 2})
```

### Map
The zero value of a map is `nil`. A `nil` map has no keys, nor can keys be added. The `make` function returns a map of the given type, initialized and ready for use.

```go
var m map[string]int
m = make(map[string]int)      // Initialize and return an empty map
m := map[string]int {}
m["Jon"] = 15
m["Tom"]++                    // A new field will be initialized to 0 so m["Tom"] == 1
// Map literals
var m = map[string]int{
    "Jon": 15,
}
// Delete an element
delete(m, key)
// Test that a key is present with a two-value assignment:
elem, ok = m[key]
// Looking up a non-existing key return the default type value
elem = m["I don't exist"]       // elem = 0
// Iteration
for k, v := range m {...}
// Extract keys
m := make(map[int]string)
keys := make([]int, 0, len(m))
for k := range m {
    keys = append(keys, k)
}
```

### Set
Go doesn't have sets. However, a `map` can be used to achieve the same behaviour.

```go
set := map[string]bool {"1": true}
found := set["1"]   // found == true
found := set["2"]   // found == false
```

## Strings
Strings are defined between double quotes "" or backticks ``. In backticks, backslashes have no special meaning and the string may contain newlines.

Concatenation is done with a `+`

### Strings Package

For string operations (e.g. replace, slice, etc.), the package `strings` is used.

```go
import "strings"

// Split a string by whitespaces
func Fields(s string) []string
```

## Structs
```go
type person struct{
    name string
    age, height int
}
var x person
x = person{"Jon", 14}
x = person{}            // Unspecified fields take their default value
x = person{age: 14}
x = person{age: 14, name: "Jon"}
x.age = 10
var y = x               // Deep copy
if x == y {}            // Returns true if all the fields are equal
ptr := &x
ptr.age = 15            // Same as (*ptr).age
```

### Type Embedding
Type embedding is a way for a type to use exported fields and methods of another type as if they were its own. That's done by including the embedded type as a nameless (anonymous) field.

```go
type Person struct {
    Name string
}
type Parent struct {
    Person
    NumChildren int
}
func (p Person) printName() {
    fmt.Println(p.Name)
}

john := Parent{
    Person:      Person{Name: "John"},
    NumChildren: 3,
}
john.printName()
```

_______________________________________________________________________________
# Functions

```go
func f_name(param type) ret_type { return 0 }
func f_name(p1, p2 type) ret_type { return 0 }
func swap(x, y string) (string, string) { return y, x }     // Multiple results
func f(str_list []string) string { return "" }

// Named return values
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return              // Naked return. Returns the named return values
}

// In-line functions
x := sum(a,b int) { return a+b }

//** Ellipsis (three dots) notation allows writing variadic functions **//
// `nums` is of type []int
func sum(nums ...int) int { }
sum()       // Actually passes {}
sum(1, 2)   // Passes {1, 2}
nums := []int{1, 2}
sum(nums...)    // Unpack the slice

//** Empty interface **//
// Takes any number of parameters of any type
func f(vals ...interface{}) {}
```

## Closures
A closure is a function that references variables from outside its body. In the example, the returned function _closes over_ the variable `i` to form a closure.

```go
func intSeq() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
func main() {
    nextInt := intSeq()
    fmt.Print(nextInt())
    fmt.Print(nextInt())
    // Prints 01
}
```

## Methods
A method is a function bound to a type, similar to class methods in C++. Methods have a special _receiver_ argument (see `Abs`). Methods can also take pointer receivers in order to modify the value to which the receiver points (see `Scale`).

Methods can be declared on non-struct types too.

```go
type Point struct {
    X, Y float64
}

// the Abs method has a receiver of type Point named p
func (p Point) Abs() float64 {
    return math.Sqrt(p.X*p.X + p.Y*p.Y)
}

// Methods with a pointer receiver are used to pass a reference
func (p *Point) Scale(f float64) {
    p.X = p.X * f
    p.Y = p.Y * f
}
func main() {
    p := Point{3, 4}
    fmt.Println(p.Abs())
}
```

## Goroutines
A _goroutine_ is a lightweight thread managed by the Go runtime.

`go f(x, y, z)` starts a new goroutine running `f(x, y, z)`.

### Channels
Channels allow sending and receiving values cross goroutines with the channel operator `<-`. Channels can be:
- _Unbuffered channels_: By default, channel sends and receives block until the other side is ready allowing synchronization.
- _Buffered channels_: Provide the buffer length as the second argument to `make` to initialize a buffered channel. It behaves as FIFO. In this case, sends block when the buffer is full. Receives block when the buffer is empty.

```go
ch := make(chan T)          // Unbuffered channel
ch := make(chan T, length)  // Buffered channel
ch <- v                     // Send v to channel ch
v := <-ch                   // Receive from ch, and assign value to v
// Channel as function parameter
func serve(ch <-chan SomeType) { /*do stuff*/ }     // reading from channel (input channel)
func serve(ch chan<- SomeType) { /*do stuff*/ }     // writing to channel (output channel)
func serve(ch chan SomeType) { /*do stuff*/   }     // read from or write to channel (input/output channel)
```

_Example:_

```go
func sum(s []int, c chan int) {
    sum := 0
    for _, v := range s {
        sum += v
    }
    c <- sum // send sum to c
}

func main() {
    s := []int{7, 2, 8, -9, 4, 0}
    c := make(chan int)
    go sum(s[:len(s)/2], c)
    go sum(s[len(s)/2:], c)
    x, y := <-c, <-c // receive from c
    fmt.Println(x, y, x+y)
}
```

#### Closing a Channel
A sender can close a channel with `close(ch)` to indicate that no more values will be sent. Receivers can test whether a channel has been closed by assigning a second parameter to the receive expression: `v, ok := <-ch`. `ok` is `false` if there are no more values to receive and the channel is closed.

`for i := range c` receives values from the channel repeatedly until it is closed.

#### Channel Select
The `select` statement lets a goroutine wait on multiple communication operations. 
A `select` blocks until one of its cases can run, then it executes that case. It chooses one at random if multiple are ready. If `default` is used, it's run if all the cases block.

```go
func increment(c, quit chan int) {
    x := 0
    for {
        select {
        case c <- x:
            x++
        case <-quit:
            return
        }
    }
}

func main() {
    c := make(chan int)
    quit := make(chan int)
    go increment(c, quit)
    for i := 0; i < 10; i++ {
        fmt.Println(<-c)
    }
    quit <- 0
}
```

### Syncing Goroutines

#### Syncing with Channels
```go
done := make(chan bool)
for i, param := range param_list {
    fmt.Printf("-> Crawling child %v/%v : %v.\n", i, len(param_list), param)
    go func(url string) {
        Crawl(url)
        done <- true
    }(param)
}
for i, param := range param_list {
    fmt.Printf("<- %v/%v Waiting for child %v.\n", i, len(param_list), param)
    <-done
}
fmt.Println("<- Done")
```

#### Syncing with WaitGroup
A `WaitGroup` is used to wait (block) for a collection of Goroutines to finish executing. Whenever we spawn `n` goroutines, we `Add(n)` to the `WaitGroup` causing its internal counter to increment. When a goroutine finishes execution we call `Done()`, causing the counter to decrement. `Wait()` blocks until the counter reaches zero.

```go
func do_stuff(i int, wg *sync.WaitGroup) {
    fmt.Println("started Goroutine ", i)
    wg.Done()
}

func main() {
    var wg sync.WaitGroup
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go do_stuff(i, &wg)
    }
    wg.Wait()
    fmt.Println("Finished!")
}
```

### Mutex
Go's standard library provides mutual exclusion with `sync.Mutex` and its two methods: `Lock`, `Unlock`. We can also use `defer` to ensure the mutex will be unlocked.

```go
import "sync"
var x  = 0
func increment(m *sync.Mutex) {
    m.Lock()
    x = x + 1
    m.Unlock()
}
func increment_defer(m *sync.Mutex) {
    m.Lock()
    defer m.Unlock()
    x = x + 1
}
func main() {
    var m sync.Mutex
    for i := 0; i < 1000; i++ {
        go increment(&m)
    }
    fmt.Println("final value of x", x)
    // This example just shows the mutex syntax. The program will probably finish before the threads return. See WaitGroup.
}
```

_______________________________________________________________________________
# Interfaces
An _interface_ is a named set of method signatures. If a variable has an interface type, then it can call all methods that are in it.

A type implements an interface by implementing its methods.

```go
type geometry interface {
    area() float64
}
type circle struct {
    radius float64
}

func (c circle) area() float64 { ... }

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
}

func main() {
    c := circle{radius: 5}
    measure(c)

    var g geometry
    g = c
    fmt.Printf("(%v, %T)\n", g, g)
    // Prints ({5}, main.circle)
}
```

## The Empty Interface
An empty interface is an interface that specifies zero methods, therefor, it can handle values of any type. Empty interfaces are used by code that handles values of unknown type. For example, `fmt.Print`.

```go
func Print(v interface{}) {
    fmt.Println(v)
}
func main() {
    x := 4
    Print(x)
    y := "Hi"
    Print(y)
    var i interface{}
    i = y
    Print(i)
}
```

## Type Assertion
The following statements are used to assert that the interface value `i` holds the concrete type `T` and assigns the underlying `T` value to the variable `t`.

```go
t := i.(T)
t, ok := i.(T)
```

The first statement will trigger a panic if `i` doesn't hold a `T`. The second statement will set `ok` to `true` and set `t` to the value of `i` if it holds a `T`. If not, `ok` will be `false` and `t` will be the zero value of type `T`, and no panic occurs.

## Type Switch
A type switch is like a regular switch statement, but the cases in a type switch specify types (not values), and those values are compared against the type of the value held by the given interface value.

```go
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}
```

## Stringers
`Stringer` is an interface defined by the `fmt` package and is used by many packages to print values.

```go
/**** In fmt ****/
type Stringer interface {
    String() string
}
/****************/

type circle struct {
    radius  int
}

func (c circle) String() string {
    return fmt.Sprintf("Radius is %v", c.radius)
}

func main() {
    a := circle{42}
    fmt.Println(a)
}
```

## Readers
`Reader` is an interface defined by the `io` package and is used by many packages to read streams. The interface has a `Read` method. `Read` populates the given byte slice with data and returns the number of bytes populated and an error value. It returns an `io.EOF` error when the stream ends.

```go
/**** In io ****/
type Reader interface {
    func (T) Read(b []byte) (n int, err error)
}
/****************/

func main() {
    r := strings.NewReader("Hello, Reader!")
    b := make([]byte, 8)
    for {
        n, err := r.Read(b)
        fmt.Printf("n = %v err = %v b = %v\n", n, err, b)
        fmt.Printf("b[:n] = %q\n", b[:n])
        if err == io.EOF {
            break
        }
    }
}
// Output:
// n = 8 err = <nil> b = [72 101 108 108 111 44 32 82]
// b[:n] = "Hello, R"
// n = 6 err = <nil> b = [101 97 100 101 114 33 32 82]
// b[:n] = "eader!"
// n = 0 err = EOF b = [101 97 100 101 114 33 32 82]
// b[:n] = ""
```


_______________________________________________________________________________
# Flow control

## If
The `if` statement can start with a short statement to execute before the condition. Variables declared by the statement are only in scope until the end of the `if`.

```go
if v := getV(); v < 0 { x = v }
```

## Foreach
Used to iterate over a slice or a map. The type of the index and the value are inferred since we use `:=`.

```go
for i, v := range nums {}   // We get item index and value
for _, v := range nums {}   // We only care about the value (i replaced with 'blank identifier')
for i := range nums {}      // We only care about the index
```

## For Loop
```go
for i := 0; i < count; i++ {...}
for ; i < count;  {i++}             // The init and post statements are optional
for {}                              // Infinit loop
```

## While
```go
for x == 1 { ... }
```

## Switch
```go
switch name := getName(); name {
    case "A": x = 1
    case "B", "C": x = 2
    default: x = 2
}

// Switch can be written with no condition. Works like if/else
switch {
    case x == 1: ...
    case x == 2: ...
}

// Type switch
whatAmI := func(i interface{}) {
    switch t := i.(type) {
    case bool:  fmt.Println("I'm a bool")
    case int:   fmt.Println("I'm an int")
    default:    fmt.Printf("Don't know type %T\n", t)
    }
}
```

## Defer
A defer statement postpones the execution of a function until the surrounding function returns. Used often when dealing with files. A deferred function's arguments are evaluated when the defer statement is evaluated.

```go
func main() {
    i := 0
    defer fmt.Println(i)
    i++
    fmt.Print(i)
}
// Prints: 10
```

Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order.

```go
func b() {
    for i := 0; i < 4; i++ {
        defer fmt.Print(i)
    }
}
// Prints: 3210
```

_______________________________________________________________________________
# IO

## Read Stdin
```go
func read_input() (string, error) {
    scanner := bufio.NewScanner(os.Stdin)
    err := scanner.Err()
    if err != nil { return "", err }
    return scanner.Text(), nil
}
```

## Read Files
```go
// Open file for read access.
file, err := os.Open("file.go")
if err != nil {
    log.Fatal(err)
}
// Read n bytes from a file
data := make([]byte, 100)
count, err := file.Read(data)

// Read all bytes in a file
import "io/ioutil"
data, err := ioutil.ReadAll(file)
```

## Print (fmt)
```go
import "fmt"
// Print to console
fmt.Println(1, "x")
// Print to a string
fmt.Sprintf()

// Print with formatting
fmt.Printf("string %s, int %d, struct with field names %+v")    // Struct fields
fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)             // Length and capacity of a slice

// JSON MarshalIndent can be used to format format a struct before printing its contents
s, err := json.MarshalIndent(person, "", "\t")
```

### Format Verbs

```bash
# General
%v  the value in a default format. When printing structs, the plus flag (%+v) adds field names
%#v a Go-syntax representation of the value
%T  a Go-syntax representation of the type of the value
%%  a literal percent sign; consumes no value

# Boolean:
%t  the word true or false

#Integer:
%b  base 2
%c  the character represented by the corresponding Unicode code point
%d  base 10
%o  base 8
%q  a single-quoted character literal safely escaped with Go syntax.
%x  base 16, with lower-case letters for a-f
%X  base 16, with upper-case letters for A-F
%U  Unicode format: U+1234; same as "U+%04X"

# Floating-point and complex constituents:
%b  decimalless scientific notation with exponent a power of two e.g. -123456p-78
%e  scientific notation, e.g. -1.234456e+78
%f  decimal point but no exponent, e.g. 123.456
%g  %e for large exponents, %f otherwise

# String and slice of bytes:
%s  the uninterpreted bytes of the string or slice
%q  a double-quoted string safely escaped with Go syntax
%x  base 16, lower-case, two characters per byte
%X  base 16, upper-case, two characters per byte

# Pointer:
%p  base 16 notation, with leading 0x
```

_______________________________________________________________________________
# Error Handling
There is an interface called `error` which has one method `Error() string`. Functions usually return a tuple, with an `error` value last. The value is set to `nil` if no error occurs.

```go
func readFile(fileName string) (string, error) {
    r, err := os.Open(fileName)
    if err != nil { return "", errors.New("Unable to open file") }
    if err != nil { return "", fmt.Errorf("Unable to open file %s", fileName) }
    if err != nil { return "", err }
}
```

## Error Types
Errors are not just strings, they have types as well. To print error type:

```go
fmt.print("%T", err)
```

Checking the error type can be useful if we have different potential error sources:

```go
switch errType := err.(type) {
case *net.OpError:
    ...
}
```

## Adding context to an error
The `errors.Wrap` function returns a new error that adds context to the original error, basically constructing a stack of errors. For example

```go
import "github.com/pkg/errors"

_, err := ioutil.ReadAll(r)
if err != nil {
        return errors.Wrap(err, "read failed")
}
```

_______________________________________________________________________________

# Web

## HTTP Library

**1. Handle dynamic requests**

An `http.ResponseWriter` value assembles the HTTP server's response; by writing to it, we send data to the HTTP client.

An `http.Request` is a data structure that represents the client HTTP request. `r.URL.Path` is the path component of the request URL.

```go
import "net/http"

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprint(w, "<h1> Welcome </h1>!")         // Write text/html to the page

    // Accessing "localhost:80/Jon" shows "Hi Jon!"
    fmt.Fprintf(w, "Hi %s", r.URL.Path[1:])

    path := r.URL.Path

    // Read GET parameters
    t := r.URL.Query().Get("keyword")
    // Read POST parameters (fields from an HTML form)
    email := r.FormValue("email")
}

// Handle dynamic requests
http.HandleFunc("/", handler)
http.HandleFunc("/about/", aboutHandler)

// We can also specify GET or POST methods
router.HandleFunc("/", rootHandler).Methods("GET")
```

**2. Serving static assets**

To serve static assets like JavaScript, CSS and images, we use the inbuilt `http.FileServer` and pass to it the files location (directory). Then we specify the desired URL using `http.Handle`.

```go
http.Handle("/static", http.FileServer(http.Dir("./src")))
// http.Handle("/static/", http.StripPrefix("/static/", fs))    // Not sure if Strip is needed
// OR
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
    http.ServeFile(w, r, "./src")
})
```

**3. Accept connections (listen to a port)**

`http.ListenAndServe` specifies that the port to listen to on any interface. This function will block until the program is terminated.

```go
log.Fatal(http.ListenAndServe(":80", nil))
```

### HTTPS Support
```go
log.Fatal(http.ListenAndServeTLS(":443", "server.crt", "server.key", nil))
```

### Other HTTP Functions
```go
func saveHandler(w http.ResponseWriter, r *http.Request) {
    doSomething()
    // Redirect to another page and add HTTP status code http.StatusFound (302)
    http.Redirect(w, r, "/view/", http.StatusFound)
    // HTTP error
    http.Error(w, "Something went wrong", http.StatusInternalServerError)
}
```

## WebSocket
WebSocket is an alternative protocol to HTTP, providing full-duplex communication channels over a single TCP connection. Therefor, we have an ideal way of pushing data to the client without having to resort to polling. It also brings significant performance benefits as we don't have the overhead of opening multiple TCP connections and we can push as much data through the connection as we want without the overhead of traditional HTTP requests.

A websocket is obtained by upgrading an HTTP connection.

```go
import (
    "net/http"
    "github.com/gorilla/websocket"
)

const maxMessageSize = 1024

var upgrader = websocket.Upgrader{
    ReadBufferSize:  maxMessageSize,    // optional
    WriteBufferSize: maxMessageSize,    // optional
}

func wsHandler(w http.ResponseWriter, r *http.Request) {
    conn, err := upgrader.Upgrade(w, r, nil)
    if err != nil {
        log.Println(err)
        return
    }
    // Receive a message
    // p is a []byte and messageType is an int with value websocket.BinaryMessage or websocket.TextMessage
    messageType, p, err := conn.ReadMessage()
    if err != nil {
        log.Println(err)
        return
    }
    // Send a message
    if err := conn.WriteMessage(messageType, p); err != nil {
        log.Println(err)
        return
    }
}

func main() {
    http.HandleFunc("/ws", wsHandler)   // Will listen to ws://localhost:80/ws
    http.ListenAndServe(":80", nil)
}
```

```js
var socket = new WebSocket("ws://localhost:8844/ws")
var name = document.getElementById("name");
var addr = document.getElementById("address");
// When a message (GET/POST) is received
socket.onmessage = function (event) {
             var nameAddress = event.data.split(" ");
             name.textContent = nameAddress[0].toString();
             addr.textContent = nameAddress[1].toString();
           }
socket.onopen = function(e) {};
socket.onclose = function(e) {};
```

_______________________________________________________________________________
## Network I/O
Package `net` provides a portable interface for network I/O, including TCP/IP, UDP, domain name resolution, and Unix domain sockets.

The Dial function connects to a server:

```go
conn, err := net.Dial("tcp", "golang.org:80")
conn, err := net.DialTimeout("tcp", "golang.org:80", 2*time.Second)
if err != nil {
    // handle error
}
// Don't forget to close the connection
defer sniffer.Close()

fmt.Fprintf(conn, "GET / HTTP/1.0\r\n\r\n")
status, err := bufio.NewReader(conn).ReadString('\n')
// ...
```

The Listen function creates servers:

```go
ln, err := net.Listen("tcp", ":8080")
if err != nil {
    // handle error
}
for {
    conn, err := ln.Accept()
    if err != nil {
        // handle error
    }
    go handleConnection(conn)
}
```

_______________________________________________________________________________
# JSON

```go
import "encoding/json"

type Person struct {
  Name string `json:"name"`
  Age  int    `json:"years"`
}

// Unmarshal
data := `{"Name": "Jon", "Age": 10}`
var person Person
err := json.Unmarshal([]byte(data), &person)

// Marshal
person := Person{ Name: "Jon", Age: 10 }
jsonStr, err := json.Marshal(person)    // jsonStr == `{"Name": "Jon","Age": 10}`
```

The struct doesn't need to specify all possible JSON fields.

```go
type Person struct {
  Name string `json:"name"`
  Job  string `json:"job"`
}
data := `{"name": "Jon", "age": 10}`
var person Person
err := json.Unmarshal([]byte(data), &person)    // err = nil
fmt.Printf("%+v", person)   // {Name:Jon Job:}
```

__Ignore JSON fields when parsing/writing__

```go
type Person struct {
  Name string `json:"name"`
  Age  int    `json:"-"`
}

data := `{"name": "Jon", "age": 10}`
var person Person
err := json.Unmarshal([]byte(data), &person)    // err = nil
fmt.Printf("%+v", person)   // {Name:Jon Age:0}

person := Person {Name: "Jon", Age: 10}
data, err := json.Marshal(person)   // err = nil
fmt.Println(string(data))           // {"name":"Jon"}
```

__Leave out empty fields__

```go
type Person struct {
  Name string `json:"name,omitempty"`
  Age  int    `json:"age,omitempty"`
}

person := Person {Name: "", Age: 0}
data, err := json.Marshal(person)   // err = nil
fmt.Println(string(data))           // {}
```

__Useful snippets__

```go
// For convenience, we can use a wrapper for Marshal
func jsonMarshal(v interface{}) string {
    jsonStr, err := json.Marshal(v)
    if err != nil {
        panic(err)
    }
    return string(jsonStr)
}

// MarshalIndent can be used to format the created JSON
s, err := json.MarshalIndent(person, "", "\t")
```

_______________________________________________________________________________

# Reflection
```go
import "reflect"

// reflect.Type
// Find type
varType := reflect.TypeOf(var)
// Type name
varType.Name()
// Type kind (a primitive type: slice, map, struct, pointer, func, etc.)
varType.Kind()
// Contained type of a data structure, pointer, channel, etc.
varType.Elem()

// Call a method by name
func (fsm *FSM) callAction(fname string, arg string) bool {
    obj := reflect.ValueOf(fsm)
    method := obj.MethodByName(fname)
    // Convert to a function with the right signature
    mCallable := method.Interface().(func(string) bool)
    return mCallable(arg)
}

```

_______________________________________________________________________________

# Testing
Rules for writing tests:
- It needs to be in a file with a name like `xxx_test.go`
- The test function must start with the word `Test`
- The test function takes one argument only `t *testing.T`

```go
package main

import "testing"

func TestAbs(t *testing.T) {
    got := Abs(-1)
    want = 1
    if got != want {
        t.Errorf("Abs(-1) = %d; want %d", got, want)
    }
}
```

## Subtests
Subtests allow us to group different related tests.

```go
func TestAbs(t *testing.T) {
    t.Run("absolute of zero", func(t *testing.T) {
        got := Abs(0)
        want = 0
        if got != want {
            t.Errorf("got %d; want %d", got, want)
        }
    })

    t.Run("absolute of non-zero", func(t *testing.T) {
        got := Abs(-1)
        want = 1
        if got != want {
            t.Errorf("got %d; want %d", got, want)
        }
    })
}
```

## Helper Functions
To reduce repetitive code (like assertions), a helper function can be used.

`t.Helper()` tells the test suit that this function is a helper and therefore the failure line number will be in the test function rather that the helper.

```go
func TestAbs(t *testing.T) {
    assertCorrectInt := func(t *testing.T, got, want int) {
        t.Helper()
        if got != want {
            t.Errorf("got %d; want %d", got, want)
        }
    }

    t.Run("absolute of zero", func(t *testing.T) {
        got := Abs(0)
        want = 0
        assertCorrectMessage(t, got, want)
    })
}
```

## Examples
Examples are compiled (and optionally executed) as part of a package's test suite.

An example is executed if it has an output comment. `go test` will fail if the expected output doesn't match the actual one.

```go
func ExampleAdd() {
    sum := Add(1, 5)
    fmt.Println(sum)
    // Output: 6
}
```

## Benchmarks
The benchmark works by running the tested code `b.N` times.

To run the benchmarks: `go test -bench=.` or `go test -bench="."` in Powershell.

```go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(1, 5)
    }
}
```

_______________________________________________________________________________

# Miscellaneous

## Execution Time

```go
start := time.Now()
run_func()
elapsed := time.Since(start)
log.Printf("Function took %s", elapsed)
```

## Modules
A module is a collection of related Go packages that are versioned together as a single unit.

```sh
# Initialize the module and create go.mod
go mod init <module_name>
# Create vendor directory
go mod vendor
# Prune any no-longer-needed dependencies
go mod tidy
# List current modules and their dependancies
go list -m all
```

## Helpful Tools

### StaticCheck
Staticcheck is a static analysis toolset.

```sh
cd my_project
go get honnef.co/go/tools/cmd/staticcheck
# Run `staticcheck` like you run `build`
staticcheck
```

## To write about
- HTTP templates: https://golang.org/doc/articles/wiki/
