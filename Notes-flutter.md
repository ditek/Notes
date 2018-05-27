# Contents
<!-- TOC -->

- [Contents](#contents)
- [Random](#random)
- [Tips and Tricks](#tips-and-tricks)
- [Dart](#dart)
  - [General](#general)
  - [Variables](#variables)
  - [Operators and num class functions](#operators-and-num-class-functions)
  - [Strings](#strings)
  - [Functions](#functions)
    - [Required Parameters](#required-parameters)
    - [Lambdas (anonymous functions)](#lambdas-anonymous-functions)
  - [Classes](#classes)
  - [Flow Control](#flow-control)
    - [ForEach](#foreach)
  - [Collections](#collections)
    - [Iterable](#iterable)
    - [List](#list)
    - [Queue](#queue)
    - [Set](#set)
    - [Map](#map)
- [Widgets](#widgets)
  - [StatelessWidget](#statelesswidget)
  - [StatefulWidget](#statefulwidget)
  - [Containers](#containers)
    - [Container](#container)
    - [Row and Column](#row-and-column)
    - [Center](#center)
    - [Align](#align)
    - [Expanded](#expanded)
    - [Flexible](#flexible)
  - [Material](#material)
  - [Text](#text)
  - [SizedBox](#sizedbox)
  - [Scaffold](#scaffold)
  - [ListTile](#listtile)
  - [ListView](#listview)
  - [GridView](#gridview)
  - [GestureDetector](#gesturedetector)
  - [Inkwell](#inkwell)
  - [Others Widgets](#others-widgets)
- [Navigation](#navigation)
- [Platform Specific Code](#platform-specific-code)
- [Test App](#test-app)

<!-- /TOC -->

# Random
- In Flutter, almost everything is a widget, including alignment, padding, and layout. The app itself is a widget, as it extends `StatelessWidget`, or example.
- Whenever you change the internal state of a [State] object, make the change in a function that you pass to [setState]:
    ```js
    setState(() { _myState = newValue });
    ```

# Tips and Tricks
- To remove `Test Mode` banner disable `debugShowCheckedModeBanner` in the `MaterialApp` widget.
- To surround a widget with `Center` or another widget, place the cursor over the widget and hit `Alt+Enter` 

# Dart
## General
- Everything in Dart is an object.

## Variables
Dart has two kinds of numbers, which are subclasses of the `num` class: `int` (arbitrary precision) and `double` (64bit)

```js
var x = 2;
int x = 2;
final x = 2;
final int x = 2;
x.runtimeType // Get type
```

## Operators and num class functions
```js
var x = 5 ~/ 2; // Truncating division. Returns the integer part
2.7.ceil(); // 2.0
2.7.floor(); // 3.0
2.7.round(); // 3.0
(-2).abs(); // 2
int.parse('1');
double.parse('1.1');
```

## Strings
```js
var x = 2;
print('The value is $x');
42.toString();
var longStr = 'A string can be'
              'spread over two lines'
var longStr = '''
Triple quotes can also be used
for longs strings.''';
var rawString = r'Raw strings \n are $left as is.'
```

For building strings, it is recommended to use `StringBuffer`:

```js
var msg = 'Hello';
var fullMsg = new StringBuffer(msg);
fullMsg.add('World');
return fullMsg.toString();
```

## Functions

```js
// Return type and parameter types are optional
addOne(value) {return value+1;}
int addOne(int value) {return value+1;}

// Optional positional parameters
int add(int val1, [int val2]){
  if (val2 == null) {}  // val2 is null if it's not provided
  if (?val2) {}         // Check if val2 is provided 
}

// Optional named parameters (named parameters have to be optional)
int add(int val1, {int val2}) {...}
var sum = add(1, val2: 2); // 3

// Optional parameters can have default values
int add(int val1, {int val2: 1}) {...}
int add(int val1, [int val2 = 1]) {...}

// Passing functions as parameters
foo(List items, Function filter) {...}
foo(List items, bool filter(int n)) {...} // Type annotations can be used
```

### Required Parameters
Named parameters are optional. To have a named parameter that's not optional we use `@required` annotation, which checks whether a named parameter is passed in.  
It doesn't check whether the object passed in is null though. We can check that using an assert statement.

```js
String name;
const Category({@required this.name}) : assert(name != null);
cat = Category(name: 'MyCat');
```

### Lambdas (anonymous functions)
```js
// Fat arrow notation 
sayHi() => 'hi';
var loud = (msg) => print(msg.toUpperCase());
loud('hi'); // HI
// Method 2
var func = () { print('I was tapped!'); }
```
 
## Classes

*Note: Use `this` only when there is a name conflict. Otherwise, Dart style omits the `this`.*

```js
class Point {
  num x, y;
  // There's a better way to do this down
  Point(num x, num y) {
    this.x = x;
    this.y = y;
  }
  // Setting x and y before the constructor body runs.
  Point(this.x, this.y);  // p = Point(1, 2)
  // @required is needed to use this format with named parameters
  Point({@required this.x, @required this.y});  // p = Point(x:1, y:2)
  
  // Named constructor
  Point.origin() {
    x = 0;
    y = 0;
  }
  // Initializer list:
  // Sets instance variables before the constructor body runs
  Point.initListConstructor(num a, num b)
      : x=a-b, y=a+b {
    print('Initialized with ($x, $y)');
  }
}
```

## Flow Control

```js
if (condition1) {} else if (condition2) {} else {}
x = y>0 ? 1 : 2;
y > 0 ? add(y) : add(x);
for (var i = 0; i < 5; i++) {}
for (var item in items) {}
while(condition) {}
do {} while(condition);
switch (command) {
  case 'CLOSED':
  case 'LOCKED':
    executeClosed();
    break;
  case 'OPEN':
    executeOpen();
    break;
  default:
    executeUnknown();
}
```

### ForEach

```js
[0, 1, 2, 3].where((n) => n.isEven).forEach((n) => print(n));
[0, 1, 2, 3].where((n) => n.isEven).forEach(print);

```

## Collections
### Iterable
Iterable is the base class of all Collections

```js
var numbers = new Iterable.generate(5, (i) => i);
for (var number in numbers)
  print(number);
numbers.length; // 5
numbers.contains(10); // false
// Filtering
numbers.where((i) => i.isOdd).toSet(); // 1, 3
checkOdd(n){ if (...) {return true;} else {return false;} }
numbers.where(checkOdd).toSet(); // 1, 3
numbers.map((i) => i * 2).toList(); // 0, 2, 4, 6, 8
```

### List
- Ordered
- Fast index retrieval
- Costly to change size

```js
var myList = []
// var myList = <MyClass>[];      // Optionally provide the type
var myList = new List();          // Unrecommended style
var myList = new List<MyClass>(); // Unrecommended style
var fruits = ['apples', 'oranges'];
fruits[0]; // apples
fruits.add('pears');
fruits.where((f) => f.startsWith('a')).toList();  // ['apples']
```

### Queue
- Ordered
- Efficient add/remove from head/tail
- No index access

```js
var orders = new Queue();
orders.addFirst('B23432');
var order = orders.removeFirst();
orders.addLast('Z94093');
orders.removeLast();
```

### Set
- Unordered
- No duplicates

```js
var fruits = new Set();
fruits.add('apples');
fruits.add('oranges');
fruits.add('apples');
fruits.length == 2;
var inBoth = fruits.intersection(otherFruits);
```

### Map
- Key/value pairs
- Keys are unique and cannot be null

```js
var map = {};
var map = <T, T>{};  // Optionally provide the types
var map = Map();                 // Unrecommended style
var map = Map<String, Fruit>();  // Unrecommended style
var fruits = {'apples': new Fruit(/* … */),
              'oranges': new Fruit(/* … */)};

var fruit = fruits['apples'];
fruits.containsKey('pears'); // false

fruits.putIfAbsent('banana', () => loadFromDatabase('myBanana'));
```

________________________________________________________________________________________________
# Widgets
- A widget's main job is to provide a `build()` method that describes how to display the widget in terms of other, lower level widgets.

## StatelessWidget
`StatelessWidget` is immutable and has no internal state to manage, meaning that its properties can't change and all values are final.

`Icon`, `IconButton`, and `Text` are examples of stateless widgets, which subclass `StatelessWidget`.

```js
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(...),
    );
  }
}
```

## StatefulWidget
- `StatefulWidget` has a state that can change during the lifetime of the widget. The user can interact with it (typing, moving a slider, etc.). 
- `Checkbox`, `Radio`, `Slider`, `InkWell`, `Form`, and `TextField` subclass `StatefulWidget`.

Implementing a stateful widget requires at least two classes:
1. a `StatefulWidget` class that creates an instance of
2. a `State` class, which contains the widget's state and the widget's `build()` method.

- The `StatefulWidget` class is, itself, immutable, but the `State` class persists over the lifetime of the widget.
- The `State` can access the widget variables as `widget.varName`. It has read-only access though.
- You can override `initState()` and `dispose()` to execute code when the state object is created/destroyed.

_Note: When the widget's state changes, the state object calls `setState()`, telling the framework to redraw the widget._

```js
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: new MyWords()
    );
  }
}

class MyWord extends StatefulWidget {
  final String word;
  MyWord({this.word});
  @override
  createState() => new MyWordState();
}

class _MyWordState extends State<MyWord> {
  @override
  void initState() {
    super.initState();
    ...
  }
  @override
  Widget build(BuildContext context){
    return FlatButton(
      onPressed: () {
        setState(() {color = _genRandomColor();});
      },
      color: _color,
      child: Text(widget.word);
    )
  }
}
```

## Containers
### Container
Adds padding, margins, borders, background color, or other decorations to a widget.

```js
new Container(
  color: Colors.puple,
  padding: new EdgeInsets.all(20.0),
  margin: new EdgeInsets.fromLTRB(0.0, 40.0, 0.0, 30.0),
  decoration: BoxDecoration(
    borderRadius: new BorderRadius.circular(50.0),
  ),
  height: 600.0,
  child: new Row(...)
)
```

### Row and Column

_Packing widgets_  
Children can be packed closely together by setting `mainAxisSize: MainAxisSize.min`

_Even Spacing_  
`mainAxisAlignment: MainAxisAlignment.spaceEvenly`

### Center
The `Center` widget aligns its widget subtree to the center of the screen.

### Align
Customize widget alignment

```js
Align(
  alignment: Alignment.bottomCenter,
  child: ...
);
```

### Expanded
Forces the child to expand to fill the available space along the main axis. Can be used to split the space equally among elements.

```js
// pic2 is twice as wide as pic1
new Row(children: [
  new Expanded(child: new Image.asset('images/pic1.jpg')),
  new Expanded(flex: 2, child: new Image.asset('images/pic2.jpg'))])
```

### Flexible
Gives a child the flexibility to expand to fill the available space in the main axis, but, unlike `Expanded`, `Flexible` does not require the child to fill the available space.

## Material
Creates a piece of material. Make sure that the context implements material before using it.

```js
Widget build(BuildContext context) {
  debugCheckHasMaterial(context);
  return Material(...);
}
```

## Text
TextStyle

```js
final _biggerFont = const TextStyle(fontSize: 18.0);
final _newTheme = Theme.of(context).textTheme.display1;
return new Text('Hello World', style: _biggerFo nt,)
```

## SizedBox
Placing a `Text` in a `SizedBox` and setting its width prevents a discernible “jump” when the text changes between values of different widths.

```js
new SizedBox(
  width: 18.0,
  child: new Container(
    child: new Text('$count'),
  ),
```

## Scaffold
Provides a default app bar, title, and a body property that holds the widget tree for the home screen.

```js
home: new Scaffold(
    appBar: new AppBar(
        title: new Text('Welcome to Flutter'),
        elevation: 4.0,  // Elevation in Z axis
        centerTitle: true,
    ),
    body: new Center(
        child: new Text('Hello World'),
    ),
    actions: <Widget>[...],  // Widgets to display after the `title` (commonly `IconButton`s)
)
```

## ListTile
Organizes up to 3 lines of text, and optional leading and training icons, into a row.

## ListView
Made up of `ListTile`s. Can be constructed using the `builder` method (suitable for large lists where only visible items are built), or directly from a `ListTile` list.

```js
// Build a list form the contents of an existing list
myList = new ListView.builder(
  itemBuilder: (context, i) {
    if (i.isOdd) return new Divider();
    final index = i / 2;  // Use ~/ to get integer division
    if (index >= listData.length) {
      listData.addAll(generateWordPairs().take(10));
    }
    return new ListTile(title: new Text(listData[i]);
  },
  itemCount: 100,      // Specify itemCount if the list isn't infinite
  padding: const EdgeInsets.all(16.0)
);

// Build children list on the fly
myList = ListView(
  // Generate 100 Widgets that display their index in the List
  children: new List.generate(100, (index) {
    return Text('Item $index');
  }),
);

// Create widgets list from data list
List<String> names;
final listWidgets = names.map((String name) {
  return Text(name);
}).toList();
myList = ListView(children: listWidgets);

// Use a list of `ListTile`s
myList = new ListView(children: myTiles)

/* Useful functions */
// Add dividers to between the `ListTile`s
final dividedList = ListTile.divideTiles(tiles: tilesList, context: context).toList();
```

## GridView
GridView has multiple constructors:

`GirdView.builder`: For having a large/infinite number of tiles

```js
final Orientation orientation = MediaQuery.of(context).orientation;
final bool isLandscape = orientation == Orientation.landscape;
myGrid = new GridView.builder(
  itemCount: data.length,
  gridDelegate: new SliverGridDelegateWithFixedCrossAxisCount(
      crossAxisCount: isLandscape ? 3 : 2),
  itemBuilder: (BuildContext context, int index) {
    return new GridTile(
      footer: new Text(data[index]),
      child: new Text(data[index]),
    );
  },
);
```

`GridView.count`: A grid with a fixed number of tiles in the cross axis.

```js
myGrid = new GridView.count(
  // Create a grid with 2 columns. If you change the scrollDirection to 
  // horizontal, this would produce 2 rows.
  crossAxisCount: 2,
  // Generate 100 Widgets that display their index in the List
  children: new List.generate(100, (index) {
    return new Center(
      child: new Text('Item $index'),
    );
  }),
);
```

## GestureDetector
Detects gestures

## Inkwell
- Provides tap animation. One of the ancestors of `Inkwell` must be a `Material` widget.
- The `InkWell` will not animate if the onTap function is null.

## Others Widgets

`Icon`

```js
Icon( Icons.favorite, color: Colors.red)
```

`IconButton`  
In addition to an `Icon` property, has an `onPressed` property that defines the callback method for handling a tap

`GridView`  
Lays widgets out as a scrollable grid.

`Stack`  
Overlaps a widget on top of another (similar to `FrameLayout`)

`Card`  
Organizes related info into a box with rounded corners and a drop shadow.
________________________________________________________________________________________________
# Navigation
To navigate form one screen from another we use the `Navigator` class.

_Navigate to the second screen using `Navigator.push`_  
The `push` method requires a `Route`. We can create our own, or use the `MaterialPageRoute`, which transitions to the new screen using a platform-specific animation.

_Return to the first screen using `Navigator.pop`_  
The `pop` method will remove the current `Route` from the stack of routes managed by the navigator.

```js
// Within the `FirstScreen` Widget
onPressed: () {
  Navigator.push(
    context,
    new MaterialPageRoute(builder: (context) => new SecondScreen()),
  );
}
// Within the SecondScreen Widget
onPressed: () {
  Navigator.pop(context);
}
```

________________________________________________________________________________________________
# Platform Specific Code

________________________________________________________________________________________________
# Test App

```js
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Movie Explorer',
      theme: new ThemeData(primarySwatch: Colors.blue),
      home: new HomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class HomePage extends StatefulWidget {
  HomePage({Key key, this.title}) : super(key: key);
  final String title;

  @override
  createState() => new HomePageState();
}

class HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
      body: buildThumbnailGrid(),
    );
  }

  final List<String> data = ['text1', 'text2'];

  GridView buildThumbnailGrid() {
    final Orientation orientation = MediaQuery.of(context).orientation;
    final bool isLandscape = orientation == Orientation.landscape;
    return new GridView.builder(
      itemCount: data.length,
      gridDelegate: new SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: isLandscape ? 3 : 2),
      itemBuilder: (BuildContext context, int index) {
        return new GridTile(
          footer: new Text(data[index]),
          child: new Text(data[index]),
        );
      },
    );
  }
}
```