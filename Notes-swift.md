
## Operators
```go
...         // Closed range operator. `1...3` is a range including 1, 2, 3.
!           // Force unwrap an optional.
```

## Clean Code Guidelines
- Use `MARK`s to organize code.
- Use `extension` to separate properties from protocol conformance

```go
// MARK: - UIViewController
class ResultsViewController: UIViewController {
    
    // MARK: Outlets

    @IBOutlet private weak var myButton: UIButton!

    // MARK: Properties

    var state: Int

    // MARK: Life Cycle

    override func viewWillAppear(_ animated: Bool) {}
    
    // MARK: UI

    ...

    // MARK: Actions
    
    @IBAction private func doStuff() {}
}

// MARK: - Private Methods
class ResultsViewController {
    private func getSum() {}
}
```

## Data Types

### Primitive Types
```go
// With type inference
var x = "hello"
// Explicit type: Int, String, Float, Double, Character, Bool, Any
// The compiler defaults to String over Character, and Double over Float
var x: String = "hello"

// Constants
let x = "hello"

// Computed variable
var nameLength: Int {
    return name.count
}

// Optionals: a value that can hold 'nil'
var x: String! = nil
```

### Type Aliases
Allows giving a type an alternative name. Especially helpful when dealing with closures.

```go
typealias Str = String
let x: Str = "x"

typealias IntToInt = (Int) -> Int
typealias VoidToInt = () -> Int 
```

### Structs
```go
struct Student {
    let name: String
    // Fields can have an initial value
    var age: Int = 10
    // Computed properties
    var ageNextYear: Int {
    	return age + 1
    }
    // Static properties
    static var species = "human"
    // Custom initializer (constructor). In case we want to change the
    // behaviour of the default initializer or have a different signature.
    init(name: String, age: Int) {
        self.age = age
    }
    // Methods
    func myMethod(){}
    // Getters and setters
    var nameLength: Int {
        get { return name.count }
    }
    // OR as a computed property
    var nameLength: Int {
        return name.count
    }
    // description. Used when a struct instance is used in a string as: "\(student)"
    var description: String {
        get { return "Student is \(name)" }
    }
}
var joe = Student(name: "Joe", age: 19)
print(joe.name)
print(Student.species)
```

BTW, I went to the outdoor gym nearby and it's nice. We should try it out once you're back

### Classes
Class construction and use is identical to a struct. Differences are:
- A class is passed by reference while a struct is passed by value.
- Classes support inheritance. A class can inherit from only one other class.
- Classes don't have default initializers.

```go
class Animal {
    var name: String
}
class Dog: Animal {
    var tail: Bool
}

// Overriding parent methods
override func doStuff() {
    // ...
    super.doStuff()
}
```

__Static Functions__

They are functions that are bound to the class rather than an object. They are not inherited.

```go
static func doStuff(){}
```

__Class Functions__

They are static functions that can be inherited and overridden by child classes

```go
class func doStuff(){}
```

### Protocols
Similar to a Java Interface, a protocol defines a set of methods signatures that can be implemented by a struct or class.

```go
protocol Animal {
    func eat(food: String) -> String
}

class Dog: Animal, AnotherProtocol {
    func eat(food: String) -> String {}
}

// Protocols are types and are used as so
var x: Animal
func doStuff(myAnimal: Animal) {}
```

Common protocols:

```go

```

### Extensions
Extensions provide the ability to add new methods and properties to classes.

```go
// To extend a class, use the extension keyword, followed by the type name.
extension MyClass {}
// You can also add the protocols you would like the type to conform to.
extension MyClass: MyProtocol {}
```


### Enums

```go
// Raw enums
enum Color {
    case red
    case blue
}
enum Color {
    case red, blue
}

// Enums can have methods and init()
enum Color {
    case red, blue
    init(){
        self = .red
    }
    func isRed() -> Bool {
        return self == .red
    }
    var description: String {
        get {
            switch (self) {
            case .red: return "red"
            }
        }
    }
}

// Using enums
func myFunc(c: Color){}
myFunc(c: .red)


// Using with switch
var bestColor = Color.blue
switch bestColor {
    .red:
        // ...
    .blue:
        // ...
}
```

