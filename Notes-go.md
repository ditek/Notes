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
        - [sync.Map](#syncmap)
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

# Project Structure
_src: https://go.dev/doc/modules/layout __

```
project-root-directory/
  [packages we don't wish to expose]
  internal/
    trace/
      trace.go
  [package can be imported by others]
  auth/
    auth.go
    auth_test.go
  go.mod
  modname.go
  modname_test.go
  hash.go
```

`go.mod` should start with the following (assuming using Github):

```
module github.com/someuser/modname
```

The code in `modname.go` and `hash.go` declares the package with:

```go
package modname
```

Package users import it with:

```go
import "github.com/someuser/modname"
```

If the module is a command, it contains a `func main` in one of the top file. By convention, that file is `main.go`.
Users are able to install the command with:

```sh
$ go install github.com/someuser/modname@latest
```

The `modname.go` file could include other module packges as:

```go
import "github.com/someuser/modname/internal/trace"
```

Exposed sub-packages can be imported as:

```go
import "github.com/someuser/modname/auth"
```

If the repository has multiple programs, it will have sperate directories:

```
project-root-directory/
  go.mod
  prog1/
    main.go
  prog2/
    main.go
```

If the repository includes commands and importable packages, it's a convention to include the programs in a `cmd` directory:

```
project-root-directory/
  go.mod
  modname.go
  auth/
    auth.go
  cmd/
    prog1/
      main.go
    prog2/
      main.go
```

If the project has non-Go files, it is recommended to keep Go commands in a `cmd` directory and Go packages in an `internal` directory.

# Packages

## Importing Packages

```go
package main

// Normal import
import "strings"
// Import with alias
import log "github.com/sirupsen/logrus"
```

### Blank Import
Go does not allow importing packages that are not used. If we want to import a package for its side effects, we can use the blank identifier so the value of the import is discarded while the side effects come through.

```go
import _ "image/png"
```

## init()
The `init()` function runs before the rest of the package is loaded. Each file can have its own (even multiple) `init` function.

`init` has several use cases including:
- Initializing variables
- Side effects of package import
- Checking program state

Initialization is run only once even if the package is imported in several files.

## Rand
```go
import "math/rand"      // Generating random numbers
rand.Intn(x int)        // Return a random int in range 0:x-1
rand.seed(x int64)      // Change seed
```

## Time
```go
import "time"

// Current time
time.Now()
// ISO format "2020-03-26T17:52:05+01:00"
time.Now().Format(time.RFC3339)
// Convert to int64 value (nanoseconds since 1970)
time.Now().UnixNano()

// Returns a second
time.Second
// Returns a millisecond
time.Millisecond
// Using a variable
time.Duration(interval) * time.Minute

// Sleep
time.Sleep(1 * time.Millisecond)

// Return a channel on which a timestamp is sent every 100ms
tick := time.Tick(100 * time.Millisecond)
// Return a channel on which a timestamp is sent after 50ms
done := time.After(50 * time.Millisecond)
select {
case <-tick:
    fmt.Println("tick")
case <-done:
    fmt.Println("done")
}
```

### Timeout
```go
select {
case m := <-c:
    handle(m)
case <-time.After(time.Hour):
    fmt.Println("timed out")
}
```

*NOTE* The underlying Timer is not recovered by the garbage collector until the timer fires. To avoid that, use NewTimer instead and call Timer.Stop if the timer is no longer needed.

```go
timer := time.NewTimer(time.Hour)
select {
case m := <-c:
    timer.Stop()
    handle(m)
case <-timer.C:
    fmt.Println("timed out")
}
```


### Ticker
Use `Tick` when you have no need to shut down the Ticker

```go
func tickForever(){
    for now := range time.Tick(time.Minute) {
        fmt.Println(now, statusUpdate())
    }
}
```

*NOTE* The underlying `Ticker` is not recovered by the garbage collector until the timer fires. To avoid that, use NewTimer instead and call Timer.Stop if the timer is no longer needed.

```go
ticker := time.NewTicker(time.Minute)
for {
    select {
    case <-ticker.C:
        doStuff()
    case <-quit:
        ticker.Stop()
    }
}
```

Modifying ticker interval

```go
ticker := time.NewTicker(time.Duration(config.Interval) * time.Minute)
for {
    select {
    case <-ticker.C:
        doStuff()
    case config := <-configChan:
        ticker.Stop()
        ticker = time.NewTicker(time.Duration(config.Interval) * time.Minute)
    }
}
```

### Call after wait
`time.AfterFunc` can be used to call a function (in a goroutine) after a specific duration.

```go
timer = time.AfterFunc(time.Minute, doStuff())
// If we want to cancel the call
timer.Stop()
```

## Exported Names
A package exports a name (makes it accessible in importing code) if it begins with a capital letter. When importing a package, you can refer only to its exported names.

_______________________________________________________________________________
# Variables
```go
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

## Consts and Enums
```go
// Constants
const Pi = 3.14
const e float = 2.7
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

// Enum type
type Foo int

const (
    A Foo = iota
    B
)

func F(foo Foo) {
    switch foo {
    case A:
        ...
    default:
        // error
    }
}
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

### Getting Object Type
```go
// Using string formatting
t := fmt.Sprintf("%T", v)

// Using reflection
t := reflect.TypeOf(v).String()

// Using type assertion
switch v.(type) {
case int:
    t := "int"
}

switch x := v.(type) {
case int:
    // x has type int
}

```

### Custom Types

```go
type MyFloat float64
```

### Limiting Custom Types

```go
package unary
type unary int

const (
    Positive unary = 1
    Negative unary = -1
)

func (u unary) String() string {
    if u == Positive {
        return "+"
    }
    return "-"
}
```

However, a user can still assign a value to a `unary` variable that is neither Positive nor Negative

```go
p := unary.Positive
fmt.Printf("%v %d\n", p, p) // Prints: + 1

p = 3
fmt.Printf("%v %d\n", p, p) // Prints: - 3
```

A better way to restrict the values is using an unexported struct:

```go
type unary struct {
    val int
}

var (
    Positive = unary{1}
    Negative = unary{-1}
)

func (u unary) String() string {
    if u == Positive {
        return "+"
    }
    return "-"
}
```

_Note_ See https://stackoverflow.com/questions/37385007/creating-a-constant-type-and-restricting-the-types-values

## Casting and Type Conversion
__Interface__
For an expression `x` of interface type and a type `T`, the primary expression

> x.(T)

asserts that `x` is not nil and that the value stored in `x` is of type `T`. The notation `x.(T)` is called a type assertion. If `x` does not hold a `T`, the statement will trigger a panic. Therefore, a better approach is to test the assertion as:

```go
t, ok := x.(T)
```

__Other Types__

`T(v)` converts the value `v` to the type `T`

```go
// int -> float64
a := float64(4)

// string -> int
a, err := strconv.Atoi(s)

// string -> hex (string with even length)
hex.DecodeString("1234")            // []byte{0x12, 0x34}

// int -> string
a := 123
s := string(a)                      // s = "E" (ASCII)
s := strconv.Itoa(a)                // s = "123"
s := fmt.Sprintf("%d", a)           // s = "123"    (uses more resources than `Itoa`)

// int64 -> string
var a int64 = 123
s := strconv.FormatInt(a, 10)       // s = "123"

// uint64 -> string
var a uint64 = 123
s := strconv.FormatUint(a, 10)      // s = "123"

// int -> []byte
import "encoding/binary"
bytes := make([]byte, 2)
binary.LittleEndian.PutUint16(bytes, uint16(num))
return bytes

// bin -> int
uint, err := strconv.ParseUint(binStr, 2, 64)

// int -> hex
hexStr := fmt.Sprintf("%x", uint)

// []byte -> hex (or BCD) string
str := hex.EncodeToString([]byte{0x12, 0x34})   // "1234"

// hex string -> []byte
bytes, err := hex.DecodeString("d312")          // []byte{0xd3, 0x12})
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
b = a[0:]                   // works!
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
b = append(b, c...)     // b = c

// Remove element i
b = append(b[:i], b[i+1:]...)

// Remove elements while iteratiog
items := []int{1, 2, 2, 3}
newItems := items[:0]
for _, item := range items {
    shouldRemove := item == 2
    if !shouldRemove {
        newItems = append(newItems, item)
    }
}
items = newItems

// Sorting
strs := []string{"c", "a", "b"}
sort.Strings(strs)
ints := []int{7, 2, 4}
sort.Ints(ints)
isSorted := sort.IntsAreSorted(ints)
// Sort custom types
sort.Slice(dirRange, func(i, j int) bool { return dirRange[i] < dirRange[j] })

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
// Delete an element if it exists. Does not panic if missing
delete(m, key)
// Test that a key is present with a two-value assignment:
elem, ok = m[key]
// Looking up a non-existing key return the default type value
elem = m["I don't exist"]       // elem = 0
// Iteration
for k, v := range m {...}
// Extract keys
mymap := make(map[int]string)
keys := make([]int, len(mymap))
i := 0
for k := range mymap {
    keys[i] = k
    i++
}
```

### sync.Map
`sync.Map` is like a Go `map` but is safe for concurrent use without additional locking or coordination.

The zero Map is empty and ready for use. A Map must not be copied after first use.

```go
// Store sets the value for a key.
func (m *Map) Store(key, value interface{})

// Delete deletes the value for a key.
func (m *Map) Delete(key interface{})

// Returns the value stored in the map for a key, or nil if no value is present.
// The ok result indicates whether value was found in the map.
func (m *Map) Load(key interface{}) (value interface{}, ok bool)

// Returns the existing value for the key if present. Otherwise, it stores and returns the given value.
// The loaded result is true if the value was loaded, false if stored.
func (m *Map) LoadOrStore(key, value interface{}) (actual interface{}, loaded bool)

// Calls f sequentially for each key and value present in the map. If f returns false, range stops the iteration.
func (m *Map) Range(f func(key, value interface{}) bool)
```

_Common operations_

```go
// Clear map
m.Range(func(key interface{}, value interface{}) bool {
    m.Delete(key)
    return true
})
```

### Set
Go doesn't have sets. However, a `map` can be used to achieve the same behaviour.

```go
set := map[string]bool {"1": true}
found := set["1"]   // found == true
found := set["2"]   // found == false
```

## Strings
Strings are defined between double quotes "" or backticks ` `. In backticks, backslashes have no special meaning and the string may contain newlines.

Concatenation is done with a `+`

### Strings Package

For string operations (e.g. replace, slice, etc.), the package `strings` is used.

```go
import "strings"

// Split a string by whitespaces
func Fields(s string) []string
// Get lower case
func ToLower(s string) string
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

#### Using close to broadcast to a set of channels

```go
func worker(i int, ch chan string, quit chan struct{}) {
    for {
        select {
        case w := <-ch:
            fmt.Println("worker", i, "processed", w)
        case <-quit:
            fmt.Println("worker", i, "quitting")
            return
        }
    }
}

func main() {
    ch, quit := make(chan string), make(chan struct{})
    go makeWork(ch)
    for i := 0; i < 4; i++ { go worker(i, ch, quit) }
    time.Sleep(5 * time.Second)
    close(quit)
    time.Sleep(2 * time.Second)
}
```

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

#### Embedded Lock
```go
var hits struct {
    sync.Mutex
    n int
}

hits.Lock()
hits.n++
hits.Unlock()
```

### Context
Contexts make it easy to pass request-scoped values, cancellation signals, and deadlines across API boundaries to all the goroutines involved in handling a request.

The `WithCancel`, `WithDeadline`, and `WithTimeout` functions take a parent Context and return a derived Context and a `CancelFunc`. Calling the `CancelFunc` cancels the child and its children, removes the parent's reference to the child, and stops any associated timers.

#### Rules for using contexts
Do not store Contexts inside a struct type; instead, pass a `Context` explicitly to each function that needs it. The Context should be the first parameter, typically named `ctx`:

```go
func DoSomething(ctx context.Context, arg Arg) error {
    // ... use ctx ...
}
```

- Do not pass a `nil` Context, even if a function permits it. Pass `context.TODO` if you are unsure about which Context to use.
- Use context `Value`s only for request-scoped data that transits processes and APIs, like request IDs and user authentication tokens, not for passing optional parameters to functions.
- The same Context may be passed to functions running in different goroutines; Contexts are safe for simultaneous use by multiple goroutines. 

#### Derived Contexts

`Background()`

Returns an empty context, which can serve as the root of a Context tree.

`WithCancel(parent Context) (ctx Context, cancel CancelFunc)`

Returns a copy of `parent` whose `Done` channel is closed as soon as `parent.Done` is closed or cancel is called.

`WithDeadline(parent Context, deadline time.Time) (Context, CancelFunc)`

Returns a copy of `parent` whose `Done` channel is closed as soon as `parent.Done` is closed, cancel is called, or the deadline expires.

`WithTimeout(parent Context, timeout time.Duration) (Context, CancelFunc)`

Equivalent to `WithDeadline(parent, time.Now().Add(timeout))`. Returns a copy of `parent` whose `Done` channel is closed as soon as `parent.Done` is closed, cancel is called, or timeout elapses.

`WithValue(parent Context, key, val interface{}) Context`

Returns a copy of `parent` in which the value associated with `key` is `val`. The value is retrieved by calling `ctx.Value(key)`.

#### Usage for canceling a gorouting
```go
import "context"

func myReader(ctx context.Context) {
    for {
        select {
        case <-ctx.Done():
            return
        default:
            ...
        }
    }
}

func main() {
    var ctxReader context.Context
    ctxReader, readerCancel = context.WithCancel(context.Background())
    go myReader(ctxReader)
    err := doSomething()
    if err != nil {
        readerCancel()
    }
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

To check if a type actually implementes the interfaces, we can do this:

```python
var _ MyInterface = (*MyType)(nil)
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
# Generics

## Generic Functions
```go
func f[type_parameter_list](params) {...}
```

The type parameter can be a primitive type (e.g. `int`), a set of types (`int|float`) or a type constraint (`any`, `comparable`).

```go
func min[T constraints.Ordered](x, y T) T {...}
x := min[int](2, 3)

// The instantiation can be used to have a new non-generic function
iMin := min[int]
x := iMin(2, 3)
```

## Generic Types
```go
type customConstraint interface {
   ~int | ~string
}

```

## Type Constraints
```go
import "golang.org/x/exp/constraints"

any
comparable

constraints.Complex
constraints.Float
constraints.Integer
constraints.Ordered
constraints.Signed
constraints.Unsigned
```

_______________________________________________________________________________
# Flow control

## If
The `if` statement can start with a short statement to execute before the condition. Variables declared by the statement are only in scope until the end of the `if`.

```go
if v := getV(); v < 0 { x = v }
```

## For Loop
Used to iterate over a slice or a map. The type of the index and the value are inferred since we use `:=`.

```go
// With a variable
for i := 0; i < count; i++ {...}
for ; i < count;  {i++}             // The init and post statements are optional
for {}                              // Infinite loop

// Iteration
for i, v := range mySlice {}   // We get item index and value
for _, v := range mySlice {}   // We only care about the value (i replaced with 'blank identifier')
for i := range mySlice {}      // We only care about the index

// Similarly for maps
for key, value := range myMap {}

// Breaking out of nested loops
out:
for i := 0; i < 10; i++ {
    for j := 0; j < 10; j++ {
        break out
    }
}
```


## For on a Channel
Used to receive values from the channel repeatedly until it is closed.

```go
for val := range myChannel {
    fmt.Println(val)
}

// Equivalent to
for {
    select {
    case val <- myChannel:
        fmt.Println(val)
    }
}

// In case the value is not important
for range done {}
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
A `defer` statement postpones the execution of a function until the surrounding function returns.
Used often to make sure that we clean up resources before function return.
A deferred function's arguments are evaluated when the `defer` statement is evaluated.

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
# OS & IO

## Read Stdin
```go
func read_input() (string, error) {
    scanner := bufio.NewScanner(os.Stdin)
    err := scanner.Err()
    if err != nil { return "", err }
    return scanner.Text(), nil
}
```

## File Operations
```go
// Create with 0666 mode
f, err := os.Create("file.txt")

// Create with custom mode
f, err := os.OpenFile("file.txt", os.O_RDWR|os.O_CREATE, 0644)

// Open file for append
f, err := os.OpenFile("file.txt", os.O_APPEND|os.O_WRONLY, 0644)

// If the file doesn't exist, create it, or append to the file
f, err := os.OpenFile("file.txt", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)

// Open file for read
file, err := os.Open("file.txt")
err = file.Close()

// Check if a file exists
func fileExists(filename string) (bool, error) {
    if info, err := os.Stat(filename); err == nil {
        return !info.IsDir(), nil
    } else if os.IsNotExist(err) {
        return false, nil
    } else {
        return false, err
    }
}

// Check if it's a directory
info, err := os.Stat(filename)
isDir := info.IsDir()

// Check if there is an error opening file or it's a directory
if info, err := file.Stat(); err != nil || info.IsDir() {
  // error or is directory
}

// Remove file
if err := os.Remove(filename); err != nil && os.IsExist(err) {
    panic(err)
}

// Copy file method 1
func CopyFile(src, dst string) error {
    in, err := os.Open(src)
    if err != nil {
        return err
    }
    defer in.Close()

    out, err := os.Create(dst)
    if err != nil {
        return err
    }
    defer out.Close()

    _, err = io.Copy(out, in)
    if err != nil {
        return err
    }
    return out.Close()
}

// Copy file method 2
func CopyFile(src, dst string) error {
    input, err := ioutil.ReadFile(src)
    if err != nil {
        return err
    }
    if err = ioutil.WriteFile(dst, input, 0644); err != nil {
        return err
    }
    return nil
}

// Write bytes
bytes := []byte("Hello")
num, err := f.write(bytes)

// Write string
num, err := f.WriteString("Hello")

// Write using fmt
fmt.Fprintln(f, "Hello")

// Write data to a file.
// It creates the file with the given permissions if it does not exist; otherwise it truncates it before writing. 
bytes := []byte("Hello")
err := ioutil.WriteFile("/tmp/tmp.txt", bytes, 0644)

// Read n bytes from a file
data := make([]byte, 100)
count, err := file.Read(data)

// Read all bytes in a file
import "io/ioutil"
data, err := ioutil.ReadAll(file)

// Read the file and returns the contents
content, err := ioutil.ReadFile("testdata/hello")

// Extract filename/dir from a path
dir, file := filepath.Split("/path/to/file.txt")
file := filepath.Base("/path/to/file.txt")
dir := filepath.Dir("/path/to/file.txt")
```

## Directory Operations
```go
// Create directory if it doesn't exist
if _, err := os.Stat(path); os.IsNotExist(err) {
    os.Mkdir(path, 0700)
}

// Files in a directory
files,_ := ioutil.ReadDir(path)
fmt.Println(len(files))

// Join path elements
path.Join("a", "b", "c")        // "a/b/c"
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

## Shell Command Execution
```go
import "os/exec"

// Define the command that needs to run
cmd := exec.Command("ls", "-l", "/tmp")

// Run the command
err := cmd.Run()

// Run the command and return the output
out, err := cmd.CombinedOutput()

// Check if an executable exists and get its path
path, err := exec.LookPath("ls")
```

## Serial
```go
import "github.com/tarm/serial"

// Init
c := &serial.Config{Name: "COM45", Baud: 115200}
s, err := serial.OpenPort(c)

// Write
n, err := s.Write([]byte("test"))

// Read
buf := make([]byte, 128)
n, err = s.Read(buf)
log.Printf("%q", buf[:n])
```

## CLI
```go
import "flags"

/* Defining flags */
// Define a string flag with specified name, default value, and usage string
var fileName string
flags.StringVar(&fileName, "f", "./myfile", "File to use")

// Parse the flags
flag.Parse()
```

## OS
```go
// Handle relevant OS signals for graceful shutdown
signals := make(chan os.Signal, 1)
signal.Notify(signals, syscall.SIGINT, syscall.SIGTERM)

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

### Custom Error Types
We can have a simple error instance:

```go
var ErrNotFound = errors.New("not found")
if err == ErrNotFound {...}
if errors.Is(err, ErrNotFound) {...}

// If we want a custom type
type notFoundError error
var ErrNotFound notFoundError = errors.New("not found")
```

To add more information, we can also define a new type that implements the `error` interface.

```go
type error interface {
    Error() string
}
```

Example:

```go
type LoadingError struct {
    Path string
}

func (e *LoadingError) Error() string {
    return fmt.Sprintf("could not load %v", e.Path)
}

// Returning an error
func doStuff() Error {
    return &LoadingError{"/var/lib"}
}
err := doStuff()

// Checking the error:
switch e := err.(type) {
case *LoadingError:
    ...
}
//OR
if e, ok := err.(*QueryError); ok {...}
// OR
var e *QueryError
if errors.As(err, &e) {
    // e is set to the error's value
}
```

### Common Error Types
```go
os.IsNotExist(err)      // File or directory does not exist
os.IsExist(err)         // File or directory already exists
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

## Recover

```go
import (
    "fmt"
    "runtime/debug"
)

func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Error:", r)
            fmt.Println("Stack trace:", string(debug.Stack()))
        }
    }()
}
```

_______________________________________________________________________________

# Web

## HTTP Library

**1. Handle dynamic requests**

An `http.ResponseWriter` value assembles the HTTP server's response; by writing to it, we send data to the HTTP client.

An `http.Request` is a data structure that represents the client HTTP request. `r.URL.Path` is the path component of the request URL.

`http.HandleFunc` registers a handler for the given patter.
- If the pattern ends with a `/`, then it matches everything under it. For example `/` matches `/x` and `/x/y`. Also, `/about/` matches `/about/x`, but `/about` does not.
- If a string matches multiple patterns, the longest one applies. For example, the string `/about/me` matches both `/` and `/about/`, but the hander for `/about/` will be triggered since it's longer.

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
// We use `nil` for the second argument to use the DefaultServeMux
log.Fatal(http.ListenAndServe(":80", nil))
```

