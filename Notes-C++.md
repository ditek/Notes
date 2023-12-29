# Language Fundamentals

## Includes
- .h after the library name is optional
- Most C libraries are available by adding 'c' before the C++ library name, e.g. cstdlib, ctime ...

## Functions
- inline keyword is used instead of macros to get functions with low runtime overhead.
- Class member functions are automatically inline.
- Default parameters are supported: f(int x, int y=0){...}

## Casting
- C style casting, i.e. `(type)` is deprecated. 
- Available casting types:

```cpp
  static_cast<type>       // Safe cast
  dynamic_cast<type>      // Change type through the class hierarchy.
  reinterpret_cast<type>  // Force cast. Highly unsafe.
  const_cast<type>        // Cast away constness
```

## Memory management

```cpp
// Allocation
	char *s = new char[size];	// Allocate an array in heap
	int *p = new int(9);	//	Allocate and initialize a single int
// Deallocation
	delete []s;
	delete p;
```

## Miscellaneous
C++11 introduced nullptr keyword to represent the null pointer. I.e.:

```cpp
    int *ptr = nullptr;   <=>   int *ptr = 0;
```

---------------------------------------

# Classes
If access specifier is not declared explicitly, then by default access specifier will be private.

```cpp
class Rectangle {
    int width, height;
  public:
    Rectangle(int, int);
};

class Circle {
    double radius;
  public:
    Circle(double r) : radius(r) { }
};

// Class constructor can be called in two ways:
Rectangle x(1,2);
Rectangle x = {1,2};
```

## Constructor

- `explicit` is used when declaring a constructor that takes 1 param to avoid implicit type conversion (C++11)

```cpp
  class classA{ explicit classA (int i) {...} };
  main(){classA a = 5;}   // This implicit conversion is not allowed now
```

- When you want to call the default constructor, don't put any parentheses. Putting them would mean a declaring a function that returns Rectanble type.

```cpp
  Rectangle rectb;   // ok, default constructor called
  Rectangle rectc(); // ops, default constructor NOT called 
```

- Constructor member initialization:

```cpp
  Rectangle::Rectangle (int x, int y) : width(x), height(y) { }
```

- If a parameter has a class type, it must be initialized this way if something other than the default constructor is needed:

```cpp
  Cylinder::Cylinder (double r, double h) : base{r}, height{h} { }     // base is of type Circle
```

## Destructor
- Called automatically when the object gets out of scope.
- There can only be one destructor with void signature.
- It usually has delete statements to clean up dynamically allocated memory.

```cpp
// Syntax
  ~classname(){}
```

- The default destructor is declared as `virtual` in base classes to force looking for a child destructor when destroying an object.

```cpp
  virtual ~ClassTemplate() = default;  
```

## Methods and member functions
- Constant member functions: A constant function is a "read-only" function that does not modify the object for which it is called. It cannot modify any non-static data members or call any member functions that aren't constant.
- If a function is defined within the class body it will be automatically considered an inline member function by the compiler.

- `const` after a class member function causes the `this` pointer passed to it to become const.
  - That means the function cannot change any class members except ones that are marked mutable.
  - The `const` keyword is part of the functions signature which means it can be used for overloading.

```cpp
    class MyClass {
      private:
        mutable int counter;
      public:
        void Foo(){ counter++; }
        void Foo() const { counter+=2;  }
    };
    int main(void) {
      MyClass cc;
      const MyClass& ccc = cc;
      cc.Foo();
      ccc.Foo();
    }
```

## Const Members
If the class has a private const member, the only way it can be initialized is in the constructor initialization list:

```cpp
    private: const int x;
    public: classA(int x):x(x){}
```

## Static Members
Static class members MUST be initialized or they will not be in scope, and this cannot be done in .h file. Syntax:

```cpp
  type class_name::static_variable = value
```

## Type conversion
- A conversion between a user type and a native type can be defined.
- Type-cast operator:

```cpp
  class B {public: operator A() {return A();}};
  :
  A foo;  B bar;
  foo = bar;

// Example: Converting a user defined 'point' to a double:
  point::operator double(){return x+y;}
```

## Friend functions
- Functions that can access private members but do not need the . notation.
- Used usually with operator overloading.

```cpp
	class point{ friend ostream& operator<<(ostream &out, const point &p){...}}
	main(){ point p; cout<<p; }
```

## Operator overloading
- Can be done using a member function or a friend function.
- Using a friend function is preferred to have a symmetric case where implicit conversion from other types is available.

```cpp
	point operator+(point p){return point(x+p.x, y+p.y);}
	friend point operator-(point p1, point p2){return point(p1.x-p2.x, p1.y-p2.y);}
	main(){	point a,b,c;
					a = b+c;		// b.operator+(c)
					a = b-c;	}	// operator-(b,c)
```

