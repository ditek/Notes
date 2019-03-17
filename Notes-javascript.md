# Javascript
<!-- MarkdownTOC -->

- [Language Fundamentals](#language-fundamentals)
    - [Variables](#variables)
    - [Data Types](#data-types)
        - [Arrays](#arrays)
    - [Operators](#operators)
    - [Functions](#functions)
        - [Lambdas](#lambdas)
    - [Asynchronicity](#asynchronicity)
    - [Promises](#promises)
- [Document Operations](#document-operations)
    - [Obtaining ELements](#obtaining-elements)
    - [Handling Events](#handling-events)
    - [Modify div contents](#modify-div-contents)
    - [Window Methods](#window-methods)
        - [setTimeout](#settimeout)
- [AJAX](#ajax)
- [iFrame](#iframe)
    - [Fit size to contents](#fit-size-to-contents)
- [HTML Manipulation](#html-manipulation)
    - [Adding Elements Dynamically](#adding-elements-dynamically)
    - [Removing Elements Dynamically](#removing-elements-dynamically)
- [Useful Snippets](#useful-snippets)
    - [Extract a video and open it in a new tab](#extract-a-video-and-open-it-in-a-new-tab)
    - [Wait for an element to load](#wait-for-an-element-to-load)
    - [Reuse Headers and Footers](#reuse-headers-and-footers)

<!-- /MarkdownTOC -->

# Language Fundamentals

## Variables
- ES6 introduced `let` and `const` as keywords for declaring variables. These are both lexically scoped.
- Do always use `let`/`const`. Do never use `var`. As a rule of thumb, always use `const`, and only switch to `let` when you attempt to reassign the value.

_______________________________________________________________________________
## Data Types

### Arrays
```js
// Creation
var colors = Array("red", "green", "blue");
var color = colors[0];
// Delete element
const index = myArr.indexOf("a");
myArr.splice(index, 1);
```

_______________________________________________________________________________
## Operators
```
==      Compare with type conversion: "0" == 0 => true
===     Literal comparision:    "0" === 0 => false, 0 === 0 => true
?       Ternary operator:       let accessAllowed = (age > 18) ? true : false;
```

## Functions

### Lambdas
```js
const myLambda = function () {
    console.log(this.value);
};
// This way is preferred
const myLambda = () => console.log(this.value);
const myLambda = () => {
    console.log(this.value);
};
```

## Asynchronicity
- All interactions with external resources, happens asynchronously. Like HTTP requests.

## Promises
A `Promise` is an object that holds a `then` and `catch` callback function. It is returned immediately, and when the asynchronous event finishes, the appropriate callback is invoked, depending on the success state of the operation

The `then` callback gets invoked with the return value of the operation, so Promises are typically regarded as a _promise to a future value_.

```js
function doSomethingAsync(value) {
   return new Promise((resolve, reject) => {
       if (value === 42) {
           setTimeout(() => resolve("The meaning of life, the universe, everything"), 1000);
       } else {
           setTimeout(() => reject("This is not the meaning of life"), 1000);
       }
   });
}
doSomethingAsync(42).then((v) => console.log(v), () => console.log("This should not happen"));
```

_______________________________________________________________________________
# Document Operations

## Obtaining ELements

```js
/* By id */
document.getElementById("id");

/* By class */
// Get the first element in the document with class="example":
document.querySelector(".example");
// Get all matching elements
document.querySelectorAll(".example");
```

## Handling Events

```html
<span id="text-container">Click me!</span>
<script>
    const text = document.getElementById("text-container");
    text.onclick = () => {
       text.innerHTML = "Hello, world of DHTML!";
    };
</script>
```

## Modify div contents

```html
<body onload="loadMsg()">
    <div id="msg"></div>
    <script>
        function loadMsg() {
            var msg = document.getElementById("msg")
            msg.innerHTML = "<h1>Write HTML </h1>"
            msg.textContent = "or write text"
        }
    </script>
</body>
```

_______________________________________________________________________________
## Window Methods

### setTimeout
Call a function after a specified number of milliseconds. Default timeout is 1 second.

```js
// Syntax
setTimeout(function, milliseconds, param1, param2, ...)
// Usage
setTimeout(function(){ alert("Hello"); }, 3000);

var x = document.getElementById("txt");
setTimeout(function(){ x.value = "2 seconds" }, 2000);
```

# AJAX
```js
// Create an XMLHttpRequest object
var xhttp = new XMLHttpRequest(); 

// Create a request
xhttp.open( method,             // Request type: "GET" or "POST"
            url,                // Server file location
            async);             // asynchrounous (true) or synchronous (false)
xhttp.open("GET", "get_info.php", true);

// To send information with the GET method, add it to the URL
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true);

// Send the request to the server
xhttp.send()                    // For GET
xhttp.send(string);              // For POST. The string is optional
```

_______________________________________________________________________________
# iFrame

## Fit size to contents
```html

```

_______________________________________________________________________________
# HTML Manipulation

## Adding Elements Dynamically
```js
function addElement(parentId, elementTag, elementId, html) {
    // Adds an element to the document
    var p = document.getElementById(parentId);
    var newElement = document.createElement(elementTag);
    newElement.setAttribute('id', elementId);
    newElement.innerHTML = html;
    p.appendChild(newElement);
    var header = document.createElement('h1');
    header.textContent = "This page has been eaten";
    document.body.appendChild(header);
}
```

## Removing Elements Dynamically
```js
function removeElement(elementId) {
    // Removes an element from the document
    var element = document.getElementById(elementId);
    element.parentNode.removeChild(element);
}
```

_______________________________________________________________________________
# Useful Snippets

## Extract a video and open it in a new tab
```js
var video = document.getElementById("video_streamx_html5_api");
var src = video.src;
var win = window.open(src, '_blank');
```

## Wait for an element to load
```js
function waitForElementToDisplay(selector, time) {
    if(document.querySelector(selector)!=null) {
        console.log("The element is displayed!")
        return;
    } else {
        setTimeout(() => waitForElementToDisplay(selector, time), time);
    }
}
waitForElementToDisplay(".media-play", 1000);
```

## Reuse Headers and Footers

```html
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script> 
    $(function(){
        $("#footer").load("footer.html"); 
    });
    </script> 
</head>
<body>
    ...
    <footer id="footer"/>
</body>

<!-- footer.html -->
<hr />
<small>&copy; 2016 My Awesome Company</small>
```

Or a more generic solution:

```html
<script>
    $(function () {
        var includes = $('[include-view]');
        jQuery.each(includes, function () {
            // Will get the html from 'views/footer.html'
            var file = 'views/' + $(this).data('include') + '.html';
            $(this).load(file);
        });
    });
</script>

<div include-view="footer"></div>
```

To do it in plain JS without JQuery see <https://www.w3schools.com/w3js/w3js_html_include.asp>.

It is possible to utilize a similar technique to use `#filename` in the URL for specifying the page to get the content from. This is explained here: <https://css-tricks.com/dynamic-page-replacing-content/>