### HTTPS Support
```go
log.Fatal(http.ListenAndServeTLS(":443", "server.crt", "server.key", nil))
```

### Set HTTP Status Code
If needed, we can set an HTTP status code for the response. It must be set before writing anything to the `ResponseWriter`:

```go
w.WriteHeader(http.StatusNotFound) // 404
fmt.Fprint(w, "<h1>Page not found</h1>")
```

### Set HTTP Header Entries
```go
w.Header().Set("Content-Type", "text/html")
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

_______________________________________________________________________________
## Echo

### Serving static assets
Serve static files from the provided root directory.

```go
e := echo.New()
// `assets` is a folder at the root of the project.
// `/static/js/main.js` will fetch and serve `assets/js/main.js` file.
e.Static("/static", "assets")
// Serve files for path `/*`
e.Static("/", "assets")
```

Serve a certain staic file for a path.

```go
e.File("/", "public/index.html")
```

### Retrieve Data From

#### Form Data
```go
// curl -X POST http://localhost:1323 -d 'name=Joe'
func(c echo.Context) error {
  name := c.FormValue("name")
  return c.String(http.StatusOK, name)
}
```

#### Query Parameters
```go
// http://localhost:1323/users?name=Joe
func(c echo.Context) error {
  name := c.QueryParam("name")
  return c.String(http.StatusOK, name)
})
```

#### Path Parameters
```go
// http://localhost:1323/users/Joe
e.GET("/users/:name", func(c echo.Context) error {
  name := c.Param("name")
  return c.String(http.StatusOK, name)
})
```

#### Struct Binding
The following tags for specifying data sources are supported:

- `query` - query parameter
- `param` - path parameter (also called route)
- `header` - header parameter
- `json` - request body. Uses builtin Go json package for unmarshalling.
- `xml` - request body. Uses builtin Go xml package for unmarshalling.
- `form` - form data. Values are taken from query and request body. Uses Go standard library form parsing.

```go
type User struct {
  ID string `query:"id"`
}