## Other
- Object array:

```cpp
  Rectangle* baz = new Rectangle[2] { {2,5}, {3,6} };
  delete[] baz;
```


---------------------------------------
# Data Types

## Strings

### String streams

```cpp
  #include <iostream>
  #include <sstream>
  ostringstream outs;
  outs << sqrt(2.0);
  s = outs.str();    
```

## Enums

- Default enum type is an integral type and specifically determined by the compiler.

```cpp
// unscoped enum:
	enum [identifier] [: type] {enum-list}; 
	enum Suit { Diamonds, Hearts, Clubs, Spades };
	enum Suit:int { Diamonds, Hearts, Clubs, Spades };

// scoped enum (C++11):
	enum [class|struct] [identifier] [: type] {enum-list};
	enum class Suit { Diamonds, Hearts, Clubs, Spades };

// A cast is required to convert an int to a scoped or unscoped enum.
// However, you can promote an unscoped enum to an integer value without a cast.
	enum class Suit { Diamonds, Hearts, Clubs, Spades };
	Suit hand; 
	hand = Suit::Clubs; //Correct.
	int x = 10;
	hand = x;                            // error: cannot convert from 'int' to 'Suit'
	hand = static_cast<Suit>(x);         // OK, but probably a bug!!!
	x = Suit::Hearts;                    // error: cannot convert from 'Suit' to 'int'
	x = static_cast<int>(Suit::Hearts);  // OK
```

---------------------------------------
## Struct
If access specifier is not declared explicitly, then by default access specifier will be public. 

```cpp
  struct MyStruct{...};
  void func(MyStruct *mystruct) {...}
  void main(){
    MyStruct s;
    func(&s);
    // in C++ you can directly pass the argument and the method will take it by reference
    func(s);
  }
```

- Passing to a function (by ref)

```cpp
  struct MyStruct{...};
  void func(MyStruct *mystruct) {...}
  void main(){
    MyStruct s;
    func(&s);
    // in C++ you can directly pass the argument and the method will take it by reference
    func(s);
  }
```

---------------------------------------  
---------------------------------------
## Containers

- map and set store unique ordered data with O(log N) access time.
- Iterating over a container:

```cpp
	vector<int> v;
	for (auto iter = v.begin(); iter != v.end(); ++iter)
	for (std::vector<int>::size_type i = 0; i != v.size(); i++)
	for (auto elem : v) // COPIES elements, not much better than the previous examples
	for (auto& elem : v) // observes and/or modifies elements IN-PLACE
	for (const auto& elem : v) // observes elements IN-PLACE
```

---------------------------------------
### std::vector
- Vectors are sequence containers representing arrays that can change in size.
- Random access cost is O(1).
- Push-back operation costs O(1).
- Insertion and deletion costs O(N).

```cpp
// Declaration:
	vector<T> v1;					// an empty vector
	vector<T> v2(10);			// a vector with 10 elements each initialized to the default type value
	vector<T> v2(10, 5);	// a vector with 10 elements each initialized to 5
	vector<T> v3(v2);			// a vector that is a copy of v2

// Accessing elements:
	// - Unsafe way - like an array. Overrun causes undefined behaviour
  v1[3]=2;

	// - Safe way - using at() member function. Overrun throws an exception
  v1.at(i)=2;

// Methods
  v1.push_back(value);

// Convert vector<string> into char**
  // The function must not modify the array, otherwise, a new char** is required
  void func(char** carray, size_t size){..}
  void main(){
    vector<string> strings;
    vector<char*> cstrings;
    for(size_t i = 0; i < strings.size(); ++i)
        cstrings.push_back(const_cast<char*>(strings[i].c_str()));
    func(&cstrings[0], cstrings.size());
  }
```

---------------------------------------  
### std::list
- Lists are sequence containers that allow constant time insert and erase operations anywhere within the sequence, and iteration in both directions.
- Random access cost is O(N), i.e. it lacks direct access to elements by their location.
- Insertion and deletion costs O(1).

```cpp
// Iterator
  list<type>::iterator iterator_name;
// Member functions
  begin();     // return an iterator to the first value
  end();       // return an iterator to the first value
  push_front(value);    // insert value at the beginning
  push_back(value);     // insert value at the end
  pop_front();   // return and remove the first value
  pop_back();   // return and remove the last value
  insert(it_ position, value);         // insert value before iterator position
  insert(it_ position, n, value);      // insert value n times
  insert(it_ position, it_ first, it_ last);  // insert values from another container
  size();     // don't use it to check for emptyness
  empty();
  sort();
  reverse();
  unique();   // turn a string of similar elements to one element [1,1,2,1]=>[1,2,1]
```

---------------------------------------
### std::map
- An ordered container that stores elements formed by a combination of a key value and a mapped value

