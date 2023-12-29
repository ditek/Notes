# Python
<!-- MarkdownTOC -->

- [Miscellaniuous](#miscellaniuous)
    - [Recommended Code Structure](#recommended-code-structure)
    - [Cygwin Setup](#cygwin-setup)
    - [Multi-file projects](#multi-file-projects)
    - [Other](#other)
- [Operators](#operators)
- [Functions](#functions)
    - [Lambda](#lambda)
- [Classes](#classes)
    - [Syntax](#syntax)
    - [Check if a class attribute exists](#check-if-a-class-attribute-exists)
- [Flow Control](#flow-control)
    - [If-else](#if-else)
    - [Ternary Operator](#ternary-operator)
    - [For Loop](#for-loop)
- [Types](#types)
    - [Type Annotation](#type-annotation)
    - [Strings](#strings)
        - [Functions](#functions-1)
        - [Working with non-ascii strings](#working-with-non-ascii-strings)
    - [Collections](#collections)
        - [Lists](#lists)
        - [Dictionaries](#dictionaries)
        - [Sets](#sets)
        - [Tuples](#tuples)
            - [Definition](#definition)
            - [Operations](#operations)
            - [NamedTuples](#namedtuples)
- [I/O and OS](#io-and-os)
    - [Printing](#printing)
    - [Format Min-language](#format-min-language)
    - [Pretty Print](#pretty-print)
    - [Input](#input)
    - [Command-line Arguments](#command-line-arguments)
    - [File manipulation](#file-manipulation)
        - [Opening files](#opening-files)
        - [Reading](#reading)
        - [File methods](#file-methods)
        - [File auto clean-up \(auto close\)](#file-auto-clean-up-auto-close)
    - [OS Operations](#os-operations)
    - [Issuing shell commands](#issuing-shell-commands)
- [RegEx](#regex)
    - [Groups](#groups)
    - [Examples](#examples)
    - [Regex functions](#regex-functions)
        - [Flags](#flags)
- [Exception Handling](#exception-handling)
- [Python debugger \(pdb\)](#python-debugger-pdb)
- [Libraries](#libraries)
    - [Random](#random)
    - [Timeit](#timeit)
    - [Simple GUI](#simple-gui)
    - [Nose \(Unit Test\)](#nose-unit-test)
    - [Matplotlib](#matplotlib)
    - [PyQt5](#pyqt5)
        - [Components](#components)
        - [Connecting Callbacks \(Slots\)](#connecting-callbacks-slots)
        - [Multithreading](#multithreading)
        - [Other](#other-1)
            - [Change Widget Color](#change-widget-color)
- [Profiling](#profiling)
- [Multithreading](#multithreading-1)
    - [Using `threading` library](#using-threading-library)
    - [Using `ThreadPool`](#using-threadpool)
- [Multiprocessing](#multiprocessing)
    - [`Process` class](#process-class)
    - [`Pool` class](#pool-class)
    - [`joblib.Parallel` class](#joblibparallel-class)
    - [Async IO](#async-io)
    - [Issues](#issues)
- [CSV](#csv)
    - [CSV Reader](#csv-reader)
    - [CSV Writer](#csv-writer)
- [XML](#xml)
    - [Example](#example)
    - [Functions](#functions-2)
- [Web Scrapping](#web-scrapping)
- [Code Snippets](#code-snippets)
    - [Using a dictionary of functions](#using-a-dictionary-of-functions)
    - [Using a dictionary to ease updating values](#using-a-dictionary-to-ease-updating-values)
    - [Google Drive API](#google-drive-api)
    - [Run a Local Web Server](#run-a-local-web-server)

<!-- /MarkdownTOC -->

# Miscellaniuous
## Recommended Code Structure
- Globals
- Helper functions
- Classes
- Defining event handlers
- Frame creation
- Registering event handlers
- Starting frame and timers

## Cygwin Setup
- Install Python IDE and Python for Cygwin (probably already there)
- Download and run ez_setup.py from: https://pypi.python.org/pypi/setuptools
- Use Easy Setup tool for getting packages:
    `$ easy_install BeautifulSoup4`

## Multi-file projects
```python
    from my_file import func    # The function can be called directly: func()
    from my_file import *       # All functions in the file can be called directly (not recommended)
    import my_file              # File name should precede function call: my_file.func()
```

## Other
- Type conversion:
    `int(var)`
- Variable names cannot include a dash.
- If a function contains no return statement it will return None
- Strings and tuples are non-mutable (cannot be modified).
- `:` indicates that the next block is indented
- Python allows fractions to be entered as `.1` (omitting the zero)
- Reimport a module:
    `import importlib; importlib.reload(module)`

---------------------------------------
# Operators
- Arithmatic
    `% //(floor division) **(exponent) += **=`
- Relational and logical
    `== != <> and or not is in`
- Bitwise
    `& | ^ << >> ~`

---------------------------------------
# Functions
If you need to modify a global variable you should declare it inside the function as global first. This is not needed for read access.

```python
def func_name( [param1,param2,...] ):
    [global global_vars]
   "function_doc_string"
   [function_body]
   return [expression]
```

This does not apply to mutation, e.g. in `a[1]=5`, `a` is consider global implicitly.

## Lambda
- A Lambda is a small anonymous function that is needed only at the place of creation.
- Syntax:
    `lambda argument_list: expression`
- Example:
    
```python
sum = lambda x, y : x + y
print(sum(1,2))
functools.reduce(lambda x,y: x+y, [1,2,3,4])
functools.reduce(sum, [1,2,3,4])
```

---------------------------------------
# Enums

Member values can be anything: `int`, `str`, etc.. If the exact value is unimportant you may use `enum.auto` instances and an appropriate value will be chosen for you.

```python
from enum import Enum, auto
class Color(Enum):
    RED = 1
    GREEN = 2

Color.RED.name      # 'RED'
Color.RED.value     # 1

# Auto enums
class Color(Enum):
    RED = auto()
    GREEN = auto()
```

---------------------------------------
# Classes

## Syntax
```python
class MyClass:
    def __int__(self[, arg1, ...])
        "Constructor body"
        self.field1 = arg1
        self.field2 = []
    def __str__(self)
        "Retrurn a string when str(object) is called"
        return str(self.field1)
    def __call__(self[, arg1, ...]):
        "Called when the object name is used as a function. E.g.: obj = MyClass(); obj()"
        ...
    def func(self[, arg1, ...]):
        "A class method"
        ...
def use_class():
    x = MyClass("Testing class")
```

## Check if a class attribute exists
- Method 1
`hasattr(object, 'property')`
- Method 2
`try: doStuff(a.property)`
`except AttributeError: ...`
- Method 3
`getattr(object, 'property', 'default value')`
- Performance

  Method  |Positive|Negative
  --------|--------|--------
  Method1 |  0.446 |  1.87
  Method2 |  0.247 |  3.13

## Data Class
Introduced in Python 3.7, data classes aim to reduce boilerplate for instantiating, printing and comparing class instances.

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int

# OR
from dataclasses import make_dataclass
Person = make_dataclass('Person', ['name', 'age'])
```

That is mostly equivalent to:

```python
class Person
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return (f'{self.__class__.__name__}'
                f'(name={self.name!r}, age={self.age!r})')

    def __eq__(self, other):
        if other.__class__ is not self.__class__:
            return NotImplemented
        return (self.name, self.age) == (other.name, other.age)
```

Fields can have a default value and no type information:

```python
from dataclasses import dataclass
from typing import Any

@dataclass
class Person:
    name: str
    age: int = 0
    other: Any
```

### Field

```python
@dataclass
class Billiard:
    balls: List[BilliardBall] = field(default_factory=make_ball_set)

# To retrieve field information
from dataclasses import fields
fields(Billiard)
# Prints: (Field(name='balls',type=<class 'List[BilliardBall]'>, ...), ...)
```

The field() specifier is used to customize each field of a data class individually. You will see some other examples later. For reference, these are the parameters field() supports:

- `default`: Default value of the field
- `default_factory`: Function that returns the initial value of the field
- `init`: Use field in `.__init__()` method? (Default is True.)
- `repr`: Use field in `repr` of the object? (Default is True.)
- `compare`: Include the field in comparisons? (Default is True.)
- `hash`: Include the field when calculating `hash()`? (Default is to use the same as for `compare`.)
- `metadata`: A mapping with information about the field

### `@dataclass` decorator

- `init`: Add `.__init__()` method? (Default is True.)
- `repr`: Add `.__repr__()` method? (Default is True.)
- `eq`: Add `.__eq__()` method? (Default is True.)
- `order`: Add ordering methods? (Default is False.)
- `unsafe_hash`: Force the addition of a `.__hash__()` method? (Default is False.)
- `frozen`: If True, assigning to fields raise an exception, i.e. it makes the class immutable. (Default is False.)

__order__

If we want to enable ordering, but don't like the default order, we can declare a sort index and set its value in `__post_init__()`:

```python
@dataclass(order=True)
class Person:
    sort_index: int = field(init=False, repr=False)
    name: str
    age: int

    def __post_init__(self):
        self.sort_index = calculate_index(name, age)
```

## Optimizing Classes (Slots)
slots are defined using `.__slots__` to list the variables on a class. Variables or attributes not present in `.__slots__` may not be defined. Furthermore, a slots class may not have default values.

The benefit of adding such restrictions is that certain optimizations may be done. For instance, slots classes take up less memory and are faster to work with.

(See https://realpython.com/python-data-classes)

```python
from dataclasses import dataclass

@dataclass
class SimplePosition:
    name: str
    lon: float
    lat: float

@dataclass
class SlotPosition:
    __slots__ = ['name', 'lon', 'lat']
    name: str
    lon: float
    lat: float
```

```python
>>> from pympler import asizeof
>>> simple = SimplePosition('London', -0.1, 51.5)
>>> slot = SlotPosition('Madrid', -3.7, 40.4)
>>> asizeof.asizesof(simple, slot)
(440, 248)
```

```python
>>> from timeit import timeit
>>> timeit('slot.name', setup="slot=SlotPosition('Oslo', 10.8, 59.9)", globals=globals())
0.05882283499886398
>>> timeit('simple.name', setup="simple=SimplePosition('Oslo', 10.8, 59.9)", globals=globals())
0.09207444800267695
```

---------------------------------------
# Flow Control

## If-else
```python
    if x > 10:
        x += 1
    elif x < 5:
        x -= 1
    else:
        x += 2
```

## Ternary Operator
```python
    x = 'paff' if codec=='h264' else 'mbaff'        # 'else' is necessary
```

## For Loop
```python
# Loop over lists:
    for x in [1,4,5,10]:
        print x
# Loop over dictionaries, you get keys:
    prices = { 'GOOG' : 490.10,'AAPL' : 145.23,'YHOO' : 21.71 }
    for key in prices:
        print key
# Loop over a string, you get characters
    for c in s:
        print c
# Loop over a file, you get lines
    for line in open("real.txt"):
        print line
```

## With
Objects which provide predefined clean-up actions can be used within with structure

```python
    with open("myfile.txt") as f:
        [file_operations]
```

---------------------------------------
# Types

## Type Annotation
Used for code documentation and to help the IDE with code checking. However, this is not enforced by the interpreter.

__Note__

`Dict`, `DefaultDict`, `List`, `Set` and `FrozenSet` are mainly useful for annotating return values. For arguments, prefer the abstract collection types defined below, e.g. `Mapping`, `Sequence` or `AbstractSet`.

```python
import typing
from typing import List, NoReturn
def f1(a: str, b: int) -> bool: pass
def f2(a: List, b: float) -> List[int]: pass
def f5(a: List, b: float) -> NoReturn: pass
# One of multiple types
Union[str,int]
# Nullable. The following are equivalent
Union[int,None]
Optional[int]
# Returning multiple values
Tuple[str, int]
Tuple[int, ...] # Arbitrary length of ints
Tuple[()]       # Empty tuple
# Callable
Callable[[Arg1Type, Arg2Type], ReturnType]

# From Py3.9 the following is possible without importing 'typing'
list[int]
tuple[str, int] 
dict[str, str]

# From 3.10, Union[x,y] can be written as x|y
str|int
```

## Type Casting and Conversion
```python
str()       # Convert to str
int()       # Convert to int
int(s, 16)  # Hex string to int

bytes.fromhex(s)    # Hex string (e.g. 'ab12') to bytes
b.hex()     # bytes to hex
b.decode()  # bytes to str (utf-8 by default)
s.encode()  # str to bytes (utf-8 by default)

# bytes to int
int.from_bytes(b, byteorder='little')
```

## Type Checking
```python
# Use isinstance to check if o is an instance of str or any subclass of str:
if isinstance(o, str):

# To check if the type of o is exactly str, excluding subclasses of str:
if type(o) is str:
```

## Bytes
A `bytes` object is an array of bytes. It can also be defined similar to a string if we only use asscii characters.

```python
b = b'hello'
b = bytes([104, 101, 108, 108, 111])
```

## Strings
- A string can be used as an array with `s[0]` its first letter and `s[-1]` its last letter.
- String slicing:
 
```python
s[1:5] = s[1] -> s[4]
s[1:]  = s[1] -> s[len(s)-1]
s[:5]  = s[0] -> s[4]
```

- Comparing strings: Simply done by testing equality (== or !=)

### Functions
```python
    str.split(sep=None, maxsplit=-1)    # Return a list of strings in str which are separated by sep.
    '1.2.3'.split('.')                  # ['1','2','3']
    str.join(iterable)                  # Return the concatenation of the strings in the iterable separated by str.
    '.'.join(['1', '2'])                # '1.2'
    if sub_str in str1: ...
    str.find(sub[, start[, end]])       # Return first occurance index of sub within s[start:end]. Return -1 if not found.
    str.count(sub[, start[, end]])      # Return the number of non-overlapping occurrences of sub within s[start, end]
    str.format(*args, **kwargs)         # Perform a string formatting operation.
    str.isdigit()                       # Return true if all characters are digits and there is at least one character
    # Evaluate a string as an expression
    y = eval('[x*5 for x in range(2,10,2)]')    # y = [10, 20, 30, 40]
```

### Working with non-ascii strings
Python 3 uses `utf-8` as the default source code encoding.

Python 2 uses `ASCII` by default, so unless you explicitly tell Python `# -*- coding: utf-8 -*-` at the top of your file, it doesn't know how to handle character values above 127.

---------------------------------------
## Collections

### Lists
- They can contain objects of different data types.
- Creating a list:

```python
list1 = [0] * size        #Initializing the list
list1 = ["a", "b", 1, (1,2)];
list2 = [n**2 for n in list1]
list2 = [n for n in list1 if n>0]
list1 = list(<iterable>)        # Convert an iterable (tuple, etc)into a list (deep copy).
list1 = list(range(stop))               # start=0, step=1
list1 = list(range(start, stop))        # step=1
list1 = list(range(start, stop, step))  # step=1
list1 = list(range(n))                  # Same as range(0,n,1)
```

__Operations__

```python
# Concatenation
[1, 2, 3] + [4, 5, 6]   # [1, 2, 3, 4, 5, 6]

# Repetition
['Hi!'] * 4             # ['Hi!', 'Hi!', 'Hi!', 'Hi!']

# Accessing elements
lst[0]          # first element
lst[-1]         # last element.
lst[1:5]        # lst[1] -> lst[4]
lst[1:]         # lst[1] -> lst[len(lst)-1]
lst[:5]         # lst[0] -> lst[4]

# Testing memebershipo
if 2 in lst: ...

# Intersection
list(set([1, 2, 3]) & set(2, 3, 4))     # [2, 3]

# Difference between two lists
## If items are hashable
temp3 = set(temp1) - set(temp2)
## If items are not hashable
temp3 = [item for item in temp1 if item not in temp2]
```

__List functions__
 
```python
lst.index('a')          # returns the index of the first 'a' or -1 if not found
lst.append('a')         # adds 'a' to the end of the list
lst.extend(<iterable>)  # Append each item from an iterable to lst.
lst.extend(Arr2)
lst.insert(idx, obj)    # Add obj to lst at idx.
lst.insert(0, 'a')
lst.pop([idx])          # Pops (returns and removes) the element at idx if provided. Pops the last element if not provided.
lst.remove(obj)         # Looks for obj and remove its first occurrence from lst. Issues an error if not found.
lst.reverse()
lst.count('a')          # how many times it appears
del lst[2]
max_item = max(lst)
min_item = min(lst)
sum_list = sum(lst)
list2 = filter(lambda x: x!=0, list1)           # Python2: return non-zero elements of list1
list2 = list(filter(lambda x: x!=0, list1))     # Python3 version
list2 = functools.reduce(lambda x,y: x+y, [1,2,3,4])    # P3: Apply a func on all elements in pairs
item = next(x for x in lst if ...)              # Find the first occurrence or raise a StopIteration if none is found.
item = next((x for x in lst if ...), [default_value])   # Return default_value if not found
```

#### Sorting
```python
# Sort lst items in ascending order
lst.sort([args])
# Sort with a custom soring key, e.g. the part following the last '/'
sorted_list = sorted(url_list, key=lambda x: x.rsplit('/', 1)[-1])
```

__List iteration__

```python
for i in xrange(5, len(lst)-1):
for i in xrange(len(lst)-1):
    lst[i]=...
for item in lst: ...
```

- _NOTE: You cannot modify a list while iterating on it. Instead, put the elements to modify in another list,  loop on `list(lst)` or use:_
    `somelist[:] = [x for x in somelist if should_keep(x)]`

---------------------------------------
### Dictionaries
- A dictionary is a mapping between keys and values
- Keys can be any non mutable value like numbers, strings or tuples. Values can be any data type.

```python
# Instantiation
    dict = {<key1>:<val1>, <key2>:<val2>, ...}
    dict = {1:'x', 'abc':53, (1,2):[1,2,3]}
# Accessing elements
    dict[<key>] = <new_val>
    # NOTE: Trying to write to a non-existing key will create a new element with that key
    dict[5] = 2         # If key 5 does not exist it will create it.
# Dictionary iteration
    for key in dict:
    for key, value in dict.items():
# Apply function to dictionary values
    dict2 = {key:func(val) for key, val in dict.items()}
# Getting max/min:
    key_of_max = max(mydict, key=mydict.get)
# Check if an item is in a dict
    if 'item' in d: ...
```

### OrderedDict
Since Python 3.7, `dict` conserves ordereing. However, another type of dict exists that offeres more ordering features in addition to signaling that ordering is intended.
`OrderedDict` is used almost exactly like `dict`.

```python
from collections import OrderedDict

numbers = OrderedDict([("one", 1), ("two", 2), ("three", 3)])
numbers = OrderedDict({"one": 1, "two": 2, "three": 3})
numbers = OrderedDict(one=1, two=2, three=3)
numbers["one"] = 2
```

---------------------------------------
### Sets
- A set is an unordered collection of unique elements.
- Sets allow faster manipulation of their elements.

```python
# Creating a set
    set1 = set(<iterable>)
    set1 = set([1,2,2,2])        # will include [1,2] only
    set3 = set()                # an empty set
# Functions
    set1.add/remove(obj)                # add/remove obj
    set1.discard(obj)                   # remove obj. Don't  throw an exception when not found
    set2 = set1.union(<iter>)           # return the union of set1 and iter
    set1.update(<iter>)                 # mutates set1 to its union with iter
    set1.difference_update(<iter>)      # remove set1 elements that exist in an iterable
    set2 = set1.intersection(<iter>)    # returns the intersection b/w set1 and iter
    set1.intersection_update(<iter>)    # update set1 to contain the intersection
    set1.issubset/issuperset(<iter>)    # checks whether set1 contains/is contained in iter
    set(set1) & set(set2)               # Set intersection
```

---------------------------------------
### Tuples
- A `tuple` is a sequence of immutable Python objects.
- The differences between tuples and lists are:
  - Tuples cannot be changed unlike lists
  - Tuples use parentheses, whereas lists use square brackets.

#### Definition
```python
# Parentheses are optional when defining a tuple
    tup0 = ();      # Empty tuple
    tup1 = ('physics', 'chemistry', 1997, 2000);
    tup2 = (1, 2, 3, 4, 5 );
    tup3 = "a", "b", "c", "d";
# Tuple declaration must include at least one comma, even if it contains a single value.
    tup1 = (50,);
```

#### Operations
```python
# Assignment
    t1 = t2     # t1 and t2 will point to the same object
# Copy: Tuple assignment returns a reference. To copy a tuple it should be converted to a list first
    tuple2 = list(tuple1)
# Concatenation
    (1, 2, 3) + (4, 5, 6)    # (1, 2, 3, 4, 5, 6)
# Repetition
    ('Hi!',) * 4        # ('Hi!', 'Hi!', 'Hi!', 'Hi!')
```

#### NamedTuples
- Named tuples assign meaning to each position in a tuple.
- They can be used wherever regular tuples are used, and they add the ability to access fields by name instead of position index.

```python
# Definition:
    namedtuple(typename, field_names)
# Usage:
    from collections import namedtuple
    Point = namedtuple('Point', ['x', 'y'])
    p = Point(11, y=22)               # instantiate with positional or keyword arguments
    sum_res = p[0] + p[1]             # indexable like the plain tuple (11, 22)
    sum_res = p.x + p.y               # fields also accessible by name
    x, y = p                          # unpack like a regular tuple
    print(p)                          # >> Point(x=11, y=22)
    # Convert tuple to namedtuple
    t = (1, 2)
    named_t = Point(*t)
    named_t = Point._make(t)
```

---------------------------------------
# I/O and OS

## Printing and Formatting
```python
# Python 2
    print expression1 [, expression2] [, ...]
    print "Number", x, "isn't too much"
    print "Line No %d in %s" % (10, "test.py")
# Python 3
    print(expression1[, expression2, ...])
    print("Number", x, "isn't too much")
    print("Line No %d" % 10)
    print("Line No %d in %s" % (10, "test.py"))
```

Using format:

```python
    print("Line No {} in {}".format(10, "test.py"))
    "First, thou shalt count to {0}"  # References first positional argument
    "Bring me a {}"                   # Implicitly references the first positional argument
    "From {} to {}"                   # Same as "From {0} to {1}"
    "My quest is {name}"              # References keyword argument 'name'
    "Weight in tons {0.weight}"       # 'weight' attribute of first positional arg
    "Units destroyed: {players[0]}"   # First element of keyword argument 'players'.
    "Harold's a clever {0!s}"         # Calls str() on the argument first
    "Bring out the holy {name!r}"     # Calls repr() on the argument first
    "More {!a}"                       # Calls ascii() on the argument first
```

### Format Min-language
```
    format_spec ::=  [[fill]align][sign][#][0][width][,][.precision][type]
    fill        ::=  <any character>
    align       ::=  "<" | ">" | "=" | "^"
    sign        ::=  "+" | "-" | " "
    #           ::   Valid for binary, octal, or hexadecimal output. Prefixes the output by '0b', '0o', or '0x'.
    ,           ::   Use of a comma for a thousands separator
    width       ::=  integer
    precision   ::=  integer
    type        ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "x" | "X" | "%"
```

```python
    '{:0>4}'.format('Hi')                 # '00Hi'
    '{:<30}'.format('left aligned')       # 'left aligned                  '
    '{:>30}'.format('right aligned')      # '                 right aligned'
    '{:^30}'.format('centered')           # '           centered           '
    '{:*^30}'.format('centered')          # '***********centered***********'
    'Percentage: {:.2%}'.format(1.0/3.0)  # 'Percentage: 33.33%'

    person = {'name': 'Eric', 'age': 74}
    'Hello, {name}. You are {age}'.format(**person)
```

### Formatting with f-Strings

```python
name = "John"
f"Hello, {name}"        # Hello, John
f"{2 * 37}"             # '74'
f"{name.lower()}"       # john
```

### Pretty Print
```python
    import pprint
    class pprint.PrettyPrinter(indent=1, width=80, depth=None, stream=None, *, compact=False):
    PrettyPrinter.pprint(object)    # Print the formatted representation of object
    PrettyPrinter.pformat(object)   # Print the formatted representation of object
    # Example:
    pp = pprint.PrettyPrinter(indent=4)
    pp.pprint(stuff)
```

### `__str__` and `__repr__`
`__str__` and `__repr__` help getting useful information about your object by calling `str(my_obj)` and `repr(my_obj)` respectively.

- `__repr__` is a representation of a Python object that can potentially be converted back to that object using `eval()`.
- `__str__` is the object in text form.

```python
>>> import datetime
>>> today = datetime.datetime.now()
>>> str(today)
'2012-03-14 09:21:58.130922'
>>> repr(today)
'datetime.datetime(2012, 3, 14, 9, 21, 58, 130922)'
```

## Input
```python
    # Read one line and return it
    str_in = input("Enter your input: ")
```

## Command-line Arguments and Doc Strings
The easiest way is to use `sys.argv`. The arguments start from `arg[1]` while the script name is `arg[0]`

```python
"""
Description:
    Get name and age
Usage:
    python {script_name} name [-a age(default=10)]
Example:
    python {script_name} Jon -a 20
"""
import sys
if __name__ == '__main__':
    if len(sys.argv) < 2:
        scriptname = sys.argv[0]
        print(__doc__.format(script_name=scriptname))
        sys.exit()
    filename = sys.argv[1]
    process_file(filename)
```

If option arguments are needed we can use `getopt`.

```python
import getopt, sys
try:
    # `arguments` is a list of non-option arguments.
    # Here we define o
    options, arguments = getopt.gnu_getopt(sys.argv[1:], "ha:")
    name = arguments[0]
except:
    print(__doc__.format(script_name=sys.argv[0]))
    sys.exit(2)
age = 10
for o, a in options:
    if o == "-h":
        print(__doc__)
        sys.exit(0)
    elif o == "-a":
        age = int(a)
```

## External call and CMD commands
```python
import subprocess
subprocess.run(["ls", "-l"])
# The returned instance will have attributes args, returncode, stdout and stderr. By default, stdout and stderr are not captured, and those attributes will be None. Pass stdout=PIPE and/or stderr=PIPE in order to capture them.
subprocess.run(["ls", "-l"], stdout=subprocess.PIPE)

```

## File manipulation

### Opening files
```python
    f = open(file_name [, access_mode])
    # File auto clean-up (auto close)
    with open("myfile.txt") as f:
        [file_operations]
```

**Access modes:**

```
    'r'     read only, default mode
    'r+'    read/write
    'w'     open for writing only, truncates on opening, create if doesn't exist
    'w+'    open for read/write, truncates on opening, create if doesn't exist
    'a'     append (create if doesn't exist)
    'a+'    append/read (create if doesn't exist)
    '?b'    open the file in binary format (e.g. 'wb+')

|          Mode          |  r   |  r+  |  w   |  w+  |  a   |  a+  |
| :--------------------: | :--: | :--: | :--: | :--: | :--: | :--: |
|          Read          |  +   |  +   |      |  +   |      |  +   |
|         Write          |      |  +   |  +   |  +   |  +   |  +   |
|         Create         |      |      |  +   |  +   |  +   |  +   |
|         Cover          |      |      |  +   |  +   |      |      |
| Point in the beginning |  +   |  +   |  +   |  +   |      |      |
|    Point in the end    |      |      |      |      |  +   |  +   |
```

### Reading
```python
    f.read([N])             # Reads N bytes. If N isn't specified it will try to read all
    f.tell()                # Return the current position
    f.seek(N[,START])       # Moves the position for N bytes depending on START
    lines = f.readlines()   # Read f into a list
    line = f.readline([N])  # Read one line at a time. If N is provided, read N characters
    while line:
        line = f.readline()
    # Read using iterator
    for line in iter(f):
        print line
```

### Edit file contents
```python
with open("myfile.txt", 'r') as f:
    contents = f.read()
contents += 'changes'
with open("myfile.txt", 'w') as f:
    f.write(contents)
```

### File methods
```python
    f.close()
    f.closed        # Check if file is closed
    f.mode          # Return access mode
    f.name
    f.write(string)
    f.writelines(sequence)
    # Check that a file/directory exists
    from pathlib import Path
    my_file = Path("/path/to/file")
    if my_file.is_file():...
    if my_file.is_dir():...
    if my_file.exists():...
```


## OS Operations
```python
    import os
    os.rename(file_name, new_name)
    os.remove(file_name)
    os.mkdir(new_dir_name)
    os.chdir("/home/newdir")
    os.rmdir("/tmp/test")
    os.listdir('cpptoolsEn')
    os.getcwd()                 # Get current working directory
    # Remove non-empty directory
    shutil.rmtree('/folder_name')
    # Join path
    full_filename = os.path.join(path, filename)

    import shutil
    shutil.copy2(src, dst)
```

## Path

### Relative Paths
Using a relative path in a script (e.g. `../file.txt`) would only work if the script is launched from its location since the path would resolve relative to the cli cwd. To get around this we do the following.

```python
from pathlib import Path
# Path to a file located in the parent folder
def get_full_path(path: str) -> str:
    return str(Path.joinpath(Path(__file__).parent, path))

```

### Home Directory
```python
Path.home()
```

## Running shell commands
Run command with no output.

```python
status_code = os.system('ls -l')
```

Run command and get output.

```python
stream = os.popen('echo Returned output')
output = stream.read()
# 'Returned output\n'
```

Do more.

```python
    import subprocess
    cmd = 'cp file1 file2'
    # The command needs to be passed as a list of words so we use split()
    process = subprocess.Popen(cmd.split(), stdout=subprocess.PIPE)     # Non-blocking
    process = subprocess.call(cmd.split(), stdout=subprocess.PIPE)      # Blocking
    output = process.communicate()[0]
    if 'Failed' in str(output): ...
    # Using aliases in a shell command:
    subprocess.call(['/bin/bash', '-i', '-c', cmd_alias])
```

---------------------------------------
# RegEx
    .           any character except newline [^\n\r]
    [\s\S]      any character including line breaks.
    \w          low-ascii word character (alphanumeric & underscore) [A-Za-z0-9_]
    \d          digit [0-9]
    \s          whitespace [ \t\n]
    \W \D \S    not word, digit, whitespace
    [abc]       any of a, b, or c
    [^abc]      not a, b, or c
    [a-g]       character between a & g
    a* a+ a?    0 or more, 1 or more, 0 or 1
    a{5} a{2,}  exactly five, two or more
    a{1,3}      between one & three
    a+? a{2,}?  match as few as possible (examples 5, 6)
    ab|cd       match "ab" or "cd"
    (?:ab|cd)   match "ab" or "cd"
    ^ $         beginning/end of string respectively
    \b          word boundary
    \1          back reference to group1 (example 1)
    (?:abc)     non-capturing group
    (?=abc)     positive lookahead. Matches a group after an expression without including it (example 2)
    (?!abc)     negative lookahead. Discards a match if the group comes after an expression (example 3)

## Groups
```python
# Grouping is the ability to address certain sub-parts of the entire regex match.
    match = re.search(r'(\w+): (\S+)', 'Doe, John: 555-1212')
    match.group(0)          # 'John: 555-1212'
    match.group(1)          # 'John'
    match.group(2)          # '555-1212'
# Grouping by Name
    match = re.search(r'(?P<last>\w+), (?P<first>\w+): (?P<phone>\S+)', 'Doe, John: 555-1212')
    match.group('last')     # 'Doe'
# Groups using re.findall: The returned value a list of tuples of the found groups. It does not support named groups.
    re.findall(r'(\w+), (\w+): (\S+)', 'Doe, John: 555-1212')   # [('Doe', 'John', '555-1212')]
# It is possible to back-reference a group in the same expression:
    re.search(r'(\w)x\1', 'HxH HxG')    # 'HxH'
```

## Examples
    1- (\w)a\1      hah dad bad dab gag gab =>  hah dad gag
    2- \d(?=px)     1pt 2px 3em 4px         =>  2 4
    3- \d(?!px)     1pt 2px 3em 4px         =>  1 3
    4- colou?r      color colour
    5- <(.*)>       <h>Text</h>             =>  h>Text</h
    6- <(.*?)>      <h>Text</h>             =>  Text

## Regex functions
```python
# Check for a match only at the beginning of the string
re.match(pattern, string, flags=0)
# Check for a match anywhere in the string but stops at the first occurrence
re.search(pattern, string, flags=0)
# Split string by the occurrences of `pattern`
# >>> re.split('\W+', 'Words, words, words.')     =>      ['Words', 'words', 'words', '']
re.split(pattern, string, maxsplit=0, flags=0)
# Return all non-overlapping matches of `pattern` in a string as a list of strings.
# If one or more groups are present in the pattern, return a list of groups.
re.findall(pattern, string, flags=0)
# Split `string` by the occurrences of `pattern`.
# If groups are used in `pattern`, then the text of all groups in the pattern are also returned as part of the resulting list.
# If `maxsplit` is nonzero, at most `maxsplit` splits occur, and the remainder of the string is returned as the final element of the list.
# >>> re.split('[a-f]+', '0a3b9')         =>      ['0', '3', '9']
# >>> re.split('([a-f])+', '0ab3bc9')     =>      ['0', 'a', '3', 'b', '9']
re.split(pattern, string, maxsplit=0, flags=0)
# Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.
# >>> re.sub(r'(\w+)\sAND\s(\w+)', '\2 & \1', 'Beans And Spam'    =>    'Spam & Beans'
re.sub(pattern, repl, string, count=0, flags=0)
# Return the index of the match in the original string
matchObject.start()
```

### Flags
    re.DOTALL       Make '.' match anything including new line '\n'
    re.MULTILINE    Symbols '^' and '$' match the beginning and end of each line
    re.IGNORECASE   Case insensetive look up


---------------------------------------
# Exception Handling
```python
if x:
    raise Exception('My error!')
try:
    [statements]
    raise NameError('HiThere')
# Catch one exception
except ValueError:
    pass
# Catch several exceptions
except (RuntimeError, TypeError, NameError):
    pass
# Create a variable of type Exception with exception info
except OSError as err:
    print("OS error: {}".format(err))
# Catch everything not captured in earlier excepts
except:
    # Get exception info
    print("Unexpected error:", sys.exc_info()[0])
    # Re-raise the exception after reporting it for example
    raise
else:
    # Code that must be executed if the try clause does not raise an exception
finally:
    # Code that must always be excecuted even if except returns
    # or raises another exception

# Getting the value passed when the exception was created
e.args[0]
```

---------------------------------------
# Python debugger (pdb)
To break execution and run pdb:
    `import pdb; pdb.set_trace()`

**Useful PDB commands:**

    p var           print
    pp var          pretty print
    ! statement     Execute the (one-line) statement in the context of the current stack frame.
                    The '!' can be omitted unless the first word of the statement resembles a debugger command.
    interact        Start an interactive Python interpreter
    w(here)         Print a stack trace, with the most recent frame at the bottom.
    u(up)           go up in call stack
    d(own)          go down in call stack
    l [n1[, n2]]    no args: list 11 lines of code around current line
                    1 arg: list 11 lines around n1
                    2 args: list lines between n1 and n2
    ll(longlist)    List all source code for the current function or frame
    a(rgs)          Print the argument list of the current function.
    whatis expr     Print the type of the expression.
    interact        Start an interative interpreter
    s(tep)          Step in: Step to the next statement. If it is a function step into it.
    n(ext)          Step over: Step to the next statement in the current function.
    unt(il) [line]  With an arg, execute until the line is reached or the frame returns.
    r(eturn)        Continue execution until the current function returns.
    c(ont(inue))    Continue execution until the next breakpoint
    j(ump) lineno   Set the next line that will be executed. Only available in the bottom-most frame.
                    This lets you jump back and execute code again, or jump forward to skip code that you don’t want to run.
                    Not all jumps are allowed – e.g. you cannot jump into the middle of a for loop or out of a finally clause.
    q(uit)          Quit from the debugger. The program being executed is aborted.

---------------------------------------
# Virtual Environment and Requirements.txt

```sh
# Create a new virtual environment
python3 -m venv venv
# Source it
source venv/bin/activate
# Install all the needed packages
# Create the requirements file
pip freeze > requirements.txt
# Next time, you can just install the requirements
pip install -r requirements.txt
```

Using `virtualenv`:

```sh
pip3 install virtualenv
virtualenv venv
```

Usage:

```sh
# On MacOS/Linux/WSL
source venv/bin/activate
# On Windows - Powershell
powershell Set-ExecutionPolicy RemoteSigned
./venv/Scripts/Activate.ps1
# On Windows - Git Bash
source venv/Scripts/activate
# Deactivate
deactivate
```

## Platform specific requirements
Requirements can be customized for platform and Python version.
Valid `sys_platform` values: `darwin, win32, linux`.

```python
kivy-deps.sdl2==0.3.1; sys_platform == 'win32'
futures>=3.0.5; python_version < '3.0'
futures>=3.0.5; python_version == '2.6' or python_version=='2.7'
```

---------------------------------------
# Libraries & Frameworks

## Random
```python
  import random
  random.shuffle(list)                    # Shuffles the elements of a list or a tring
  random.choice(list)                     # Return a random item from the list
  random.randrange(start=0, stop, step=1) # Return start <= n < stop
  random.randint(start, stop)             # Return start <= n <= stop
  round(random.uniform(1.5,2.5), N)       # Random float with N digits
```

## DateTime
```python
import datetime
# str to time
# %y - 22
# %Y - 2022
t = datetime.strptime('11:15:49', '%H:%M:%S')
t = datetime.strptime('2023-07-26 15:10:01.196141', '%Y-%m-%d %H:%M:%S.%f')

# Current time
t = datetime.datetime.now()
>>> 2023-07-26 14:42:27.040442

# Local to ISO 8601:
t.isoformat()
>>> 2020-03-20T14:28:23.382748
# UTC to ISO 8601:
datetime.datetime.utcnow().isoformat()
>>> 2020-03-20T01:30:08.180856
# Local to ISO 8601 without microsecond:
t.replace(microsecond=0).isoformat()
>>> 2020-03-20T14:30:43
# UTC to ISO 8601 with TimeZone information (Python 3):
datetime.datetime.utcnow().replace(tzinfo=datetime.timezone.utc).isoformat()
>>> 2020-03-20T01:31:12.467113+00:00
# UTC to ISO 8601 with Local TimeZone information without microsecond (Python 3):
t.astimezone().replace(microsecond=0).isoformat()
>>> 2020-03-20T14:31:43+13:00
# Local to ISO 8601 with TimeZone information (Python 3):
t.astimezone().isoformat()
>>> 2020-03-20T14:32:16.458361+13:00
# Get just the time part
t.strftime('%H:%M:%S')
>>> 14:32:16

# Delta
delta = datetime.now() - prev_t
if delta.seconds/3600 > 11.5:...

# Date
from datetime import date
date.fromordinal(730920) # 730920th day after 1. 1. 0001
>>>datetime.date(2002, 3, 11)
t.isoformat()
>>>'2002-03-11'
t.strftime("%d/%m/%y")
>>>'11/03/02'
t.strftime("%A %d. %B %Y")
>>>'Monday 11. March 2002'
t.ctime()
>>>'Mon Mar 11 00:00:00 2002'
```

## Timeit
- From command-line interface:
    `$ python -m timeit [-n number] [-s setup] [statement ...]`
    - If `-n` is not given, a suitable number of loops is calculated by trying successive powers of 10 until the total time is at least 0.2 seconds.
    - Example:
        `$ python -m timeit '"-".join(str(n) for n in range(100))'`
- From within Python:

```python
# Syntax
    # `setup`: statement to be executed once initially
    timeit.timeit(stmt='pass', setup='pass', number=1000000, globals=None)
# Example:
    import timeit
    timeit.timeit('"-".join(str(n) for n in range(100))', number=10000)
    timeit.timeit('my_func(10)', globals=globals())    # execute the code within your current global namespace
```

## Simple GUI
```python
# Import
    import simplegui
# Frame creation
    frame1 = simplegui.create_frame(title, canvas_width, canvas_height [, control_width])
# Starting a Frame
    frame1.start()
# Adding a Label
    [label1 =] frame1.add_label(text [, width])
# Changing label text
    label1.set_text("New Text")
# Adding a Botton
    def button_handler():...
    frame1.add_button(text, button_handler [, width])
# Adding an Input
    def input_handler(string):...
    frame1.add_input(text, input_handler , width)
# Timer creation
    def timer_handler():...
    timer1 = simplegui.create_timer(interval_ms, timer_handler)
# Starting a Timer
    timer1.start()
# Set Draw Handler
    def draw_handler(canvas):...
    frame.set_draw_handler(draw_handler)
# Draw Text
    canvas.draw_text(text, point, font_size, font_color[, font_face])
# Draw a Circle
    canvas.draw_circle(center_point, radius, line_width, line_color[, fill_color])
# Draw a polygon
    canvas.draw_polygon(point_list, line_width, line_color, fill_color = color)
# Key down event
    def keydown_handler(key): k = chr(key)
    frame.set_keydown_handler(keydown_handler)
# Key up enent
    def keyup_handler(key): k = ' '
    frame.set_keyup_handler(keyup_handler)
# SimpleGUI Key map
    if key == simplegui.KEY_MAP["left"]
# Mouse click
    def mouseclick_handler(position):        # position is a tuple of two integers (x, y)
    frame.set_mouseclick_handler(mouseclick_handler)
# Images
    # Load an image
    img = simplegui.load_image(URL)
    # Draw an image
    canvas.draw_image(img, src_center, src_size, dst_center, dst_size, angle=0)
# Sounds
    music = simplegui.load_sound("http://commondatastorage.googleapis.com/codeskulptor-assets/Epoq-Lepidoptera.ogg")
    music.play()            # play some music, starts at last paused spot
    music.pause()
    music.rewind()          # rewind the music to the beginning
    music.set_volume(0.5)   # Set volume to a value between 0-1.0
```

## Nose (Unit Test)
Every file starts with `test` is considered a test file. Every function starts with `test` is considered a test function.

A `setup`/`teardown` function can be called before/after running the test using `with_setup` decorator:

```python
@with_setup(setup, teardown)
def test_something():
    ...
```

## PyTest
Install Pytest:

```
pip install -U pytest
```

Run pytest:

```
pytest
```

```python
# test_great_functions.py
from great_functions import add

def test_add_1_4():
    assert(add(1, 4) == 5)
```

## Matplotlib
```python
import matplotlib.pyplot as plt

# Figure title
plt.figure().canvas.set_window_title('Ideal Signal')

# Use subplot 1 in a 1x2 grid
plt.subplot(121)

# Draw plot
plt.plot(data, label="Profit", color='red')

# A scatter plot
plt.scatter(x, y)

# Show legend
plt.legend( loc=1, borderaxespad=0.)

# Axis labels
ax1.set_xlabel('Time')

# Show plot
plt.show()

# Close plot
plt.close()
```

## Numpy

```python
# Intersection
arr = np.intersect1d(arr1, arr2)
# convert elemnt types
arr = np.array(arr).astype(int)

# Filtering elements
arr2 = arr[arr < 25]                # Elements less than 25
# Slightly faster
arr2 = arr[np.where(arr < 25)]

# Arithmatics
arr2 = arr1 * 2
arr2 = arr1.sum()
arr2 = np.sum(arr1)
```

---------------------------------------
## PyQt5

### Components

```python
    # ComboBox
    self.mode_box = QtWidgets.QComboBox()
    self.mode_box.addItem("Telnet")
    # Edit Box
    self.edit_box = QtWidgets.QLineEdit()
    self.edit_box.setMaxLength(25)
    self.edit_box.setMaximumSize(40, 20)
    self.edit_box.setAlignment(QtCore.Qt.AlignCenter)
    self.edit_box.setEnabled(False)  # True by default
    # Button
    self.button = QtWidgets.QPushButton("Connect")
    self.button.setSizePolicy(QtWidgets.QSizePolicy.Minimum, QtWidgets.QSizePolicy.Preferred)  # Size fits contents
    # Checkbox
    self.proxy = QtWidgets.QCheckBox("Proxy")
    self.proxy.setTristate(False)
    # Toolbar
    self.ToolBar = self.addToolBar("Connect")
    self.ToolBar.setMovable(False)
    self.ToolBar.addWidget(self.mode_box)
    self.ToolBar.addSeparator()
    self.ToolBar.addWidget(self.edit_box)
    # Statusbar
    self.status_bar = self.statusBar()
    self.status_bar.showMessage("Idle")
    # Timer
    self.timer = QtCore.QTimer()
    self.timer.setInterval(10000)
    self.timer.timeout.connect(self.perform_action)
    self.timer.start()
```

### Connecting Callbacks (Slots)
```python
    edit_box.returnPressed.connect(my_handler)
    self.button.clicked.connect(my_handler)

    def my_handler():
        pass
```

### Multithreading
- Threads communicate using signals (`pyqtSignal`).
- A `pyqtSignal` has to be defined within a class derived from `QObject`. That can be a `QThread` or a custom class.
- An optional decorator `@pyqtSlot` can be added to provide more efficiency and readablility.
- Threads automatically emmit `started` and `finished` signals, which can be connected to slots.

```python
class DebugMonitor(QtCore.QObject):
    # The type(s) of the signal parameter(s) need to be specified
    error_signal = QtCore.pyqtSignal(str)

    def __init__(self):
        super().__init__()
        self.error = False

    def emit_on_error(self):
    if self.error:
        self.error_signal.emit('There is an error')


# In the working thread
class FWComThread(QtCore.QThread):
    fwcom_error = QtCore.pyqtSignal()

    def __init__(self):
        super().__init__()
        self.debug_monitor = DebugMonitor()

    def run():
        # What the thread needs to do


# In the main thread
class MainWindow(QtWidgets.QMainWindow):
    def __init__(self):
        super().__init__()
        self.fwcom_thread = FWComThread()
        self.fwcom_thread.start()
        self.fwcom_thread.finished.connect(thread_finished)
        self.fwcom_thread.debug_monitor.error_signal.connect(self.set_monitor_err_msg)
        self.fwcom_thread.fwcom_error.connect(self.fwcom_error)

    def disconnect_signals(self):
        self.fwcom_thread.fwcom_error.disconnect()

    @QtCore.pyqtSlot
    def set_monitor_err_msg(self, err_msg: str):
        QtWidgets.QMessageBox.warning(self, 'Tag Monitor Error', err_msg)

    def fwcom_error(self):
        QtWidgets.QMessageBox.warning(self, 'FWCOM Error', 'FWCOM crashed')

    def thread_finished(self):
        # gets executed if thread finished
        pass

app = QtWidgets.QApplication(sys.argv)
window = MainWindow()
# Optionally set the size
window.resize(640, 480)
window.show()
app.exec_()
```

#### Change Widget Color
```python
    def make_widget_red(widget: QtWidgets):
        p = widget.palette()
        p.setColor(widget.backgroundRole(), QtGui.QColor('red'))
        widget.setPalette(p)
```


---------------------------------------
## PostgreSQL with psycopg2

```python
import psycopg2

conn = psycopg2.connect('dbname=mydb user=myuser')

cursor = conn.cursor()

# Open a cursor to perform database operations
cur = conn.cursor()

# Execute queries
cur.execute("DROP TABLE IF EXISTS todos;")
cur.execute("""
  CREATE TABLE todos (
    id serial PRIMARY KEY,
    description VARCHAR NOT NULL
  );
""")

# We can use variables in the query.
# Either variables + tuples
cur.execute('INSERT INTO todos (id, completed) VALUES (%s, %s);', (2, False))
# Or named variables + dict
cur.execute('INSERT INTO todos (id, completed) VALUES (%(id)s, %(completed)s);', {'id': 2, 'completed': False})

# Get data from the database
# Fetch methods pop values from the returned set of the last executed query,
# so if the table includes 3 rows, calling `fetchall` after `fetchone` would
# return only 2 values
cur.execute('SELECT * FROM todos;')
result = cur.fetchall()
result = cur.fetchone()
result = cur.fetchmany(3)

# Commit all changes to the PostgreSQL database permanently
conn.commit()

# Rollback uncommitted changes
conn.rollback()

# Close the connection and cursor
cur.close()
conn.close()
```

---------------------------------------
## Flask

### Flask for Web

```python
# app.py
from flask import Flask

# If you're using a single module, you should use __name__ for the app module
app = Flask(__name__)

@app.route('/')
def index():
    # Redirect to another endpoint
    redirect(url_for('index'))

    return 'Hello, World!'

# We may choose to handle only certain methods
@app.route('/create', methods=['POST'])
def create():
    return 'Created!'
```

```sh
# To enable live reload of the server on code changes
export FLASK_ENV=development
# FLASK_APP is assigned the filename
FLASK_APP=app.py flask run
```

Instead of using `flask run`, we can change the code to run with `python app.py`

```python
...
if __name__ == '__main__':
  app.run()
```

__Another way to structure the project__

We create an `__init__.py` file in our project folder and assign the folder name to `FLASK_APP`.

```python
# flask_app/__init__.py
from flask import Flask
def create_app(test_config=None):
    app = Flask(__name__)
    return app
```

We run the app so:

```sh
FLASK_APP=flask_app flask run
```

#### App Config
If we need to set up app configuration, we can simply do that one config at a time, pass multiple configurations from mapping or use a config file.

```python
# One config
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://myusername@localhost:5432/mydb'
# Multiple config
app.config.from_mapping(
    SECRET_KEY='dev',
    DATABASE=os.path.join(app.instance_path, 'flaskr.sqlite')
)
# From environment variables
app.config.from_envvar('YOURAPPLICATION_SETTINGS')
```

Using a config file

```python
app.config.from_pyfile('config.py', silent=True)

# config.py
import os
DEBUG = True
SECRET_KEY = os.environ.get("SECRET_KEY")
if not SECRET_KEY:
    raise ValueError("No SECRET_KEY set for Flask application")
```

Using a config object

```python
app.config.from_object('config.ProductionConfig')
# OR
from config import ProductionConfig
app.config.from_object(ProductionConfig)

# config.py
class Config(object):
    DEBUG = False
    DATABASE_URI = 'sqlite:///:memory:'

class ProductionConfig(Config):
    DATABASE_URI = 'mysql://user@localhost/foo'
```

#### Receiving input data
_Path parameters_

```python
@app.route('/users/<user_id>')
def index(user_id):
    return f'User ID is {user_id}'
```

_URL query parameters_

URL query parameters are listed as key-value pairs at the end of a URL, preceding a "?" question mark. E.g. `www.example.com/hello?my_key=my_value`.

```python
v = request.args.get(arg_name, <default?>)
```

_Form data_

Data from a form input control (text input, number input, password input, etc) is read by the name attribute on the input HTML element.

```python
v = request.form.get(field_name, <default?>)
# To get all items with the given key
v = request.form.getlist(field_name, <default?>)
```

_JSON_

Data type `application/json`. `request.data` retrieves JSON as a string and `json.loads` turns it into into lists and dictionaries.

```python
data_dictionary = json.loads(request.data)
# OR
data_dictionary = request.get_json()
```

#### Useful Flask Functions
__jsonify__

Create a JSON object. If we want our routes to return anything more complicated that a string, we need to jsonify it first.

```python
x = jsonify({ 'name': 'Jack' })
```

__abort__

Send an error code as a response.

```python
abort(status_code)
```

_______________________________________________________________________________
### HTML Templates with Jinja
Flask allows HTML templating using Jinja.

```html
<title>{{ title }}</title>
```

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html', title='User List')
```

__Variables__

```html
{{ foo.bar }}
{{ foo['bar'] }}
```

__for__

```html
<ul>
{% for user in users %}
  <li>{{ user.name }}</li>
{% endfor %}
</ul>
```

__if__

The if statement in Jinja is comparable with the Python if statement. In the simplest form, you can use it to test if a variable is defined, not empty and not false:

```html
{% if kenny.sick %}
    Kenny is sick.
{% elif kenny.dead %}
    You killed Kenny!  You bastard!!!
{% else %}
    Kenny looks okay --- so far
{% endif %}
```

_______________________________________________________________________________
### SQLAlcheemy (Database ORM)
We need to provide a database URI, which has the format:

```python
db_flavour://username[:password]@host_address:port/db_name
# Example:
postgresql://myusername@localhost:5432/mydb
```

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://myusername@localhost:5432/mydb'
db = SQLAlchemy(app)

# Creating a table
# This class is just to define the table model, so no need to define an __init__ method
class Person(db.Model):
    # By default, table name is the lower-cased class name. To change it:
    __tablename__ = 'persons'

    # db.Column takes (datatype, constraint, primary_key: bool, nullable: bool, default)
    # Setting a primary_key also enables auto-increment for it.
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(), nullable=False)
    price = db.Column(db.Float, db.CheckConstraint('price>0'))

    # It's a good practice to define this for debugging
    def __repr__():
        return f'<Person {self.id} {self.name} {self.price}'

# Create tables for defined models if they don't exist.
# IMPORTANT: Do not use if you are using migrations
db.create_all()
```

To easily make changes through the interactive terminal, assuming our script is called `app.py`:

```python
>>> form app import db, Todo
>>> todo = Todo(name='Buy milk')
```

#### SQLAlchemy Data Types
```
Integer         an integer
String(size)    a string with a maximum length (optional in some databases, e.g. PostgreSQL)
Text            some longer unicode text
DateTime        date and time expressed as Python datetime object.
Float           stores floating point values
Boolean         stores a boolean value
PickleType      stores a pickled Python object
LargeBinary     stores large arbitrary binary data
ARRAY(type)     an array of any of the other types
```

#### CRUD Operations

Create

```python
person = Person(name='Amy')
db.session.add(person)      # build a transaction for inserting in a record
db.session.commit()         # persist the record to the database. NOTE: commit can raise an exception. See below to handle this properly.

# Insert multiple
db.session.add_all([person1, person2])

```

Read (Query)

```python
# The query object of the model and be retrieved in two ways:
Person.query
session.query(Person)

# The query object generates SELECT statements
Person.query.all()                                  # SELECT * FROM person
Person.query.first()
query = Person.query.filter_by(name == 'Amy')       # SELECT * FROM person WHERE xxx
# Filter operators: https://docs.sqlalchemy.org/en/13/orm/tutorial.html#common-filter-operators
query = Person.query.filter(Person.name == 'Amy')
query.first()
query.all()

# Get by primary key
MyModel.query.get(id)

# Ordering
MyModel.order_by(MyModel.created_at)
MyModel.order_by(db.desc(MyModel.created_at))

# limit
query.limit(100).all()          # SQL: LIMIT

# Joined Queries
Person.query.join(<table_name>)

# Count
Person.query.count()
```

Update

```python
user = User.query.get(some_id)
user.name = 'Some new name'
db.session.commit()
```

Delete

```python
# Single delete
task = Task.query.get(task_id)
db.session.delete(task)
# Bulk delete
Task.query.filter_by(category='Archived').delete()
```

#### Useful Query Functions
```python
# Unique column combinations
Venue.query.distinct(Venue.city, Venue.state)
```

#### Handle commit exceptions
```python
try:
    db.session.add(x)
    db.session.commit()
except:
    error = True
    db.session.rollback()
    print(sys.exc_info())
finally:
    db.session.close()
if not error:
    print('Success!')
```

#### Relationships and Joins
- To be able to perform a Join, the child table needs to have a foreign key that points to a key in the parent table.
- The loading model can be:
    + Lazy - (Default) - Load needed joined data only as needed.
    + Eager - Load all needed joined data objects, all at once. Saves time on queries, but spends a lot of time upfront.
- Relationships are defined in the parent model using `dp.relationship`.
- `db.relationship` does not set up foreign key constraints for you. We need to add a column, e.g. `parent_id`, on the child model that has a foreign key constraint.
- A foreign key constraint prefers referential integrity from one table to another, by ensuring that the foreign key column always maps a primary key in the foreign table.

```python
class Parent(db.Model):
    __tablename__ = 'some_parent'
    id = db.Column(db.Integer, primary_key=True)
    # Defining the relationship:
    # Minimally:
    children = db.relationship('Child', backref='my_parent')
    # More control:
    children = db.relationship(
        # 'Child' is the name of the child class (model) passed as string.
        'Child',
        # backref is a custom property name of the parent object to assign to child objects
        # E.g.: `child1.my_parent` returns the parent object that child1 belongs to (the joined assets)
        backref='my_parent',
        # Lazy loading: `lazy=True` (default) or `lazy='select'`
        # Eager laoding: `lazy='joined'`
        lazy=True,
        # Type of the children collection. Can be `list`, `dict`, `set`
        collection_class=list,
        # What actions should happen to the children when the parent is updated.
        # Options are: 'save-update', 'all', 'delete-orphan'
        cascade='save-update')

class Child(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    # The foreign key name is '<parent-tablename>.<parent-primary-key-name>'
    parent_id = db.Column(db.Integer, db.ForeignKey('some_parent.id'), nullable=False)

parent1 = Parent()
child1 = Child()
child1.my_parent = parent1
# Thanks to the default cascade option, we only need to add parent and the children will be added as well
db.session.add(parent1)
db.session.commit()
```

### Many-to-Many Relationshiop
In case of one-to-one and one-to-many relationdships, it's enough to have one foreign key in the child table that refers to the parent table. However, in the case of many-to-many relationships, we need a third Association Table or Joining Table that includes foreign keys to the other tables.
> Table1 <-N-N-> Table2
> Table1 <-1-N-> Association-Table <-N-1-> Table2

For example, an order can have many products, and a product can appear in multiple orders. An association table called "order_items" can be created with each row containing an order id and a product id.

To set up a many-to-many in SQLALchemy, we:

- Define an association table using `Table` from SQLAlchemy
- Set the multiple foreign keys in the association table
- Map the association table to a parent model using the option `secondary` in `db.relationship`

If the association table includes no additional columns

```python
order_items = db.Table('order_items',
    db.Column('order_id', db.Integer, db.ForeignKey('order.id'), primary_key=True),
    db.Column('product_id', db.Integer, db.ForeignKey('product.id'), primary_key=True)
)
class Order(db.Model):
  id = db.Column(db.Integer, primary_key=True)
  status = db.Column(db.String(), nullable=False)
  products = db.relationship('Product', secondary=order_items,
      backref=db.backref('orders', lazy=True))

class Product(db.Model):
  id = db.Column(db.Integer, primary_key=True)
  name = db.Column(db.String(), nullable=False)

order = Order(status='ready')
product = Product(name='New Phone')
order.products = [product]
product.orders = [order]
# It's enough to add just one of the items
db.session.add(order)
db.session.commit()
```

If the association table includes additional columns

```python
class OrderItems(db.Model):
    __tablename__ = 'order_items'
    # Notice that there is no id field
    order_id = db.Column(db.Integer, ForeignKey('order.id'), primary_key=True)
    product_id = db.Column(db.Integer, ForeignKey('product.id'), primary_key=True)
    extra_data = db.Column(db.String(50))
    # To access the order entry of this item
    order = db.relationship("order")
    # To access the order status of this item
    order_status = db.relationship("order.status")

class Order(db.Model):
  id = db.Column(db.Integer, primary_key=True)
  status = db.Column(db.String(), nullable=False)
  products = db.relationship('order_items', backref="order")

class Product(db.Model):
  id = db.Column(db.Integer, primary_key=True)
  name = db.Column(db.String(), nullable=False)
  orders = db.relationship('order_items', backref="product")

# create parent, append a child via association
p = Product()
a = Association(extra_data="some data")
a.order = Order()
p.orders.append(a)

# iterate through child objects via association, including association
# attributes
for assoc in p.orders:
    print(assoc.extra_data)
    print(assoc.order)
```

#### SQLAlchemy Object Lifecycle
1. Transient: an object exists, it was defined, but not attached to a session (yet).

    `user = User(name='Amy')`

2. Pending: an object was attached to a session.
    - This happens after modifying the object `user.name="x"`, adding `session.add()` or deleting `session.delete()`.
    - "Undo" becomes available via `db.session.rollback()`.
    - Waits for a flush to happen.

3. Flushed: about ready to be committed to the database. Actions are translated into SQL command statements for the engine.
    - Flush happens when a query is called.
    - A flushed object would seem to include changes (e.g. new rows) we did in the transaction. However, those changes are local and haven't been pushed to the DB.
    - Calling `session.commit()` would bypass the flushed state and jump directly to committed.

4. Committed: `session.commit()` manually called for a change to persist to the database (permanently); session's transaction is cleared for a new set of changes.

#### Migration
_Migration libraries_

- Flask-Migrate (flask_migrate) is our migration manager for migrating SQLALchemy-based database changes. It uses a library called `Alembic` underneath the hood.
- Flask-Script (flask_script) lets us run migration scripts we defined, from the terminal

_Migration command line scripts_

- `migrate`: Detects the model changes to be made generating a migration file with upgrade and downgrade logic set up.
- `upgrade`: applying migrations that hadn't been applied yet ("upgrading" our database)
- `downgrade`: rolling back applied migrations that were problematic ("downgrading" our database)

_Steps to Set up Migrations_

0. Install `flask_migrate`.

```sh
pip3 install flask_migrate
```

1. Create a migration instance.

```python
from flask_migrate import Migrate
app = Flask(__name__)
db = SQLAlchemy(app)
migrate = Migrate(app, db)
### Define data models here ###
```

2. Create initial migration directory structure

```sh
flask db init
```

3. Create a new migration script. This will include our initial DB setup

```sh
flask db migrate
```

4. Verify the generated migration file.

5. Run the migration

```sh
flask db upgrade
```

_Steps to Perform Migrations_

1. Make changes to the SQLAlchemy models (e.g. create/remove columns).
2. Allow Flask-Migrate to auto-generate a migration script based on the changes by running `flask db migrate`.
3. Fine-tune the migration script. This might be needed, for example, if we have existing data and we need to set initial values for the new columns. `alembic` allows performing SQL queries on the database and other functions.

```python
def upgrade():
    # ...
    op.execute(sql_query)
```

4. Run the migration


_Migration script modification example_

When we want to add a new non-nullable column to a table with existing data, migration would fail. That's because all existing rows would have null for the new column, which doesn't match our requirements. To work around this, we modify the migration script to allow nullable fields at first, modify existing data to be not null, and then set nullable to False again:

```python
def upgrade():
    # Before:
    op.add_column('todos', sa.Column('completed', sa.Boolean(), nullable=False))
    # After
    op.add_column('todos', sa.Column('completed', sa.Boolean(), nullable=True))
    op.execute('UPDATE todos SET completed = False WHERE completed IS NULL;')
    op.alter_column('todos', 'completed', nullable=False)
```

---------------------------------------

## DynamoDB

__Setup__

The library will use the `default` aws credentionals of the system stored in `~/.aws`.

```python
import boto3
from botocore.exceptions import ClientError
from botocore.config import Config

# Optionally configure timeout
config = Config(connect_timeout=5, read_timeout=5)
dynamodb = boto3.resource('dynamodb', config=config)
my_table = dynamodb.Table('my-table-name')
```

### DynamoDB Operations

```python
def insert(profile) -> str:
    """`profile` is dict where the partition and sort keys exist"""
    try:
        profiles_table.put_item(Item=profile)
    except ClientError as err:
        return f"Could not insert item: {err.response['Error']['Code']}, {err.response['Error']['Message']}"
    except Exception as err:
        return f"Could not insert item: {err}"
    return ''

def exists(profile) -> bool:
    # ProjectionExpression: optional comma-separated list of attributes to retrieve. Cannot be empty
    response = profiles_table.get_item(
        Key={'memberID': 123}, ProjectionExpression='memberID')
    return 'Item' in response

```

__Important__

DynamoDB uses Decimal instead of Float, so when using json, we need to convert accordingly.

```python
class JSONEncoder(json.JSONEncoder):
    def default(self, obj):
        """This allows encoding Decimal type as float
        Does quasi the same things as json.loads/dumps from here: https://pypi.org/project/dynamodb-json/
        """
        if isinstance(obj, Decimal):
            return float(obj)
        return json.JSONEncoder.default(self, obj)

json.loads(data, parse_float=Decimal)
json.dump(data, f, cls=JSONEncoder)
```

---------------------------------------

## Web Requests
```python
import requests
headers = {
    "Accept-Language":  "en-US",
    "Accept-Encoding":  "gzip",
}
x = requests.get(url, headers=headers)

# Send as url encoded form
# Content-Type: application/x-www-form-urlencoded
data = {'param1': 'value1', 'param2': 'value2'}
r = requests.post(url, data=data, headers=headers)

# A raw url encoded form
payload ="scope=scope1&password=123&client_id=789&username=951&grant_type=password"
response = requests.post(url, data=payload, headers=header)

# Send as json
r = requests.post(url, json=json.dumps(data))
# OR: (this might work if the first method fails as it doesn't escape special characters)
headers = {'content-type': 'application/json'}
r = requests.post(url, data=json.dumps(data), headers=headers)

# Query
## example.org?address=xxx
params = {'address': 'xxx'}
r = requests.get(url=url, params=params)

# Path variables
## http://localhost:8080/test/api/v1/qc/:id
params = {'id': '123'}
requests.post(url="http://localhost:8080/test/api/v1/qc/{id}".format(**param)) 

# Cookies
## Getting cookies from a request
r = requests.get(url)
r.cookies['cookie_name']
## Using cookies in a request
r = requests.get("http://example.org", cookies={"my_cookie": "cookie_value"})

# Extracting data in json format
data = r.json()

# Perform requests in the same session
with requests.session() as s:
    s.post(login_url, data=login_data)
    r = requests.get(url)

# Send files
with f = open(path, 'rb'):
    files = {'photo': f}
    resp = requests.post(url, files=files)
```

### Saving an image from URL
```python
def DownloadImage(url):
    try:
        filename = url.split('/')[-1]
        r = requests.get(url, headers=headers, stream=True, timeout=5)
        if r.status_code == 200:
            with open(filename, 'wb') as f:
                r.raw.decode_content = True
                shutil.copyfileobj(r.raw, f)
    except Exception as e:
        print(e)
```

### Converting an image to bytes
```python
def get_image_from_url(url, maxsize=(1200, 850)) -> Tuple[Optional[bytes], Tuple[int, int]]:
    """Generate image data using PIL
    :returns the image as bytes and it size as a tuple
    """
    try:
        response = cached_session.get(url, stream=True, timeout=10)
    except:
        return None, (0, 0)
    response.raw.decode_content = True
    if not response.ok:
        return None, (0, 0)
    img = Image.open(response.raw)
    img.thumbnail(maxsize)
    size = img.size
    bio = BytesIO()
    img.save(bio, format="PNG")
    del img
    return bio.getvalue(), size
```

## Request Cache
`requests_cache` can either patch the std library requests making all requests go through it, or use its own session for requests.

__Patching requests__

```python
import requests_cache
requests_cache.install_cache('my_cache')
response = requests.get(url)

# Check if cache has a url
requests_cache.get_cache().has_url(url)
# If a URL has a part we ignore like a token, we might need to add it
requests_cache.get_cache().has_url(url+'?t=x')
```

__Cached Session__

```python
import requests_cache
# Create a cached session that can be used exactly like 'requests'
cached_session = requests_cache.CachedSession()
response = cached_session.get(url, stream=True, timeout=10)

# Check if response came from cache
response.from_cache

# Check if cache has a url
cached_session.cache.has_url(url)
# If a URL has a part we ignore like a token, we might need to add it
cached_session.cache.has_url(url+'?t=x')

# Save cached content to json files
src_session = CachedSession('my_cache', backend='redis')
dest_session = CachedSession('./cache_dump_dir', backend='filesystem', serializer='json')
dest_session.cache.update(src_session.cache)

# To ignore URL parameters, e.g. a token or something that doesn't affect the response
session = CachedSession(ignored_parameters=['token'])

# A custom matching key can be used
# See requests_cache.cache_keys.create_key() for the reference implementation
def create_cache_key(
    request: requests_cache.AnyRequest,
    ignored_parameters=None,
    **request_kwargs,
) -> str:
    request = requests_cache.normalize_request(request, ignored_parameters)
    # The url looks like https://x.y.com/...
    # The x part can change, so just match the part after it
    url = request.url.partition('.')[2]
    assert url
    key = hashlib.blake2b(digest_size=8)
    key.update(url.encode('utf-8'))
    return key.hexdigest()
cached_session = requests_cache.CachedSession(key_fn=create_cache_key, ignored_parameters=['t'])
```

## URL

### URL Validation
```python
>>> import validators
>>> validators.url("http://google.com")
True
```

### URL Parsing and Manipulation
```python
from urllib.parse import urlparse, urljoin, quote
url = "http://www.example.com/users/john-doe/detail"

# Parsing
parsed = urlparse(url)
parsed.hostname     # www.example.com
parsed.path

# Join
full_url = urljoin(url, 'index.html')

# Escaping invalid characters
url = quote(url)
```

_______________________________________________________________________________

## Kivy

### Kivy Basics
```python

```

### General
- Density independent pixels can be used to specify sizes and positions that look similar on screens of different sizes. A size of `40dp*40dp` is around the size of a fingertip.

```python
Button:
    size: "100dp", "80dp"
    pos: dp(100), dp(200)
```

#### Window Location
```python
from kivy.core.window import Window
Window.clearcolor = (1, 1, 1, 1)
Window.top, Window.left = (100, 100)
```

#### Kivy Colors
Colors are usually represented in RGBA format. A utility function can be used to use CSS-style colors.

```python
from kivy.utils import get_color_from_hex
Window.clearcolor = (1, 1, 1, 1)
Window.clearcolor = get_color_from_hex('#101216')
```

#### Kivy Text Formatting and Markup

Kivy uses BBCode for text markup. To use markup, the `markup` property needs to be set to true.

BBCode tag                         Effect on text
==========                         ==============
`[b]...[/b]`                       Bold
`[i]...[/i]`                       Italic
`[font=Lobster]...[/font]`         Change font
`[color=#FF0000]...[/color]`       Set color with CSS-like syntax
`[sub]...[/sub]`                   Subscript (text below the line)
`[sup]...[/sup]`                   Superscript (text above the line)
`[ref=name]...[/ref]`              Clickable zone, <a href="…"> in HTML
`[anchor=name]`                    Named location, <a name="…"> in HTML

```python
Label:
    text: '[b]00[/b]:00:00'
    markup: True
```

#### Universal properties
We could do the following to apply certain properties to all widgets of a certain kind:

```python
<TextInput>:
    pos_hint: {'center_x': 0.5, 'center_y': 0.5}
```

#### Arabic Support
```python
import arabic_reshaper
from bidi.algorithm import get_display
class CustomLabel(Label):
    txt = StringProperty()
    def on_txt(self, instance, value):
        try:
            self.text = get_display(arabic_reshaper.reshape(value))
        except Exception as e:
            self.text = value
```

#### Logging
Logging is enabled by default. To disable it, an environment variable needs to be set before importing Kivy.

```python
import os
os.environ["KIVY_NO_CONSOLELOG"] = "1"

import kivy
```

### Layouts
- AnchorLayout - Widgets can be anchored to the ‘top’, ‘bottom’, ‘left’, ‘right’ or ‘center’.
- BoxLayout - Widgets are arranged sequentially, in either a ‘vertical’ or a ‘horizontal’ orientation.
- FloatLayout - Widgets are essentially unrestricted.
- RelativeLayout - Child widgets are positioned relative to the layout.
- GridLayout - Widgets are arranged in a grid defined by the row and cols properties.
- PageLayout - Used to create simple multi-page layouts, in a way that allows easy flipping from one page to another using borders.
- ScatterLayout - Widgets are positioned similarly to a RelativeLayout, but they can be translated, rotated and scaled.
- StackLayout - Widgets are stacked in a lr-tb (left to right then top to bottom) or tb-lr order.

#### BoxLayout
- It ignores `size` and `pos` properties of widgets and arranges them sequentially.
- `size_hint` allows giving widgets a proportion of the default calculated size.
- `pos_hint` allows specifying the relative horizontal/vertical location of a widget in a vertical/horizontal layout respectively.

```python
<BoxLayoutTest>:
    orientation: "vertical"
    spacing: "10dp"         # Specify a space between children
    padding: '20dp'         # Padding around the children

    Button:
        # This has no effect. Size is calculated based on layout size
        size: "100dp", "100dp"

        # Size is a proportion of the default calculated size
        size_hint: 2, 0.8

        # Override calculated size
        size_hint: None, None
        size: "100dp", "100dp"

        # Override one dimension
        size_hint: None, 0.8
        width: "100dp"

        # x, center_x, right: position in a vertical layout relative to the layout width
        # x:        The position of the left edge of the widget
        # center_x: The position of the center of the widget
        # right:    The position of the right edge of the widget
        # y, center_y, top: position in a horizontal layout relative to the layout height
        pos_hint: {"x": 0.1}        # Place the widget's left edge at 10% of the layout width

<BorderedBox@BoxLayout>:
    border_width: 1
    padding: dp(8), 0
    canvas.before:
        Color:
            rgba: 0, 0, 0, 0.5
        Line:
            width: 1
            rectangle: self.x, self.y + 0.1*self.height, self.width, 0.8*self.height

<Separator@Widget>:
    size_hint_x: None
    width: dp(1)
    border_width: 1
    canvas:
        Color:
            rgb: 0, 0, 0
        Rectangle:
            pos: self.x + self.width - self.border_width, self.y
            size: self.border_width, self.height
```

#### AnchorLayout

```python
<AnchorLayoutTest>:
    # right, left, center (default)
    anchor_x: "right"
    # bottom, top, center (default)
    anchor_y: "bottom"

    Button:
        # Size is a fraction of the calculated size (see BoxLayout for more details)
        size_hint: 0.5, 0.8
```

#### GridLayout

```python
<GridLayoutTest>:
    # `rows` or `cols` need to be specified
    rows: 2

    Button:
        # size_hint can be used if applied to all widgets in the row/column 
        size_hint: 0.5, 0.8
```

#### StackLayout

```python
<StackLayoutTest>:
    # orientation is a combination of left-right and top-bottom, e.g. "rl-bt", "lr-tb", etc.
    orientation: "rl-tb"

    # padding is the internal margin of the layout itself
    padding: ("20dp")                           # Equal padding all sides
    padding: ("20dp", "40dp")                   # left/right=20, top/bottom=40
    padding: ("20dp", "40dp", "10dp", "5dp")    # custom (left, top, right, bottom)


    # <horizontal>, <vertical>
    spacing: "10dp", "20dp"
    spacing: "10dp"         # Equal spacing

    Button:
        # This will allows us to have 5 widgets per row
        size_hint: 0.2, 0.5
```
 
#### PageLayout

```python
# The simplest usecase is to list the widgets that will comprise the pages
<PageLayoutExample@PageLayout>:
    MainWidget:
    BoxLayoutExample:
    AnchorLayoutExample:
    GridLayoutExample:
```

#### ScrollView
Takes only one child. We need to specify the scroll direction by providing a size hint in the child and the height/width that the ScrollView needs to cover.

```python
<ScrollViewExample@ScrollView>:
    StackLayoutExample:
        size_hint: 1, None
        height: self.minimum_height
```

#### Label
```python
Label:
    text_size: self.size
    halign: 'right'
    valign: 'middle'
    # Match text size
    size_hint: None, None
    size: self.texture_size
```

#### Button
```python
# .kv
    Button:
        on_press: print("ouch! More gently please")
        on_release: print("ahhh")
# .py
def callback(instance):
    print(f'The button {instance.text} is being pressed')

btn1 = Button(text='Hello world 1')
btn1.bind(on_press=callback)
```

#### ToggleButton
```python
# .kv
    ToggleButton:
        on_state: root.on_toggle_state(self)

# .py
class ContainerWidget(BoxLayout):
    def on_toggle_state(self, widget):
        print(widget.state)     # "normal"/"down"
```

#### Switch
```python
# .kv
    Switch:
        on_active: root.on_switch_active(self)

# .py
class ContainerWidget(BoxLayout):
    def on_switch_active(self, widget):
        print(widget.active)     # Boolean
```

#### Slider
```python
# .kv
    Slider:
        min: 0                  # Default=0
        max: 100
        value: 50               # Default value
        orientation: "vertical"
        on_value: root.on_slider_value(self)

# .py
class ContainerWidget(BoxLayout):
    def on_slider_value(self, widget):
        print(widget.value)     # Float
```

#### ProgressBar
```python
# .kv
    ProgressBar:
         max: 100
        value: 50
```

#### TextInput
```python
# .kv
    TextInput:
        text: "hi"
        multiline: False
       # Called when pressing enter if 'multiline' is False
        on_text_validate: root.on_text_validate(self)
        # Enabled but cannot be edited
        readonly: True
        # Console theme
        background_color: (0, 0, 0, 1)
        foreground_color: (0, 1, 0, 1)
        font_size: sp(15)  # default
        # Center text vertically
        padding_y: [self.height / 2.0 - (self.line_height / 2.0) * len(self._lines), 0]

# .py
class ContainerWidget(BoxLayout):
    def on_text_validate(self, widget):
        print(widget.text)
```

#### Dropdown and Spinner
`DropDown` allows you to display a list of widgets that can contain any type of widget: simple buttons, images etc.
`Spinner` provides a quick way to select one value from a set.

```python
# .py
# Spinner
from kivy.uix.spinner import Spinner

def show_selected_value(spinner, text):
    print('The spinner', spinner, 'has text', text)

spinner = Spinner(
    # default value shown
    text='Home',
    # available values
    values=('Home', 'Work', 'Other', 'Custom'),
    # just for positioning in our example
    size_hint=(None, None),
    size=(100, 44),
    pos_hint={'center_x': .5, 'center_y': .5})
spinner.bind(text=show_selected_value)

###
# .kv
    DropDown:
        id: dropdown
        on_parent: self.dismiss()
        on_select: btn.text = '{}'.format(args[1])
        Button:
            text: 'First Item'
            size_hint_y: None
            height: '48dp'
            on_release: dropdown.select('First Item')
        Label:
            text: 'Second Item'
            size_hint_y: None
            height: '48dp'

    Spinner:
        size_hint: None, None
        size: '100dp', '44dp'
        text: 'Home'
        values: 'Home', 'Work', 'Other', 'Custom'
        text_autoupdate: True   # The text takes the first value
        on_text:
            print("The spinner {} has text {}".format(self, self.text))
```

__With KivyMD__

```python
from kivymd.uix.textfield import MDTextField
from kivymd.uix.menu import MDDropdownMenu
from kivy.properties import ListProperty
from kivy.metrics import dp
class MDDropDownText(MDTextField):
    items = ListProperty()

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.menu = MDDropdownMenu(
            caller=self,
            position="bottom",
            width_mult=4,
        )
        self.bind(focus=lambda x, y: self.menu.open() if self.focus else None)

    def on_text_validate(self):
        return super().on_text_validate()

    def on_items(self, instance_drop_down_item, items: str) -> NoReturn:
        if len(items) > 0:
            self.text = items[0]
        menu_items = [
            {
                "viewclass": "OneLineListItem",
                "text": s,
                "height": dp(56),
                "on_release": lambda x=s: self.set_item(x),
            } for s in items
        ]
        self.menu.items = menu_items

    def set_item(self, text_item):
        self.text = text_item
        self.menu.dismiss()

###
# .kv
    MDDropDownText:
        id: usecase
        items: '1.3', '3.5', '3.6'
        hint_text: "Usecase"
        pos_hint: {'center_x': .5, 'center_y': .5}
```

__DropDownButton__

This button shows a dropdown menu when pressed. Selecting an item triggers the `select_handler`. The handler and the item list are defined within the .kv file.

```python
from kivymd.uix.button import MDRaisedButton
class MainApp(App):
    def set_food(self, food: str):
        pass
class DropDownButton(MDRaisedButton):
    items = ListProperty()
    select_handler = ObjectProperty()

    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.menu = MDDropdownMenu(
            caller=self,
            position="top",
            width_mult=4,
        )
        self.bind(on_press=lambda x: self.menu.open())
        self.text_color_normal = App.get_running_app().theme_cls.primary_color

    def on_text_validate(self):
        return super().on_text_validate()

    def on_items(self, instance_drop_down_item, items: str):
        menu_items = [
            {
                "viewclass": "OneLineListItem",
                "text": s,
                "height": dp(56),
                "on_release": lambda x=s: self.set_item(x),
            } for s in items
        ]
        self.menu.items = menu_items

    def set_item(self, text_item):
        self.menu.dismiss()
        self.select_handler(text_item)

###
# .kv
    DropDownButton:
        text: 'Food'
        items: ['icecream', 'cake']
        select_handler: app.set_food
```

#### Image
```python
# .kv
    Image:
        source: "images/image.jpg"      # Image from local file
        allow_strech: True              # Stretch to fill the container (default: False)
        keep_ratio: False               # Keep aspect ration when streching (default: True)
        on_text_validate: root.on_text_validate(self)   # Called when pressing enter

# .py
class ContainerWidget(BoxLayout):
    def on_text_validate(self, widget):
        print(widget.text)
```

#### Popup
```python
popup = Popup(title='Test popup',
    content=Label(text='Hello world'),
    size_hint=(None, None), size=(400, 400))
popup.open()
# Disable dismissing by clicking outside the popup
popup.auto_dismiss=False
# Dismiss manually
popup.dismiss()

# From .kv
#:import Factory kivy.factory.Factory
<MyPopup@Popup>:
    auto_dismiss: False
    Button:
        text: 'Close me!'
        on_release: root.dismiss()
Button:
    text: 'Open popup'
    on_release: Factory.MyPopup().open()
```

### Canvas
A canvas is a property of all widgets and is made up of a number of instructions that draw a shape, change color, etc. It is placed on top of its parent.

- The canvas is always positioned at (0,0) except when it it's part of a relative layout.
- If we just need a canvas (i.e. no layout), we can create it inside a `Widget`.
- If not explicitly specified, the canvas takes a size of 100x100.
- The canvas is drawn _after_ the widget it's inside. To change that, we can use `canvas.before` instead of `canvas`.

```python
# .kv
#:set s dp(150)
    Widget:
        canvas:
            Color:                  # Change the color of all children that follows
                rgb: 1, 0, 0        # r, g, b
                rgba: 1, 0, 0, 0.4  # r, g, b, alpha (transparency)
            Rectangle:
                pos: self.center
                pos: self.center_x, self.center_y
                size: s, s
                source: 'images/pic.jpg'    # Fill with an image
            Ellipse:
                pos: 100, 100
                size: s, s/2
            Line:
                # A line can be drawn using points, circle, etc.
                points: (0, 0, 100, 100)        # (x0, y0, x1, y1, ...)
                circle: (200, 200, 100)         # center_x, center_y, radius
                ellipse: (200, 200, 100, 50)    # center_x, center_y, radius_x, radius_y
                width: 10                       # Line thickness

# .py
class MyCanvas(Widget):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        with self.canvas:
            Line(points=(100, 100, 400, 500), width=2)
            Color(0, 1, 0)
            # We can place an element in a variable to change it later
            self.rect = Rectangle(pos=(700, 200), size=(150, 100))

    def on_size(self, *args):
        """ Called when the canvas is created/resized"""

    def change_rect_pos(self):
        self.rect.pos = (100, 100)
```

### KV Audio
```python
# Load and store in a variable. This needs to be done only once
music = SoundLoader.load('audio/music.wav')
music.volume = 1    # 100%
music.play()
music.stop()
```

### Widgets in Python
App with one widget.

```python
from kivy.app import App
from kivy.uix.widget import Widget

class MyMainWidget(Widget):
    pass

class ProfilesApp(App):
    def build(self):
        return MyMainWidget()

if __name__ == '__main__':
    ProfilesApp().run()
```

__Add child-widgets in Python__

```python
class BoxLayoutExample(BoxLayout):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.orientation = "vertical"
        b1 = Button(text="A")
        self.add_widget(b1)
```

__Update widgets created in KV file__

```python
class MainApp(App):
    def change_stuff(self):
        self.root.ids.field.clear_widgets()
        self.root.ids.field.add_widget(Label(text='hello'))
        self.root.ids.field.remove_widget(button)
```

__Traversing the Tree__

```python
root = BoxLayout()
# ... add widgets to root ...
for child in root.children:
    print(child)
```

__Getting an App instance__

```python
class MainApp(App):
    pass

class MyWidget(Widget):
    @property
    def root(self):
        return App.get_running_app()
```

__Other__

```python
# Using sizes in dp
from kivy.metrics import dp
size = dp(100)
```

#### Handlers
- `__init__(self, **kwargs)`
    called when the widget is created.
- `on_parent(self, widget, parent)`
    called when the widget is attached to its parent.
- `on_start(self)`
    called after the application has started (after build() is called).
- `on_size(self, *args)`
    called when attached to a window and on size change.


##### Touch and Keyboard events
```python
from kivy.core.window import Window
class MainWidget(Widget):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.config_keyboard()

    def on_touch_down(self, touch):
        self.isTextInput = False

        def filter(widget):
            for child in widget.children:
                filter(child)
            # Accept touch event is the widget is a TextInput or can be pressed
            if widget.collide_point(*touch.pos):
                if isinstance(widget, TextInput):
                    self.isTextInput = True
                    widget.on_touch_down(touch)
                elif hasattr(widget, 'on_press'):
                    widget.on_touch_down(touch)

        filter(self)

        if not self.isTextInput and self._keyboard is None:
            self.config_keyboard()

    def config_keyboard(self):
        self._keyboard = Window.request_keyboard(self._keyboard_closed, self)
        self._keyboard.bind(on_key_down=self._on_keyboard_down)

    def _keyboard_closed(self):
        self._keyboard.unbind(on_key_down=self._on_keyboard_down)
        self._keyboard = None

    def _on_keyboard_down(self, keyboard, keycode, text, modifiers):
        if keycode[1] == 'w':
            ...
        return True # return True to accept the key. Otherwise, it will be used by the system.
```

To allow the parent to handle the events instead we call `super`. To ignore the event, we return `False`.

```python
def on_touch_up(self, touch):
    if should_handle:
        # Do stuff
    else if should_parent_handle:
        return super(ParentClassName, self).on_touch_up(touch)
    else:
        return False
```

#### Set Window Size

```python
    # Before the window is created. This needs to be placed before any Kivy import
    from kivy.config import Config
    Config.set('graphics', 'width', '200')
    Config.set('graphics', 'height', '200')

    # Dynamically after the Window was created:
    from kivy.core.window import Window
    Window.size = (300, 100)
```

#### KV Platform and OS
```python
from kivy import platform
def is_desktop():
    if platform in ('linux', 'win', 'macosx'):
        return True
    return False
```

### Scheduling

```python
from kivy.properties import Clock
# Repeated action
Clock.schedule_interval(handler_func, interval_sec)
Clock.schedule_interval(update, 0.5)

# Only once
Clock.schedule_once(handler_func, delay_sec)

def update(dt):
    """dt (delta-time) is the time in sec since last call"""
```

### KV File
The .kv file's name *must* be similar to the app class name. For example, if the .kv file name is `main.kv`, the App class name must be one of:
- `main`
- `Main`
- `MainApp`

```python
# (optional) Main interface (widget or layout created in .py file)
MyWidget:

# If we have the widget defined in python:
<MyWidget>:
    Button:
        text: "Hello"
        on_press: root.button_press()

# If the widget is not defined in python:
<MyWidget@Widget>:

# Variables
#: set w dp(100)
    Button:
        width: w
```

Corresponding Python file:

```python
class MyWidget(Widget):
    def button_press(self):
        ...
```

#### Root and Parent
`root` refers to the root of the current widget tree.
`parent` refers to the immediate parent of the current widget.

```py
<MyWidget>:
    BoxLayout:
        Label:
            # Refers to BoxLayout
            text: self.parent.size
            # Refers to MyWidget
            text: root.size
```

#### KV Properties
Properties are used to assign widget properties in .kv file from variables set in Python.

- StringProperty
- NumericProperty
- BoundedNumericProperty
- ObjectProperty
- DictProperty
- ListProperty
- OptionProperty
- AliasProperty
- BooleanProperty
- ReferenceListProperty


```python
# .kv
<MyWidget>:
    depth: self.width/2
    Label:
        text: root.label_text
        # To be able to refer to the label from python, we assign it an id
        # and assign that label to a new property that we create
        id: my_label
    my_label: my_label

# .py
from kivy.properties import StringProperty

class MyMainWidget(Widget):
    # IMPORTANT!! - Properties have to be declared here not inside init()
    label_text = StringProperty('Hi')
    depth = NumericProperty(0)
    my_label = ObjectProperty()
    def button_press(self):
        self.label_text = 'Clicked!'
        my_label.text = 'Clicked!'
```

__Handlers for custom properties change__

We can create handlers for custom properties that are called when the property value changes.

```python
class MyWidget(Widget):
    depth = NumericValue(0)

    def on_depth(self, widget, value):
        ...
```

__Using a property to store a callback__

```python
class DropDownButton(Button):
    select_handler = ObjectProperty()
    def func(self):
        self.select_handler()

## .kv
    DropDownButton:
        select_handler: app.set_filter_subset
```


#### Referencing Widgets Using ID
A widget can reference another widget using the `id` property.

```python
# .kv
    Slider:
        id: my_slider
    Label:
        text: my_slider.value
    TextInput:
        id: input
        on_text: app.process()
# .py
class MainApp(App):
    def process(self):
        text = self.root.ids.input.text
```

#### Multiple KV Files

```python
# menu.kv
<MenuWidget>:
    ...

# main.kv
#:import menu menu
<MainWidget>:
    MenuWidget:

# main.py
from kivy.lang import Builder
Builder.load_file('menu.kv')
```

### Custom Fonts
Font .ttf files can be placed inside a folder within the project directory, then the font can be directly used in `font_name` property.

```python
    Label:
        font_name: "fonts/myFont.ttf"
```

### App Settings and Config
Kivy supports persistent app config. Once used, it creates a file `app_name.ini` that stores the config and retrieves them on launch.
Configs are stored as key-value pairs in "sections".

```python
from kivy.config import Config
class TestApp(App):
    def build_config(self, config):
        config.setdefaults('user_info_section', {
            'name': 'value1',
            'age': '42'
        })
    
    # Get config
    Label(text='name is %s and age is %d' % (
            self.config.get('user_info_section', 'name'),
            self.config.getint('user_info_section', 'age'))
    )

    # Change the configuration and save it:
    Config.set('user_info_section', 'age', '50')
    Config.write()
```

#### Settings Screen
A settings screen can be automatically created to manage the different config. It can be accessed by pressing F1 or calling `App.open_settings()` and `App.close_settings()`.


```python
class TestApp(App):
    def build_settings(self, settings):
        jsondata = """
[
    { "type": "title",
      "title": "Login" },

    { "type": "options",
      "title": "My first key",
      "desc": "Description of my first key",
      "section": "section1",
      "key": "key1",
      "options": ["value1", "value2", "another value"] },

    { "type": "numeric",
      "title": "My second key",
      "desc": "Description of my second key",
      "section": "section1",
      "key": "key2" }
]
"""
        settings.add_json_panel('Test application1',
                                self.config, data=jsondata)
```

The `type` field is mandatory, and can take one of the following values:

    Type    Associated class
    ========================
    title   SettingTitle
    bool    SettingBoolean
    numeric SettingNumeric
    options SettingOptions
    string  SettingString
    path    SettingPath

You might want to know when a config value has been changed by the user in order to adapt or reload your UI. You can then overload the on_config_change() method:

```python
class TestApp(App):
    def on_config_change(self, config, section, key, value):
        if config is self.config:
            token = (section, key)
            if token == ('section1', 'key1'):
                print('Our key1 has been changed to', value)
            elif token == ('section1', 'key2'):
                print('Our key2 has been changed to', value)
```

The Kivy configuration panel is added by default to the settings instance. If you don't want this panel, you can declare your Application as follows:

```python
class TestApp(App):
    use_kivy_settings = False
```

### Clipboard in Kivy
```python
#:import Clipboard kivy.core.clipboard.Clipboard
Button:
    on_release:
        self.text = Clipboard.paste()
        Clipboard.copy('Data')
```
_______________________________________________________________________________

### Material Design with KivyMD
Install from pip:

    pip install kivymd

```python

from kivymd.app import MDApp
from kivymd.uix.textfield import MDTextField
from kivymd.uix.menu import MDDropdownMenu

class TaaSGUIApp(MDApp):
    pass
```

#### Toast
```python
from kivymd.toast import toast
toast('Test Kivy Toast')
```
_______________________________________________________________________________
### Useful Custom Widgets and Functions
```python
# Just some space
<Space@Widget>:
    size_hint_y: None
    height: dp(16)

<BorderedBox@BoxLayout>:
    border_width: 1
    padding: dp(8), 0
    canvas.before:
        Color:
            rgba: 0, 0, 0, 0.5
        Line:
            width: 1
            rectangle: self.x, self.y, self.width, self.height
            # rectangle: self.x, self.y + 0.1*self.height, self.width, 0.8*self.height

<CustomText@TextInput>:
    size_hint_y: None
    size: input_widget_size
    pos_hint: {'center_x': 0.5, 'center_y': 0.5}
    font_size: sp(16)
    padding_y: [self.height / 2.0 - (self.line_height / 2.0) * len(self._lines), 0]

# Separator line to the right of the widget
<Separator@Widget>:
    size_hint_x: None
    width: dp(1)
    border_width: 1
    canvas:
        Color:
            rgb: 0, 0, 0
        Rectangle:
            pos: self.x + self.width - self.border_width, self.y
            size: self.border_width, self.height

<MainLabel@Label+Separator>:
    pos_hint: {'center_x': 0.5, 'center_y': 0.5}
    size_hint_x: None
    width: max(self.texture_size[0], dp(130))
    bold: True

<SubLabel@Label>:
    pos_hint: {'center_x': 0.5, 'center_y': 0.5}
    size_hint_x: None
    size: self.texture_size

<RedBackground@Widget>:
    canvas.before:
        Color:
            rgba: 1, 0, 0, 1
        Rectangle:
            pos: self.pos
            size: self.size

class TaaSGUIApp(MDApp):
    def log(self, text, append=False):
        """Write something to the log box"""
        if append:
            text = f'{self.root.ids.log.text}\n{str(text)}'
        self.root.ids.log.text = str(text)
```
_______________________________________________________________________________
_______________________________________________________________________________
# Profiling

## cProfile
- Run the profiler:
    `python3 -m cProfile -o x.prof test.py`
- The profiling results will be stored in `x.prof`
- You can optionally use `snakeviz` package for visualizing the results in the browser.
- Run the visualizer:
    `snakevis x.prof`

__Note:__ Kivy programs need a workaround for this to work:
https://kivy.org/doc/stable/api-kivy.app.html#profiling-with-on-start-and-on-stop

## profilehooks
Can be used to profile a single function with results printed to stdout at program exit or immediately if using `immediate=True`.

```python
from profilehooks import profile

@profile(immediate=True)
def my_function(args, etc):
    pass
```

---------------------------------------
# Concurrancy

## Concurrent Futures
```py
import concurrent.futures
def do_stuff(): ...
items = []
with concurrent.futures.ThreadPoolExecutor() as executor:
    executor.map(do_stuff, items)
```

---------------------------------------
## Multithreading

### Using `threading` library
```python
  import threading

  def add(a, b):
    return a+b

  if __name__ == '__main__':
    threads = [] * 2
    for i, t in enumerate(threads):
        t = threading.Thread(target=add, args=(i, 1))
        t.start()
    for t in threads:
        t.join()
```

### Using `ThreadPool`
Similar to the interface of the `multiprocessing.Pool`

```python
  from multiprocessing.pool import ThreadPool
  pool = ThreadPool(processes=2)
  apply_results = [pool.apply_async(add, (x, 1)) for x in range(2)]
  results = [p.get() for p in apply_results]
```

---------------------------------------
## Multiprocessing

### `Process` class
```python
    import multiprocessing as mp
    # Define an output queue
    output = mp.Queue()
    # define work function
    def make_str(length, output):
        rand_str = ''.join(random.choice(string.ascii_lowercase) for i in range(length))
        output.put(rand_str)

    # Setup a list of processes that we want to run
    processes = [mp.Process(target=rand_string, args=(5, output)) for x in range(4)]

    # Run processes
    for p in processes:
        p.start()

    # Exit the completed processes
    for p in processes:
        p.join()

    # Get process results from the output queue
    results = [output.get() for p in processes]
    print(results)
```

### `Pool` class
```python
    import multiprocessing as mp
    def cube(x):
        return x**3
    def mult(x, y):
        return x*y

    pool = mp.Pool(processes=4)
    # Blocking functions (lock the main program until all process are finished)
    results_cube = pool.map(cube, range(1,7))
    results_pow = pool.map(lambda x: x**2, range(10))
    results_mult = pool.starmap(mult, [(x,2) for x in range(1,7)])
    results_mult = pool.starmap(mult, [(1,2), (2,2)])
    # Non-blocking
    apply_results = [pool.apply_async(cube, (x,)) for x in range(1,7)]
    results = [p.get() for p in apply_results]
    # OR
    map_results = pool.map_async(cube, range(1,7))
    starmap_results = pool.starmap_async(mult, [(1,2), (2,2)])
    results = map_results.get()
    # The returned value is a list of the returns
    print(results)
```

### `joblib.Parallel` class
```python
    from joblib import Parallel, delayed
    args = [(x, 2) for x in [0, 1]]
    results = Parallel(n_jobs=2)(map(delayed(mult), args))
```

### Async IO
```python
    import asyncio
    async def mult(x, y):
        await asyncio.sleep(0)
        return x*y

    ioloop = asyncio.get_event_loop()
    tasks = [ioloop.create_task(mult(x, 2)) for x in [0, 1]]
    ioloop.run_until_complete(asyncio.wait(tasks))
    ioloop.close()
```

### Issues
- The `multiprocessing` library uses `pickle` to serialize the functions that need to be passed to the processors, which does not always succeed.
- The alternative to `pickle` is `dill`, which is used as the default serialization method in `pathos` implementation of `multiprocessing`.

```python
import pathos.multiprocessing as mp
p = mp.Pool(4)
p.map(lambda x: x**2, range(10))
```

- After importing `numpy` or `scipy` the CPU affinity is set to 1, which limits the process to one core.

```python
# Check CPU affinity on Linux
import os
os.system('taskset -p %s' %os.getpid())
# Change CPU affinity on Linux
os.system('taskset -cp 0-%d %s' % (pool_size, os.getpid()))
```

---------------------------------------
# CSV

## CSV Reader

```
1/2/2014,5,8,red
no delimeter
```

```python
import csv
with open('example.csv') as csvfile:
    # Return a reader, which is a list of lists
    #[ ['1/2/2014', '5', '8', 'red'], ['no delimiter'] ]
    readCSV = csv.reader(csvfile, delimiter=',')
    for row in readCSV:
        ...
```

## CSV Writer
```python
    import csv
    csvfile = open('filename.csv', 'w', newline='')
    writer = csv.writer(csvfile, delimiter=';', quotechar='|', quoting=csv.QUOTE_MINIMAL)
    csvData = ['Band', 'Frequency', 'Baud Rate', "MER"]
    writer.writerow(csvData)
    csvfile.close()
    for child in root:
        # ...
```

---------------------------------------
# XML

## Example
```xml
  <my_data>
    <channel id="0">
      <l_band>
        <coeffs frequency="900" a="0" b="40" c="1838"/>
        <power frequency="900" value="-15"/>
        <power frequency="950" value="-15"/>
      </l_band>
      <if_band>
        <power frequency="30" value="-5"/>
      </if_band>
    </channel>
  </my_data>
```
```python
  import xml.etree.ElementTree as ET
  xml_file = 'D:/my_data.xml'
  tree = ET.parse(xml_file)
  root = tree.getroot()
  matched_child = None
  for child in root:
    if child.tag == "channel" and child.get('id') == 0:
      child.attrib      # => {'id': '0'}
```

## Functions
```python
  Element.iter('tag')       # Find all elements with a certain tag (children and subchildren)
  Element.findall('tag')    # Find all children with a certain tag
  Element.find('tag')       # Find the first child with a certain tag
  Element.text              # Accesses the element's text content
  Element.get()             # Accesses the element's attributes
```

---------------------------------------
# Web Scrapping with BeautifulSoup
We use `requests` to fetch web pages and `BeautifulSoup` to access the elements.

```python
from bs4 import BeautifulSoup
import requests

url = 'https://www.google.com'
req = requests.get(url)
soup = BeautifulSoup(req.content, features="html.parser")

# HTML contentes
print(soup.prettify())
# Getting the first 'div' tag
tag = soup.div
# For a tag with dashes
tag = soup.find('my-tag')
# Tag contents as a list
tag.contents
# Accessing an inner tag
tag.p
# Accessing an attribute
tag.p['class']
tag.p.get('class')

# Prettify the HTML
tag.prettify()
# Get the tag tree as HTML string
str(tag)
# Extract plain text (the shown text when visiting the page)
tag.get_text()

# Finding a tag using name and attributes
# soup.find(name, attrs, recursive, text)
tag = soup.find('div')  # Identical to soup.div
tag = soup.find(id='img', alt='x')
tag = soup.find(id='content_div')
tag = soup.find(attr={"class": "myclass"})
# Find all matching elements
tags = soup.find_all('a')
```

## Open website in browser
```python
import webbrowser
webbrowser.open_new_tab('http://net-informations.com')
# To open in the default broswer use:
webbrowser.get().open()
# Open a local file
webbrowser.get().open_new_tab(f'file://{os.path.realpath(filename)}')
```

If new is 0, the url is opened in the same browser window if possible. If new is 1, a new browser window is opened if possible. If new is 2, a new browser page ("tab") is opened if possible.

## Open an image from URL
```python
from PIL import Image, ImageTk
import requests
from io import BytesIO
url = "../image_url"
response = requests.get(url)
img = Image.open(BytesIO(response.content))
```

---------------------------------------
# JSON

## Encoding
```python
# To a file
with open("data_file.json", "w") as write_file:
    json.dump(data, write_file)
# To a variable
json_string = json.dumps(data)
# Prettify
json_string = json.dumps(data, indent=4)
```

## Decoding
```python
# From a file
with open("data_file.json", "r") as read_file:
    data = json.load(read_file)
# From a variable
data = json.loads(json_string)
```

### Decoding into an object
```python
class Address(object):
    def __init__(self, street, number):
        self.street = street
        self.number = number
js = '{"street":"Sesame","number":122}'
address = json.loads(js, object_hook=lambda d: Address(**d))

# In the case of nested object
class User(object):
    def __init__(self, name, address):
        self.name = name
        self.address = Address(**address)
js = '{"name":"Cristian", "address":{"street":"Sesame","number":122}}'
j = json.loads(js)
user = User(**j)
```

---------------------------------------
# Protobuf
To generate Python classes for our message:

```sh
# Generates your_proto_file_pb2.py
protoc --python_out=. your_proto_file.proto
```

```python
from google.protobuf import json_format

message = YourMessageClass()
message.ParseFromString(protobuf_message)

# Convert the parsed message to a JSON string
json_string = json_format.MessageToJson(message)

from protobuf_decoder.protobuf_decoder import Parser
parsed_data = Parser().parse(hex_string)
```

---------------------------------------
# Serial

```python
import serial
# Default baudrate is 9600
# timeout forces read functions to return if nothing is received within the timeout
ser = serial.Serial('/dev/ttyUSB3', 115200, timeout=5)

with serial.Serial('/dev/ttyUSB3') as ser:
    ser.write(b'AT+CPSI?\r')
    chars =  ser.read(2)
    line = ser.readline()
```

---------------------------------------
# Telegram

## Create a bot to send notifications

1) Go into settings (web or app) and set a username (if you don't have one already).
This is needed to obtain an id which your bot will use to send messages to

2) Send a message to RawDataBot to get your id
Just search for RawDataBot and send any message (hi will do). Take a note of your id.

3) Create your bot (which you'll command with HTTP requests)
Now search for BotFather and send the message `/start`. Help is displayed. Send the message `/newbot` and follow the instructions. Take a note of your token to access the HTTP API.

4) Send the API request using Python

__Method 1: Using requests__

API docs: https://core.telegram.org/bots/api

```python
token = 'xxx'
url = f'https://api.telegram.org/bot{token}'
params = {'chat_id': '123', 'text': msg}
r = requests.get(url + '/sendMessage', params=params)
```

__Method 2 - Using library__

Install libraries

```sh
python-telegram-bot==13.5
telegram-send==0.34
```

Create a file `telegram.conf` with the credentials.

```sh
[telegram]
token = xxx
chat_id = 123
```

```python
# Text
telegram_send.send(messages=[msg], conf='telegram.conf')
# Image
with open(image_file, "rb") as f:
    telegram_send.send(images=[f], conf='telegram.conf')
```

## Send messages from bot to private channel
First we need to find the channel ID:
1. Add the bot to the channel as admin
2. Go to getUpdates API URL in the browser and find the channel ID:

https://api.telegram.org/bot<BOT_TOKEN>/getUpdates

```json
...
 "my_chat_member":{
    "chat":{
       "id":-100987654321,
       "title":"My Channel",
       "type":"channel"
    },
```



---------------------------------------
# Code Snippets
## Using a dictionary of functions
```python
    def f1():
        ...
    def f2():
        ...
    inputs = {'w':f1, 's':f2}
    def keyDown(key)
        for i in inputs:
            if key == simplegui.KEY_MAP[i]:
                inputs[i]()
```

## Using a dictionary to ease updating values
```python
    inputs = {'w':[0,2], 's':[0,-2], 'up':[1,2], 'down':[1,-2]}
    vel = [0,0]
    def keyDown(key)
        for i in inputs:
            if key == simplegui.KEY_MAP[i]:
                vel[inputs[i][0]] += inputs[i][1]
```

## Google Drive API
```python
from __future__ import print_function

from apiclient import discovery
from httplib2 import Http
from oauth2client import file, client, tools

SCOPES = 'https://www.googleapis.com/auth/drive.readonly.metadata'
store = file.Storage('storage.json')
creds = store.get()
if not creds or creds.invalid:
    flow = client.flow_from_clientsecrets('client_id.json', SCOPES)
    creds = tools.run_flow(flow, store)
DRIVE = discovery.build('drive', 'v3', http=creds.authorize(Http()))

files = DRIVE.files().list().execute().get('files', [])
for f in files:
    print(f['name'], f['mimeType'])
```

## Run a Local Web Server
To run files from a local web server (at the current directory) as `localhost:8000/myfile.html`, run Python as:

```bash
python3 -m http.server 8000
```

## Web server with rquest logging
```python
#!/usr/bin/env python3
"""
Very simple HTTP server in python for logging requests
Usage::
    ./server.py [<port>]
"""
from http.server import BaseHTTPRequestHandler, HTTPServer
import logging

class S(BaseHTTPRequestHandler):
    def _set_response(self):
        self.send_response(200)
        self.send_header('Content-type', 'text/html')
        self.end_headers()

    def do_GET(self):
        logging.info("GET request,\nPath: %s\nHeaders:\n%s\n", str(self.path), str(self.headers))
        self._set_response()
        self.wfile.write("GET request for {}".format(self.path).encode('utf-8'))

    def do_POST(self):
        content_length = int(self.headers['Content-Length']) # <--- Gets the size of data
        post_data = self.rfile.read(content_length) # <--- Gets the data itself
        logging.info("POST request,\nPath: %s\nHeaders:\n%s\n\nBody:\n%s\n",
                str(self.path), str(self.headers), post_data.decode('utf-8'))
        self._set_response()
        self.wfile.write("POST request for {}".format(self.path).encode('utf-8'))

def run(server_class=HTTPServer, handler_class=S, port=8080):
    logging.basicConfig(level=logging.INFO)
    server_address = ('', port)
    httpd = server_class(server_address, handler_class)
    logging.info('Starting httpd...\n')
    try:
        httpd.serve_forever()
    except KeyboardInterrupt:
        pass
    httpd.server_close()
    logging.info('Stopping httpd...\n')

if __name__ == '__main__':
    from sys import argv
    if len(argv) == 2:
        run(port=int(argv[1]))
    else:
        run()
```