// in the handler for /users?id=<userID>
var user User
err := c.Bind(&user); if err != nil {
    return c.String(http.StatusBadRequest, "bad request")
}
```
_______________________________________________________________________________

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
# RegEx
```go
import "regexp"

// Compile a RegEx
// Use raw string (`...`) to avoid escaping
r, err := regexp.Compile(expression)
// Get a list of matched groups
matches := r.FindStringSubmatch(str)

```

## Find Methods
There are 16 available methods that can be applied to a compiled expression. They are given by this expression:

`Find(All)?(String)?(Submatch)?(Index)?`

- If `All` is present, it finds all matches and return a slice of them. Otherwise, it only finds the first match.
- If `String` is present, the argument (and return value) is a string; otherwise it is a slice of bytes.
- If `Submatch` is present, it also finds caputring groups and returns a slice.
- If `Index` is present, matches are identified by byte index pairs within the input string.

## Match Methods
`Match(String|Reader)?`

 Match reports whether the argument (byte slice / string / reader) contains any match of the regular expression. 

## Replace Methods
`ReplaceAll(Literal)?(String)`

- If `String` is present, the argument (and return value) is a string; otherwise it is a slice of bytes.
- If `Literal` is present, the match is literally replaced. Otherwise, a `$` in the replace argument is expanded to a submatch, e.g. `$1` represents the first submatch.

`ReplaceAll(String)?(Func)?`

- If `Func` is present, the passed function is applied to the matches before constructing the return value.

_______________________________________________________________________________
# JSON

*Note: Struct fields need to be exported (capitalized) so the `json` package can see them.*

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

## Decode Map Values to Structs
To convert from `map[string]interface{}` to a custom struct, we can use `mapstructure`. This can be useful when parsing a JSON object that can have different types depending on a condition.

```go
import "github.com/mitchellh/mapstructure"