```cpp
// Syntax:
  // comparison_function is not necessary when key_type defines a '<' operation, i.e. other than int, char, string, etc.
  std::map <key_type, data_type, [comparison_function]> my_map;

// Adding elements:
  // Using a key with no associated element creates a new element
  my_map[10] = 'A'

// Iterating over a map:
  // C++98:
    typedef std::map <int, char> my_map_t;
    my_map_t my_map;
    my_map_t::iterator it;
    for(it = my_map.begin(); it != my_map.end(); it++)
      // it->first = key
      // it->second = value
  // C++11:
    std::map <int, char> my_map;
    for(auto it = my_map.begin(); it != my_map.end(); it++)
      // it->first = key
      // it->second = value
  // C++11 (nicer version):  
    std::map <int, char> my_map;
    for(auto &element : my_map)		// See 'Containers' section above
      // element.first = key
      // element.second = value

// Check if an element exists
  count(key)      // will return 1 if it exists, 0 otherwise

// Member functions
  int erase(key);   // return number of erased elements (max 1 for map)
  int size();
  bool empty();
  clear();
  find(key);    // returns an iterator pointing to the element associated with the key or map.end() if no such key is found
                // e.g.: if(my_map.find('x') != my_map.end()) {...}
  count(key);     // return 1 if key exists and 0 if not
  lower_bound(key);    // return an iterator to the first element equal or less than 'key'
  upper_bound(key);    // return an iterator to the first element larger than 'key'
  pair<iterator,iterator> equal_range(key);  // return a pair whose first is lower-bound and second is upper-bound
  
/*
    +- lb(2) == ub(2)       +- lb(6)        +- lb(8)
    |        == begin()     |  == ub(6)     |   +- ub(8) == end()
    V                       V               V   V
    +---+---+---+---+---+---+---+---+---+---+---+
    | 3 | 4 | 4 | 4 | 4 | 5 | 7 | 7 | 7 | 7 | 8 |
    +---+---+---+---+---+---+---+---+---+---+---+
        ^               ^                       ^
        |               |                       |
        +- lb(4)        +- ub(4)                +- lb(9) == ub(9) == end()
    
        |- eq-range(4) -|
*/

// Remove element from a map while iterating
    for (auto it = m.cbegin(); it != m.cend() /* not hoisted */; /* no increment */)
    {
      if (delete_condition)
        m.erase(it++);
      else
        ++it;
    }
```

---------------------------------------  
### std::pair

```cpp
// Syntax
  std::pair<int,float> p=std::make_pair(1,2.3); 
  p.first = 2;
  p.second = 4;
```

---------------------------------------
---------------------------------------  
# Input files

```cpp
#include<iterator>
#include<fstream>
main(){
	ifstream file("file_name.txt");
	istream_iterator<string> start(file), end;

}
```

# Namespaces

- Namespace alias

```cpp
    namespace fs = boost::filesystem;
    fs::path myPath(strPath, fs::native);
```

---------------------------------------
---------------------------------------  
# Design Patterns

## Singleton
<http://c2.com/cgi/wiki?CppSingleton>

- It is a design pattern to ensure there is only one instance of a given class.
- It depends on having a public function that returns a private static instance or create on.

```cpp
  /// Singleton using a static local
  // Not suitable for multithreaded applications
  class S
  {
    public:
      static S& Instance(){
        static S    instance;
        return instance;
      }
      // or this
      // static S* Instance(){
      //   static S    instance;
      //   return &instance;
      // }
      int getVal()
      { return Instance().val;  }
    private:
      // These functions exist in all cases
      S() {}
      S(S const&);              // Don't Implement.
      void operator=(S const&); // Don't implement
   };
   
   /// Singleton using a static local with private instance function (Monostate Pattern)
  class S2
  {
    public:
      static int getVal()
      { return Instance().val;  }
    private:
      static S2& Instance(){...}
      ...
      int val;
   };
   
   /// Singleton using a static pointer to self
   class S3
  {
    public:
      static S3* Instance()
      {
        if(!instance)
          instance = new S3;
        return instance;
      }
      int getVal()
      { return Instance().val;  }
      void Destroy() 
      {
       delete instance;
       instance=0;
      }
    private:
      static S3 *instance;
      // In S3.cpp:
      // Singleton* Singleton::_instance = 0;
      ...
      int val;
   };
   
   void main()
   {
     // can use reference to use the instance
     S& x = S::Instance();
     cout<< x.getVal();
     
     // can only access member functions
     cout<< S2::getVal();
     
     // can create a pointer
     S3 *ptr = S3::Instance();
     cout<< ptr->getVal();
     cout<< S3::Instance()->getVal();
     // delete ptr;   // This will create problems when Instance() is called again.
     S3::Destroy();   // This is a safer approach
   }
```
