# Python
<!-- TOC -->

- [Python](#python)
- [Miscellaniuous](#miscellaniuous)
    - [Recommended Code Structure](#recommended-code-structure)
    - [Cygwin Setup](#cygwin-setup)
    - [Multi-file projects](#multi-file-projects)
    - [Other](#other)
- [Python debugger (pdb)](#python-debugger-pdb)
- [Operators](#operators)
- [Functions](#functions)
    - [Lambda](#lambda)
- [Classes](#classes)
    - [Syntax](#syntax)
- [Flow Control](#flow-control)
    - [If-else](#if-else)
    - [Ternary Operator](#ternary-operator)
    - [For Loop](#for-loop)
- [Collections](#collections)
    - [Lists](#lists)
    - [Dictionaries](#dictionaries)
    - [Sets](#sets)
    - [Tuples](#tuples)
        - [Definition](#definition)
        - [Operations](#operations)
        - [NamedTuples](#namedtuples)
- [I/O and OS](#i-o-and-os)
    - [Printing](#printing)
    - [Input](#input)
    - [Pretty Print](#pretty-print)
    - [File manipulation](#file-manipulation)
        - [Opening files](#opening-files)
        - [Reading](#reading)
        - [File methods](#file-methods)
        - [File auto clean-up (auto close)](#file-auto-clean-up-auto-close)
    - [OS Operations](#os-operations)
    - [Issuing shell commands](#issuing-shell-commands)
- [Strings](#strings)
    - [Functions](#functions)
    - [Working with non-ascii strings](#working-with-non-ascii-strings)
- [RegEx](#regex)
    - [Groups](#groups)
    - [Examples:](#examples)
    - [Regex functions](#regex-functions)
        - [Flags](#flags)
- [Exception Handling](#exception-handling)
- [Simple GUI](#simple-gui)
- [Libraries](#libraries)
    - [Random](#random)
    - [Timeit](#timeit)
- [Unit Test (Nose)](#unit-test-nose)
- [Profiling](#profiling)
- [Multithreading](#multithreading)
    - [Using `threading` library](#using-threading-library)
    - [Using ThreadPool](#using-threadpool)
- [Multiprocessing](#multiprocessing)
    - [`Process` class](#process-class)
    - [`Pool` class](#pool-class)
    - [`joblib.Parallel` class](#joblibparallel-class)
    - [Async IO](#async-io)
    - [Issues](#issues)
- [CSV](#csv)
- [XML](#xml)
    - [Example](#example)
    - [Functions](#functions)
- [Code Snippits](#code-snippits)
    - [Using a dictionary of functions:](#using-a-dictionary-of-functions)
    - [Using a dictionary to ease updating values:](#using-a-dictionary-to-ease-updating-values)

<!-- /TOC -->

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
- Check if a class has an attribute:
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

---------------------------------------
# Python debugger (pdb)
- Break execution and run pdb:  
    `import pdb; pdb.set_trace()`
- Useful PDB commands:
    ```
    p var           print
    pp var          pretty print
    ! statement     Execute the (one-line) statement in the context of the current stack frame.
                    The '!' can be omitted unless the first word of the statement resembles a debugger command.
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
    ```

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
- If you need to modify a global variable you should declare it inside the function as global first. This is not needed for read access.
    ```python
    def func_name( [param1,param2,...] ):
        [global global_vars]
       "function_doc_string"
       [function_body]
       return [expression]
    ```
- This does not apply to mutation, e.g. in `a[1]=5`, `a` is consider global implicitly.

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

---------------------------------------
# Collections
## Lists
- They can contain objects of different data types.
- Creating a list:
    ```python
    list1 = [0] * size        #Initializing the list
    list1 = ["a", "b", 1, (1,2)];
    list2 = [n**2 for n in list1]
    list2 = [n for n in list1 if n>0]
    list1 = list(<iterable>)        # Convert an iterable (tuple, etc)into a list (deep copy).
    list1 = range([start=0,] stop[, step=1])])
    list1 = range(n)            # Same as range(0,n,1)
    ```
- Operations
  - Concatenation  
      `[1, 2, 3] + [4, 5, 6]   =>  [1, 2, 3, 4, 5, 6]`
  - Repetition  
      `['Hi!'] * 4         =>  ['Hi!', 'Hi!', 'Hi!', 'Hi!']`
- Accessing elements
  - `lst[0]` is the list first element and `lst[-1]` is the last element.
  - List slicing:  
      `l[1:5]` contains `l[1]` to `l[4]`, `l[1:]=l[1]->l[len(l)-1]`, `l[:5]=l[0]->l[4]`
  - Using `in`:  
      `if 2 in lst: # Do something`
- List functions
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
    lst.sort([args])        # Sort lst items in ascending order
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
- List iteration
    ```python
    for i in xrange(5, len(lst)-1):
    for i in xrange(len(lst)-1):
        lst[i]=...
    for item in lst: ...
    ```
    - _NOTE: You cannot modify a list while iterating on it. Instead, put the elements to modify in another list,  loop on `list(lst)` or use:_  
        `somelist[:] = [x for x in somelist if should_keep(x)]`

---------------------------------------
## Dictionaries
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
```

---------------------------------------
## Sets
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
```

---------------------------------------
## Tuples
- A `tuple` is a sequence of immutable Python objects.
- The differences between tuples and lists are:
  - Tuples cannot be changed unlike lists
  - Tuples use parentheses, whereas lists use square brackets.

### Definition
```python
# Parentheses are optional when defining a tuple
    tup0 = ();      # Empty tuple
    tup1 = ('physics', 'chemistry', 1997, 2000);
    tup2 = (1, 2, 3, 4, 5 );
    tup3 = "a", "b", "c", "d";
# Tuple declaration must include at least one comma, even if it contains a single value.
    tup1 = (50,);
```

### Operations
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

### NamedTuples
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
```

---------------------------------------
# I/O and OS
## Printing
```python
    # Python 2
    print expression1 [, expression2] [, ...]
    print "Number", x, "isn't too much"
    print "Line No %d - %s" % (index, line)
    # Python 3
    print(expression1[, expression2, ...])
    print("Number", x, "isn't too much")
    print("Line No {} - {}".format(index, line))
```

## Input
```python
    # reads one line and returns it
    str_in = input("Enter your input: ")
```    

## Pretty Print
```python
    import pprint
    class pprint.PrettyPrinter(indent=1, width=80, depth=None, stream=None, *, compact=False):
    PrettyPrinter.pprint(object)    # Print the formatted representation of object
    PrettyPrinter.pformat(object)   # Print the formatted representation of object
    # Example:
    pp = pprint.PrettyPrinter(indent=4)
    pp.pprint(stuff)
```

## File manipulation
### Opening files
```python
    f = open(file_name [, access_mode])
```

Access modes:
```
    'r'     read only, default mode
    'r+'    read/write
    'w'     write only (overwrite or create)
    'w+'    read/write (overwrite or create)
    'rw+'   read/write (don't overwrite, create if doesn't exist)
    'a+'    append/read (create if doesn't exist)
    '?b'    open the file in binary format (e.g. 'wb+')
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

### File methods
```python
    f.close()
    f.closed        # Check if file is closed
    f.mode          # Return access mode
    f.name
    f.write(string)
    f.writelines(sequence)
```

### File auto clean-up (auto close)
Objects which provide predefined clean-up actions can be used within with structure
```python
    with open("myfile.txt") as f:
        [file_operations]
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
```

## Issuing shell commands
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
# Strings
- A string can be used as an array with `s[0]` its first letter and `s[-1]` its last letter.
- String slicing:
    ```python
    s[1:5] = s[1] -> s[4]
    s[1:]  = s[1] -> s[len(s)-1]
    s[:5]  = s[0] -> s[4]
    ```
- Comparing strings: Simply done by testing equality (== or !=)

## Functions
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

## Working with non-ascii strings
Python 3 uses `utf-8` as the default source code encoding.

Python 2 uses `ASCII` by default, so unless you explicitly tell Python `# -*- coding: utf-8 -*-` at the top of your file, it doesn't know how to handle character values above 127.

---------------------------------------
# RegEx
```
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
    ab|cd       match ab or cd
    ^ $         beginning/end of string respectively
    \b          word boundary
    \1          back reference to group1 (example 1)
    (?:abc)     non-capturing group
    (?=abc)     positive lookahead. Matches a group after an expression without including it (example 2)
    (?!abc)     negative lookahead. Discards a match if the group comes after an expression (example 3)
```

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

## Examples:
    1- (\w)a\1      hah dad bad dab gag gab =>  hah dad gag
    2- \d(?=px)     1pt 2px 3em 4px     =>      2 4
    3- \d(?!px)     1pt 2px 3em 4px     =>      1 3
    4- colou?r      color colour
    5- <(.*)>       <h>Text</h>         =>      h>Text</h
    6- <(.*?)>      <h>Text</h>         =>      Text

## Regex functions
```python
re.match(pattern, string, flags=0)
    # Check for a match only at the beginning of the string
re.search(pattern, string, flags=0)
    # Check for a match anywhere in the string but stops at the first occurrence
re.split(pattern, string, maxsplit=0, flags=0)
    # Split string by the occurrences of `pattern`
    # >>> re.split('\W+', 'Words, words, words.')     =>      ['Words', 'words', 'words', '']
re.findall(pattern, string, flags=0)
    # Return all non-overlapping matches of `pattern` in a string as a list of strings.
    # If one or more groups are present in the pattern, return a list of groups.
re.split(pattern, string, maxsplit=0, flags=0)
    # Split `string` by the occurrences of `pattern`.
    # If groups are used in `pattern`, then the text of all groups in the pattern are also returned as part of the resulting list.
    # If `maxsplit` is nonzero, at most `maxsplit` splits occur, and the remainder of the string is returned as the final element of the list.
    # >>> re.split('[a-f]+', '0a3b9')         =>      ['0', '3', '9']
    # >>> re.split('([a-f])+', '0ab3bc9')     =>      ['0', 'a', '3', 'b', '9']
re.sub(pattern, repl, string, count=0, flags=0)
    # Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.
    # >>> re.sub(r'(\w+)\sAND\s(\w+)', '\2 & \1', 'Beans And Spam'    =>    'Spam & Beans'
matchObject.start()
    # Return the index of the match in the original string
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
    # Code that must always be excecuted
```

---------------------------------------
# Simple GUI
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

---------------------------------------
# Libraries
## Random
```python
    import random
    random.shuffle(list)                    # Shuffles the elements of a list or a string
    random.choice(list)                     # Return a random item from the list
    random.randrange(start=0, stop, step=1) # Return start <= n < stop
    random.randint(start, stop)             # Return start <= n <= stop
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

---------------------------------------
# Unit Test (Nose)
Every file starts with `test` is considered a test file. Every function starts with `test` is considered a test function.

A `setup`/`teardown` function can be called before/after running the test using `with_setup` decorator:

```python
@with_setup(setup, teardown)
def test_something():
    ...
```

---------------------------------------
# Profiling
- You can optionally use `snakeviz` package for visualizing the results in the browser.
- Run the profiler:  
    `python3 -m cProfile -o x.prof test.py`
- The profiling results will be stored in `x.prof`
- Run the visualizer:  
    `snakevis x.prof`

---------------------------------------
# Multithreading
## Using `threading` library
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

## Using ThreadPool
Similar to the interface of the `multiprocessing.Pool`

```python
  from multiprocessing.pool import ThreadPool
  pool = ThreadPool(processes=2)
  apply_results = [pool.apply_async(add, (x, 1)) for x in range(2)]
  results = [p.get() for p in apply_results]
```

---------------------------------------
# Multiprocessing
## `Process` class
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

## `Pool` class
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

## `joblib.Parallel` class
```python
    from joblib import Parallel, delayed
    args = [(x, 2) for x in [0, 1]]
    results = Parallel(n_jobs=2)(map(delayed(mult), args))
```

## Async IO
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

## Issues
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
# Code Snippits
## Using a dictionary of functions:
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

## Using a dictionary to ease updating values:
```python
    inputs = {'w':[0,2], 's':[0,-2], 'up':[1,2], 'down':[1,-2]}
    vel = [0,0]
    def keyDown(key)
        for i in inputs:
            if key == simplegui.KEY_MAP[i]:
                vel[inputs[i][0]] += inputs[i][1]
```