type Data struct {
    Type string                 `json:"type"`
    Info map[string]interface{} `json:"info"`
}

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

const jsonStr = `
    {
      "type": "person",
      "info": {
        "name": "Jon",
        "age": 20
        }
    }`


func main() {
    var data Data
    json.Unmarshal([]byte(jsonStr), &data)
    if data.Type == "person" {
        var person Person
        mapstructure.Decode(data.Info, &person)
        fmt.Println(person)
    }
}
```

_______________________________________________________________________________
# Reflection
```go
import "reflect"

// reflect.Type
// Find type
var varType Type
varType = reflect.TypeOf(var)
fmt.Println("Type is ", varType)

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

type T struct {}

func (t *T) Foo() {
    fmt.Println("foo")
}

func main() {
    var t T
    reflect.ValueOf(&t).MethodByName("Foo").Call([]reflect.Value{})
}
```

_______________________________________________________________________________
# AES Encryption

## Definitions
**Block cipher**: a deterministic algorithm operating on fixed-length groups of bits, called blocks, with an unvarying transformation specified by a symmetric key. Block cipher is suitable only for the encryption of a single block under a fixed key.

**Mode of operation**: a block cipher mode of operation is an algorithm that describes how to repeatedly apply a cipher's single-block operation to securely transform amounts of data larger than a block.

**Initialization Vector**: Most modes require a unique binary sequence, often called an initialization vector (IV), for each encryption operation. The IV has to be non-repeating and, for some modes, random as well. The initialization vector is used to ensure distinct ciphertexts are produced even when the same plaintext is encrypted multiple times independently with the same key.[

**Nonce**: an arbitrary number that is unique for all time for a given key to prevent replay attacks. It can be used an initialization vector (IV) in cryptographic hash functions and is often sent in plain text along the encrypted data so it can be decrypted. 

## Usage

### CBC
```go
plaintext := []byte("Encrypt me!")