Enums can have raw values and associated values.

#### Enum Raw Values
A raw value is a string, character, or number (integer or float) that can represent an enum case. For a raw value type of Int, Swift will automatically assign integer values to each of the cases.
Raw values enable converting values into enum cases, and vice versa.

```go
// `Int` type annotation specifies that all cases must have a raw integer value. 
// Assigned by the compiler: red is 0, blue is 1, etc.
enum Color: Int {
    case red
    case blue
}
// red is 3, blue is 4
enum Color: Int {
    case red = 3
    case blue
}
// red is 1, blue is 3
enum Color: Int {
    case red = 1
    case blue = 3
}

// The default raw value for strings is the string name
enum Car: String {
    case toyota = "Toyota"
    case tesla     // raw value is "tesla"
}

// Accessing raw value
print(Car.toyota.rawValue)

// Enums can be initialized using raw values. This returns an optional.
var myCar = Car(rawValue: "Toyota")

```

#### Enum Associated Values
An enum case can have an associated value of any type that provides more information about the case. Different cases may have different associated value types.
Associated values are tuples, so they can hold multiple values.

```go
enum CarStatus {
    case new(String)
    case used(Int)
}
let myCar = CarStatus.used(4)

// With labels
enum CarStatus {
    case new(productionDate: String)
    case used(daysUsed: Int)
}
let myCar = CarStatus.used(daysUsed: 4)

// With multiple values
enum CarStatus {
    case used(from: String, to: String)
    case stolenAndFound(from: String, to: String)
}
let myCar = CarStatus.used(form: "1/1/1990", to: "1/1/2000")

// Accessing via switch
switch myCar {
// Form 1
case .used(let fromDate, let toDate):
    print("from \(fromDate) to \(toDate)")
// Form 2
case let .used(fromDate, toDate):
    print("from \(fromDate) to \(toDate)")
// Conditional match
case .used(let fromDate, _) where fromDate == "1/1/1990":
// Multiple cases
case .used(let fromDate, let toDate), .stolenAndFound(let fromDate, let toDate):
    print("from \(fromDate) to \(toDate)")
}

// Accessing via if
if case let CarStatus.used(fromDate, toDate) = myCar {
    print("from \(fromDate) to \(toDate)")
}
// Form 2
if case CarStatus.used(let fromDate, var toDate) = myCar {}
// Conditional match
if case let CarStatus.used(fromDate, _) = myCar where fromDate == "1/1/1990" {}
```

Associated values can be exposed via computed properties.

```go
enum CarStatus {
    case (productionDate: String)
    case used(from: String, to: String)
    case stolenAndFound(from: String, to: String)

    var dates: (from: String, to: String)? {
        switch self {
        case .used(let from, let to), .stolenAndFound(let from, let to):
            return (from, to)
        default:
            return nil
        }
    }
}

let myCar = CarStatus.used(form: "1/1/1990", to: "1/1/2000")
print(myCar.dates?.to)
```

### Optionals
An optional is a value that can hold 'nil'.

```go
// `model` might be nil if `myString` doesn't contain a number
var model: Int? = Int(myString)
var intModel: Int

// We can force unwrap the optional. This will case a fatal error on failure.
intModel = model!

// or we can check if it's actually an int.
// The following unwraps and assigns to a new int variable
if let x = model {
    intModel = x
} else {
    print("Error")
    return
}

// The convention is to use the same name for the unwrapped variable
if let model = model {
    // ...
}

// We can use `guard` to ensure the unwrapped optional is available for the rest of the function
guard let model = model else {
    print("Error")
    return
}

// Optional chaining: accessing a property of an optional
struct Student {
    let name: String
    var age: Int
}
var newStudent: Student?
if let name = newStudent?.name {
    print(name)
} else {
    print("No student. No name.")
}


// Unwrapping multiple optionals:
// Regular way
if let x = x {
    if let y = y {
        ...
    }
}
// Comma separated
if let x = x,
   let y = y {
    ...
}
// Using guards
guard let x = x else {
    return
}
guard let y = y else {
    return
}
...


// Nil Coalescing Operator:
// It is useful to provide a default value in case the value is nil
var newStudent: Student?
let name = newStudent?.name ?? "Ghost"

// Implicitly Unwrapped Optionals
// We tell the compiler that we know that an optional is safe to use
var model: Int! = Int(myString)
print(model)    // Used as a non-optional variable
```