// Create a fixed length key. AES accepts 16, 24, 32 long keys for AES-128, AES-192, AES-256
key := sha256.Sum256([]byte("secret key"))

func encrypt(){
    // Create a new AES block cipher
    block, err := aes.NewCipher(key[:])
    if err != nil {
      log.Fatal(err)
    }

    // Create an initialization vector
    iv := make([]byte, aes.BlockSize)
    if _, err := rand.Read(iv); err != nil {
      log.Fatal(err)
    }

    // Create a new CBC mode encrypter
    ciphertext := make([]byte, len(text))
    enc := cipher.NewCBCEncrypter(block, iv)
    enc.CryptBlocks(ciphertext, text)
}

func decrypt(){
    block, err := aes.NewCipher(key[:])
    if err != nil {
      log.Fatal(err)
    }

    newtext := make([]byte, len(ciphertext))
    dec := cipher.NewCBCDecrypter(block, iv)
    dec.CryptBlocks(newtext, ciphertext)
}
```

### GCM
```go
import (
    "crypto/aes"
    "crypto/cipher"
    "crypto/rand"
    "fmt"
    "io"
)

plaintext := []byte(Ï"Encrypt me!")

// Create a fixed length key. AES accepts 16, 24, 32 long keys for AES-128, AES-192, AES-256
key := sha256.Sum256([]byte("secret key"))

func encrypt(text []byte, key []byte) []byte {
    block, err := aes.NewCipher(key)
    if err != nil {
        panic(err.Error())
    }

    gcm, err := cipher.NewGCM(block)
    if err != nil {
        panic(err.Error())
    }

    nonce := make([]byte, gcm.NonceSize())
    if _, err := io.ReadFull(rand.Reader, nonce); err != nil {
        panic(err.Error())
    }

    // Seal(dst, nonce, plaintext, additionalData []byte) []byte
    // Seal encrypts and authenticates plaintext, authenticates the
    // additional data and appends the result to dst, returning the updated
    // slice.
    // We append the nonce to the the ciphertext so it can be used for decryption
    ciphertext := gcm.Seal(nonce, nonce, text, nil)
    fmt.Printf("%x\n", ciphertext)
    return ciphertext
}

func decrypt(ciphertext []byte, key []byte) []byte {
    block, err := aes.NewCipher(key)
    if err != nil {
        panic(err.Error())
    }
    gcm, err := cipher.NewGCM(block)
    if err != nil {
        panic(err.Error())
    }

    nonceSize := gcm.NonceSize()
    if len(ciphertext) < nonceSize {
        fmt.Println(err)
    }


    nonce, ciphertext := ciphertext[:nonceSize], ciphertext[nonceSize:]
    plaintext, err := gcm.Open(nil, nonce, ciphertext, nil)
    if err != nil {
        fmt.Println(err)
    }
    fmt.Println(string(plaintext))
    return plaintext
}
```

_______________________________________________________________________________

# Testing
Rules for writing tests:
- It needs to be in a file with a name like `xxx_test.go`
- The package can either be the code package or `xxx_test` to limit access to exported elemets.
- The test function must start with the word `Test`
- The test function takes one argument only `t *testing.T`

```go
package main

import "testing"