### Strings
```go
// Initializing a string
var s = String()        // Empty string
var s = String(15)
var multiLine = """
hello
"""

// Interpolation
var name = "Kate"
var birthdayCheer = "Happy Birthday, \(name)!" 

// Concatenation
let greeting = "hello" + " " + "world"

// String methods
str.count               // String length
str.first               // First character
str.last                // Last character
str.removeLast()
str.removeFirst()
str.contains("Lou")
str.hasPrefix("Me")
str.hasSuffix("in")
str.lowercased()
str.uppercased()
String(str.reversed())
str.append(str2)        // Equivalent to str += str2
str.range(of: str2) -> Range<String.Index>?     // Search for string

import Foundation
str.replacingOccurrences(of: String, with: String)
```

### NSString and NSRange
Those are ObjC types that are still used in iOS like in some delegates. We can convert a String to NSString to handle such cases:

```go
var newText = textField.text! as NSString
newText = newText.replacingCharacters(in: range, with: string) as NSString

```

### Collections

#### Array
Arrays are value types, i.e. assignment creates a new array.

```go
// Initializing
var arr = Array<Int>()
var arr = [Int]()
var arr = [1, 2, 3]

// Subscripting
print(arr[0])

// Merging arrays
arr += [4, 5]

// Methods and properties
arr.count
arr.append(5)
arr.insert(0, at: 4)
arr.remove(at: 3)
arr.joined(separator: "/")      // Join elements to a string
```

#### Range
```go
var r = Range<Int>()
var r = 1...3         // A range including 1, 2, 3.
```

#### Dictionary
```go
// Initializing
var dict = [String:Int]()
var dict = ["first": 1, "second": 2]

// Adding items
dict["last"] = 10

// Removing items
dict["last"] = nil

// Subscripting returns an optional which value is nil if the key doesn't exist.
var existingValue: Int? = dict["third"]

// Updating a value
// This method returns the existing value if the key exists or nil if it doesn't.
var existingValue: Int? = dict.updateValue(3, forKey: "third")

// Accessing keys and values as arrays
let values = dict.values.map({$0})
let keys = dict.keys.map({$0})

// Methods and properties
dict.count
```

#### Set
Set is an unordered collection of unique values.

```go
var s = Set<Int>()
var s: Set = [1, 2, 3]
var s: Set<Character> = ["A", "B", "C"]

// Methods and properties
s.count
s.insert("D")
s.remove("A")
```

### Casting and Type Conversion
```go
// Get type as string
type(of: object)

// String -> Int
var x: Int = Int("1")

// Casting classes
class Animal {}
class Dog: Animal {}
var pet: Animal 
// forcibly convert the types with "as!" (up-casting)
let petDog = pet as! Dog
// or safely convert with "if let" with "as?"
if let petDog = pet as? Dog {}
```

## Flow Control

### Ternary Operator
```go
variable = booleanCheck ? useThisIfTrue : useThisIfFalse
```

### If
```go
if <condition> {
	// ...
} else if {
	// ...
} else {
	// ...
}
```

### Switch
```go
switch month {
case 1: print(“January”)
case 2: print(“February”)
default: ...
}

switch width!, height {
case let (w, h) where w == h: ...
case (10, 5): ...
}
```

### Loops
```go
for i in 1...10 {}
for _ in 1...10 {}
for c in "word" {}

while condition {}

repeat {
} while condition

// Breaking the loop
break
```

### Guard
`guard` is a conditional statement requires an expression to evaluate to true for execution to continue. If the expression is false, the mandatory `else` clause is executed instead which _must_ exit the scope.
It is most useful when unwrapping optionals.
A `guard` statement without `return`, `break` or `continue` produces a compile-time error.