func TestAbs(t *testing.T) {
    got := Abs(-1)
    want := 1
    if got != want {
        t.Errorf("Abs(-1) = %d; want %d", got, want)
    }
}
```

## Running the Tests
```sh
# Run all tests in the current folder
$ go test
# Run all tests in all subfolders
$ go test ./...
# Run a specific test
$ go test -run NameOfTest
# Run tests in a specific file
$ go test foo_test.go
# Test with coverage
$ go test -cover
# Create coverage profile
go test ./... -coverprofile=coverage.out
go tool cover -html=coverage.out
```

## Subtests
Subtests allow us to group different related tests.

```go
func TestAbs(t *testing.T) {
    t.Run("absolute of zero", func(t *testing.T) {
        got := Abs(0)
        want := 0
        if got != want {
            t.Errorf("got %d; want %d", got, want)
        }
    })

    t.Run("absolute of non-zero", func(t *testing.T) {
        got := Abs(-1)
        want := 1
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

## Table Driven Tests
Test cases are grouped in tables (struct lists).

```go
func TestAdd(t *testing.T) {
    tests := []struct {
        name string
        a,b  int
        exp  int
    }{
        {
            "Add even",
            2, 4,
            6,
        },
    }
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got := Add(tt.a, tt.b)
            assertEqual(t, tt.exp, got)
        })
    }

    // We can use a sting map as well
    tests := map[string]struct{a, b, exp: int}{
        "Add even": {2, 4, 6},
    }
}
```

## TestMain
To do extra setup or teardown before or after testing, `TestMain` function can be used. It can be defined once per package.

```go
func TestMain(m *testing.M) {
    setup()
    // Run all tests
    exitCode := m.Run()
    teardown()
    os.Exit(exitCode)
}
```

## Test Fixtures
The Go tool ignores any files/directories that starts with a period, an underscore, or matches the word `testdata`.

Using golden files is also a good practice. See <https://blog.gojekengineering.com/the-untold-story-of-golang-testing-29832bfe0e19>.

## Mocking Dependencies
<https://medium.com/agrea-technogies/mocking-dependencies-in-go-bb9739fef008>
<https://deployeveryday.com/2019/10/08/golang-auth-mock.html>

Let's say a function requires accessing the serial port. This makes it hard to test. The solution is to mock the port so we could test the function.

```go
    // Create an interface for type we want to mock
    type SerialPort interface {
        Write(p int) (n int, err error)
    }

    // Use github.com/vektra/mockery to generate a mock for the interface

    // Create an instance of the mocked port
    var mockPort = &mocks.SerialPort{}

    // If we want `Write` to return (1, nil) if `123` is passed
    mockPort.On("Write", 123).Return(1, nil)

    // We can specify a pattern instead of a hard value by passing a matcher
    matcher := func(n int) bool {return n % 2 == 0}
    mockPort.On("Write", MatchedBy(matcher)).Return(2, nil)

    // We can use `mock.Anything` to cover any case that's not covered by earlier statements
    mockPort.On("Write", mock.Anything).Return(3, nil)

    // We can call a custom handler before `Write` returns
    func handler(args mock.Arguments) {
        arg := args[0].(int)
        fmt.Println(arg)
    }
    mockPort.On("Write", 123).Return(1, nil).Run(handler)

    // Assert that the expected mock calls are called
    mockPort.AssertExpectations(t)
```

## Useful Testing Functions
Taken from https://github.com/benbjohnson/testing

```go
// assert fails the test if the condition is false.
func assert(tb testing.TB, condition bool, msg string, v ...interface{}) {
    if !condition {
        _, file, line, _ := runtime.Caller(1)
        fmt.Printf("\033[31m%s:%d: "+msg+"\033[39m\n\n", append([]interface{}{filepath.Base(file), line}, v...)...)
        tb.FailNow()
    }
}

// assertOK fails the test if an err is not nil.
func assertOK(tb testing.TB, err error) {
    if err != nil {
        _, file, line, _ := runtime.Caller(1)
        fmt.Printf("\033[31m%s:%d: unexpected error: %s\033[39m\n\n", filepath.Base(file), line, err.Error())
        tb.FailNow()
    }
}

// assertEqual fails the test if exp is not equal to act.
func assertEqual(tb testing.TB, exp, act interface{}) {
    if !reflect.DeepEqual(exp, act) {
        _, file, line, _ := runtime.Caller(1)
        fmt.Printf("\033[31m%s:%d:\n\n\texp: %#v\n\n\tgot: %#v\033[39m\n\n", filepath.Base(file), line, exp, act)
        tb.FailNow()
    }
}
```

Example:

```go
value, err := DoSomething()
if err != nil {
    t.Fatalf("DoSomething() failed: %s", err)
}
if value != 100 {
    t.Fatalf("expected 100, got: %d", value)
}
// Becomes
value, err := DoSomething()
assertOK(t, err)
assertEqual(t, 100, value)
```

## Useful Test Helpers
Taken from https://www.youtube.com/watch?v=yszygk1cpEc

### Create Temp File
```go
func testTempFile(t *testing.T) (string, func()) {
    tf, err := ioutil.TempFile("", "test")
    if err != nil {
        t.Fatalf("err: %s", err)
    }
    tf.Close()
    return tf.Name(), func() { os.Remove(tf.Name()) }
}

func TestThing(t *testing.T){
    tf, tfclose := testTempFile(t)
    defer tfclose()
}
```

### Change Directory
```go
func testChdir(t *testing.T, dir string) func() {
    old, err := os.Getwd()
    if err != nil {
        t.Fatalf("err: %s", err)
    }
    if err := os.Chdir(dir); err != nil {
        t.Fatalf("err: %s", err)
    }
    return func() { os.Chdir(old) }
}

func TestThing(t *testing.T) {
    defer testChdir(t, "/other")()
}
```

### Test networking without mocking net.Conn
```go
func TestConn(t *testing.T) (net.Conn, net.Conn) {
    ln, err := net.Listen("tcp", "127.0.0.1:0")
    var server net.Conn
    go func() {
        defer server.Close()
        server, err = ln.Accept()
    }()
    client, err := net.Dial("tcp", ln.Addr().String())
    return client, server
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

_______________________________________________________________________________

# Miscellaneous

## Execution Time

```go
start := time.Now()
run_func()
elapsed := time.Since(start)
log.Printf("Function took %s", elapsed)
```

## sync.Once
To make sure a function is called only once, declare a `sync.Once` variable and use it to call the function.

```go
var initTestOnce = sync.Once{}
func runTest(){
    initTestOnce.Do(InitTest)
}
```

If you need to run something only once on a receiver, just struct embed `sync.Once` in your struct and use the Do method.

```go
type Message struct {
    sync.Once
}
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
# List current modules and their dependencies
go list -m all
```

### Using local modules
To the compiler that a package we are using exists locally, we add this to our `go.mod`

```
module github.com/myuser/main-package
replace github.com/myuser/other-package => ../other-package
```

### Using private repositories
The easiest way to achieve this is using access tokens. Basically, generate a Personal Access Token in Github (make sure it can access private repositories), create a `.netrc` file in your home directory and add your information:

```
machine github.com
       login ${MY_USERNAME}
       password ${MY_ACCESS_TOKEN}
```

Then inform Go that you need to get the code from a private repo

```sh
# A single repo
go env -w GOPRIVATE=github.com/futurehomeno/goutil
# All repos for a user
go env -w GOPRIVATE=github.com/futurehomeno/*
```

## Tools and Libraries

### Encoding

#### Base64
```go
import "encoding/base64"

// Standard encoding
base64.StdEncoding.EncodeToString([]byte("data"))
// Raw unpadded encoding. Useful when encoding encrypted data.
base64.RawStdEncoding.EncodeToString([]byte("data"))
// Encoding compatable with URLs and filenames
base64.UrlEncoding.EncodeToString([]byte("data"))

// Decoding
base64.StdEncoding.DecodeString(encodedString)
```

### StaticCheck
`staticcheck` is a static analysis toolset.

```sh
cd my_project
go get honnef.co/go/tools/cmd/staticcheck
# Run `staticcheck` like you run `build`
staticcheck
# Run on all the packages in a module
staticcheck github.com/ditek/gofsm/...
# Run on a file
staticcheck main.go
```

### Dynamic Reloading
Fresh is a command line tool that dynamically reloads whenever you save a Go or template file.

`https://github.com/gravityblast/fresh`

### MapStructure
Decoding generic map values to structures and vice versa. Used to decode `map[string]interface{}` obtained from JSON and decode it to the proper Go structure.

Say we have this JSON: `{ "type": "person", "name": "Mitchell" }`, if the struct that `name` is decoded to depending on `type`, it would be tricky to do this in plain Go. This library makes the task much easier.

`go get github.com/mitchellh/mapstructure`

### Profiling
<https://blog.golang.org/pprof>

### Go-migrate
Use to manage database migration.

__Installation__

```sh
brew install golang-migrate
```

__CLI__

```sh
# Trigger 
migrate -source file://./db/migrations -database "mysql://root:@tcp(127.0.0.1:3306)/hr" down 1
```

### Go-clock
Testable time functions

```go
import "github.com/msales/go-clock"

// In production
now := clock.Now() // Instead of `time.Now()`
since := clock.Since(now) // Instead of `time.Since()`
c := clock.After(time.Second) // Instead of `time.After(time.Second)`

// In testing
fakeNow := time.Date(2021, 1, 3, 10, 39, 12, 0, time.UTC)
// `clock.Now()` will always return `fakeNow` time.
mock := clock.Mock(fakeNow)
defer clock.Restore()
// Advances the fake clock's time by a second.
mock.Add(time.Second)
```

### Interpretters
- https://github.com/traefik/yaegi
- https://github.com/motemen/gore

_______________________________________________________________________________

## AWS

### DynamoDB

#### Scan
Scan returns all the items in the table as long as there is less than 1MB of data inside it. Otherwise, you'll have to run Scan a few times in a loop using pagination.

```go
// Scan for all elements
out, err := svc.Scan(context.TODO(), &dynamodb.ScanInput{
    TableName: aws.String("my-table"),
})

// Scan with filters and manual FilterExpression
out, err := svc.Scan(context.TODO(), &dynamodb.ScanInput{
    TableName:        aws.String("my-table"),
    FilterExpression: aws.String("attribute_not_exists(deletedAt) AND contains(firstName, :firstName)"),
    ExpressionAttributeValues: map[string]types.AttributeValue{
        ":firstName": &types.AttributeValueMemberS{Value: "John"},
    },
})

// Scan with filters using the expression builder
import "github.com/aws/aws-sdk-go-v2/feature/dynamodb/expression"
expr, err := expression.NewBuilder().WithFilter(
    expression.And(
        expression.AttributeNotExists(expression.Name("deletedAt")),
        expression.Contains(expression.Name("firstName"), "John"),
    ),
).Build()
if err != nil {
    panic(err)
}
out, err := svc.Scan(context.TODO(), &dynamodb.ScanInput{
    TableName:                 aws.String("my-table"),
    FilterExpression:          expr.Filter(),
    ExpressionAttributeNames:  expr.Names(),
    ExpressionAttributeValues: expr.Values(),
})
```
_______________________________________________________________________________

## Git Hooks
_Apply gofmt and cancel the commit process if formatting is applied_

```sh
# .git/hooks/pre-commit

gofiles=$(git diff --cached --name-only --diff-filter=ACM | grep '.go$')
[ -z "$gofiles" ] && exit 0

checkfmt() {
    hash gofmt 2>&- || { echo >&2 "pre-commit hook: gofmt not in PATH."; exit 1; }
    IFS='
'

    unformatted=$(gofmt -l $gofiles)
    # Return if no files need formatting
    [ -z "$unformatted" ] && return 0

    exitcode=0
    formatted=false
    for file in $gofiles
    do
        echo >&2 "pre-commit hook: Applying gofmt to $file"
        output=`gofmt -w "$file"`
        formatted=true
        if test -n "$output"
        then
            # any output is a syntax error
            echo >&2 "$output"
            exitcode=1
        fi
        # git add "$file"
    done

    if [ "$formatted" = true ]
    then
        echo >&2 "pre-commit hook: gofmt has been applied to some files. Please review the changes and commit again"
        echo >&2 "pre-commit hook: Changes not committed!!"
        exit 1
    fi

    exit $exitcode
}

checkfmt
```

### Add Git Hooks to the Repo
One way is to create a hook directory and create a Make target to configure Git to use it:

```makefile
init:
    git config core.hooksPath .githooks

build-go: init
    go build main.go
```

_______________________________________________________________________________

## Code Snippites

### Retry on failure
```go
func retry(attempts int, sleep int, f func() error, errMsg string) (err error) {
    for i := 0; ; i++ {
        if err = f(); err == nil {
            return
        }
        if i >= (attempts - 1) {
            break
        }
        // Increment sleep duration on each failure
        time.Sleep(time.Duration(sleep * (i+1)) * time.Second)
        logger.WithError(err).Errorf("retrying after error: %s", errMsg)
    }
    return fmt.Errorf("after %d attempts, last error: %s", attempts, err)
}
```

## To write about
- HTTP templates: https://golang.org/doc/articles/wiki/