```go
// We want to x to be > 0. Returns if x == 0.
guard x > 0 else { return }
guard x > 0, y > 0 else { return }

// Using with optionals:
// Before
if let x = x {
    if let y = y {
        ...
    } else {
        print("Error with y")
    }
} else {
    print("Error with x")
}

// After
guard let x = x else {
    print("Error with x"); return
}
guard let y = y else {
    print("Error with y"), return
}
... // Use x and y as normal variables

// Just check if a value is not `nil`
guard let _ = x else { return }
```

### Defer
A `defer` statement postpones the execution of a function until the surrounding function returns.
Used often to make sure that we clean up resources before function return.
Unlike in Go, the final value of a variable referenced in the body of a `defer` statement is evaluated. Defer blocks don’t capture the current value of a variable.

```go
func doStuff() {
    let i = 0
    defer {print(i)}
    i++
    print(i)
}
// Prints: 11
```

## Functions
```go
func myFunc(name: String) {}
myFunc(name: "Joe")

// Default parameters
func myFunc(name: String = "Joe") {}
myFunc()
myFunc(name: "Jack")

// Internal and External Parameter Names
func myFunc(nameOfEmployee name: String) {
	print(name)
}
myFunc(nameOfEmployee: "Joe")

// Omitting External Parameter Names
func myFunc(_ name: String) {}
myFunc("Joe")

// With returned value
func myFunc(/* parameters */) -> Type {
    var valueToReturn: Type
    // Rest of function
    return valueToReturn
}

```

### Operator Overloading
Operators need to be defined as global functions.

```go
func ==(lhs: Person, rhs: Person) {
    return lhs.name == rhs.name
}
```

### Closures (Lambdas)
Closures are unnamed functions that can capture values from their surrounding context.

```go
// Syntax
{ (param1: type, param2: type) -> return type in
    statements
    return param1+param2
}

// Example
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
// Single line
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
// With type inference
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
// Implicit returns from single-expression closures
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
// Shorthand argument names
reversedNames = names.sorted(by: { $0 > $1 } )
// Operator methods
reversedNames = names.sorted(by: >)
// If the closure is the function’s final argument, it can be written as a trailing closure
reversedNames = names.sorted() { $0 > $1 }
// If the closure is the only argument, you can omit the parenthesis
reversedNames = names.sorted { $0 > $1 }
```

#### Variable Capture

```go
func makeCounter() -> (() -> Int) {
    var n = 0
    return {() -> Int in n += 1; return n}
}

let c = makeCounter()
c()     // returns 1
c()     // returns 2
```

#### Escaping Closures

A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns. An example of that is web requests where the request keeps going in the background after the function returns.

```go
// Just add @escaping before the closure arguments
func doStuff(completionHandler: @escaping () -> Void) {
    ...
}
```

_______________________________________________________________________________

## Generics

### Generic Functions
```go
// Passing generic value
func printValue<T>(_ x: T){}
printValue(5)

// Multiple generics
func printValues<T1, T2> (_ x: T1, _ y: T2){}
printValues(5, 1.5)

// Passing object type
func printType<T>(_ x: T.Type){}
printType(Int.Type.self)

// Restrict to types that implement a protocol
func printValue<T: UnsignedInteger>(_ x: T){}

```

### Generic Types

```go
struct MyType<T> {
    value: T
}
// Require T to implement a protocol
struct MyType<T: UnsignedInteger> {}
// We can extend the struct only for types that implement a protocol
extension MyType where T: FixedWidthInteger {}

/* Instantiation */
// Implicit (infers Int)
let x: MyType(value: 5)
// Explicit
let x: MyType<UInt32>(value: 5)
```


_______________________________________________________________________________

## Error Handling
Function calls that throw and error need to be preceded by `try`. There are multiple ways to handle the potential error.
- Handle Error with Do-Catch.
- Convert Error to Optional with try?
- Ignore Error with try!
- Propagate Error.

```go
// Using do-catch. See the next section for more details.
do {
    let text = try String(contentsOfFile: "test.txt")
} catch {
    // The compiler automatically defines an `error` variable that contains the error object
    print(error)
    // A concise description
    print(error.localizedDescription)
}

// Convert Error to Optional
if let text = try? String(contentsOfFile: "test.txt") {
    print(text)
} else {
    print("An error has been thrown")
}

// Force try. Will crash if an error is thrown
let text = try! String(contentsOfFile: "test.txt")
```

### Catching Errors
Each error has a type that allows us to behave accordingly. An easy way to find the error type is be looking up the error code here: <https://osstatus.com>.

All errors can be casted to `NSError`. `NSError`s fall into one of three error domains:
- `CocoaError`
- `MachError`
- `PosixError`

```go
do {
    try ...
}
// Catch all. `error` is defined by the compiler
catch { print(error) }
// Explicitly defining the error object
catch let error {}
// Using error code
catch CocoaError.fileReadUnknown {}
// Using error type
catch is CocoaError {}
// Catch and cast
catch let error as CocoaError {
    switch error.errorCode {
    case CocoaError.fileReadUnknown:
    }
}
// Cast to NSError 
catch let error as NSError {
    print(error.localizedDescription, error.domain, error.code, error.userInfo)
}
```

### Throwing Errors
```go
// A function that throws an error. It propagates an error if it happens in its body.
func doStuff() throws -> String {
    let name = try String(contentsOfFile: "name.txt")
    return name + "is cool"
}

// Propagate manually
catch let error as CocoaError {
    throw error
}

// Throw NSError error
catch {
    throw NSError(domain: "StrangeError", code: 0, userInfo: ["failure": "unknown"])
}

// Throw custom error
enum MyError: Error {
    case runtimeError(String)
}
func someFunction() throws {
    throw MyError.runtimeError("some message")
}
do {
    try someFunction()
} catch MyError.runtimeError(let errorMessage) {
    print(errorMessage)
}
```

### Custom Errors
The recommended method of creating custom errors is an enum that implements the `Error` protocol. Enum associated values are used to provide more information about the error.

```go
enum IntParsingError: Error {
    case overflow
    case invalidInput(Character)
}

// Throwing
throw IntParsingError.invalidInput(c)

// Catching
catch IntParsingError.invalidInput(let invalid) { print("Invalid character: '\(invalid)'") }
catch IntParsingError.overflow { print("Overflow error") }

// As a struct
struct XMLParsingError: Error {
    enum ErrorKind {
        case invalidCharacter
    }
    let line: Int
    let kind: ErrorKind
}
throw XMLParsingError(line: 19, kind: .invalidCharacter)

// LocalizedError
struct InternalError: LocalizedError {
    let localizedDescription: String
    init(_ description: String) {
        localizedDescription = NSLocalizedString(description, comment: "")
    }
}
print(error.localizedDescription)
```

Extra debugging information can also be added by implementing `LocalizedError` and `CustomNSError` protocols.

```go
public protocol CustomNSError : Error {
    public static var errorDomain: String { get }
    public var errorCode: Int { get }
    public var errorUserInfo: [String : Any] { get }
}

extension IntParsingError: CustomNSError {
    // domain and error code...
    /// The user-info dictionary.
    var errorUserInfo: [String: Any] {
        switch self {
        case let .invalidInput(character):
            return [
                "invalidCharacter": character
            ]
        }
    }
}

struct InternalError: LocalizedError {
    let localizedDescription: String
    init(_ description: String) {
        localizedDescription = NSLocalizedString(description, comment: "")
    }
}
```
_______________________________________________________________________________

## IO
```go
print(x)
```

## Math

### Random
```go
// Generate a random Int32
arc4random() -> UInt32
// With an upper bound
arc4random_uniform(_ __upper_bound: UInt32) -> UInt32
// Random array element
let randomIndex = Int(arc4random() % UInt32(myArray.count))
// Float
Float.random(in: 0..<1)
```

_______________________________________________________________________________

