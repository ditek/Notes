# Javascript
<!-- MarkdownTOC -->

- [Language Fundamentals](#language-fundamentals)
    - [Variables](#variables)
    - [Data Types](#data-types)
        - [Strings](#strings)
        - [Arrays](#arrays)
        - [Maps](#maps)
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
- [JQuery](#jquery)
    - [Selectors](#selectors)
    - [Operations](#operations)
    - [Load](#load)
- [Useful Snippets](#useful-snippets)
    - [Extract a video and open it in a new tab](#extract-a-video-and-open-it-in-a-new-tab)
    - [Wait for an element to load](#wait-for-an-element-to-load)
    - [Reuse Headers and Footers](#reuse-headers-and-footers)
    - [Remove all element of a class](#remove-all-element-of-a-class)
    - [Debounce and Throttle](#debounce-and-throttle)

<!-- /MarkdownTOC -->

# Language Fundamentals

## Variables
- ES6 introduced `let` and `const` as keywords for declaring variables. These are both lexically scoped.
- Do always use `let`/`const`. Do never use `var`. As a rule of thumb, always use `const`, and only switch to `let` when you attempt to reassign the value.

_______________________________________________________________________________
## Data Types

### Strings
```js
// Include a variable in a string
x = 5
console.log(`#${x}`);
```

### Arrays
```js
// Creation
var colors = Array("red", "green", "blue");
var color = colors[0];
// Delete element
const index = myArr.indexOf("a");
myArr.splice(index, 1);

/* Functions */
// Sort
myArr.sort((a, b) => a - b);
// Map: Call a function on each element, and return an array that contains the results.
myArr.map((v) => v.toString());
```

### Maps
```js
let m = new Map();

// Get and Set values
m.set("name", "Joe");
m.get("name");   // "Joe"
m.get("age");    // undefined

// Check if value exists
let age = m.get("age");
if (!age)
    m.set("age", 15);

// Iterate over map keys/values
myMap.forEach(value => console.log(value));
myMap.forEach((value, key) => console.log(key, value));

// Array of keys
Array.from(myMap.keys());
// Array of values
Array.from(myMap.values());
// Array of key/value pairs
Array.from(myMap.entries());
```

_______________________________________________________________________________
## Operators
```
==      Compare with type conversion: "0" == 0 => true
===     Literal comparision:    "0" === 0 => false, 0 === 0 => true
?       Ternary operator:       let accessAllowed = (age > 18) ? true : false;
```

## Flow Control

### For
```js
for (const element of theArray) {
    // ...use `element`...
}

theArray.forEach(element => {
    // ...use `element`...
});

for (let index = 0; index < theArray.length; ++index) {
    const element = theArray[index];
    // ...use `element`...
}
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

### Catching Promise Rejection
```js
new Promise((resolve, reject) => {...})
    .then((state) => {...})
    .catch((error) => { console.log(error); });
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

_______________________________________________________________________________
# OS

## Environment Variables
```js
const password = process.env.POSTGRESS_PASSWORD;
```

_______________________________________________________________________________
# Time and Date
```js
// Current time in ms
Date.now()
// Timestamp in ISO format
new Date().toISOString();
```

_______________________________________________________________________________
# AJAX
Async requests (AJAX requests) use one of two methods:
- XMLHttpRequest
- Fetch (modern way)

## XMLHttpRequest

```js
/* Sending a request */
// Create an XMLHttpRequest object
var xhttp = new XMLHttpRequest(); 

// Create a request
xhttp.open( method,             // Request type: "GET" or "POST"
            url,                // Server file location
            async,              // asynchrounous (true - default) or synchronous (false)
            user, password);    // Authentication (optional - defaults to null)         
xhttp.open("GET", "get_info.php");

// To send information with the GET method, add it to the URL
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford");

// Send the request to the server
xhttp.send()                     // For GET
xhttp.send(string);              // For POST. The string is optional

/* Receiving a response */
xhttp.onreadystatechange = function() {
  if (this.readyState === 4 && this.status === 200) { 
    // on successful response
    console.log(xhttp.responseText);
  }
};
```

## Fetch

```js
fetch(<url-route>, <object of request parameters>)

fetch('/my/request', {
  method: 'POST',
  body: JSON.stringify({
    'description': 'some description here'
  }),
  headers: {
    'Content-Type': 'application/json'
  }
})
.then(response => console.log(response.json()))
.catch(console.log('error');
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
# URL
## Build URL with query params
```js
const params = new URLSearchParams({
    x: "1",
    y: "2",
});
const url = `example.com?${params.toString()}`;
// example.com?x=1&y=2
```

_______________________________________________________________________________
# JQuery

## Selectors
https://www.w3schools.com/cssref/css_selectors.asp

```js
/*** Selectors ***/
//All elements
$("*")
// The element with id="lastname"
$("#lastname")
// All elements with class="intro"
$(".intro")
// All elements with the class "intro" or "demo"
$(".intro,.demo")
// All elements with the class "intro" and "demo"
$(".intro.demo")
// All elements with the class "demo" that is a descendant of an element with "intro"
$(".intro .demo")

// All <p> elements
$("p")
$("div, p")     // Selects all <div> elements and all <p> elements
$("div p")      // Selects all <p> elements inside <div> elements
$("div > p")    // Selects all <p> elements where the parent is a <div> element
$("div + p")    // Selects all <p> elements that are placed immediately after <div> elements
$("p ~ ul")     // Selects all <ul> elements that are preceded by a <p> element

$('[title]')          // Selects all elements with a title attribute
$('[title=flower]')  // Selects all elements with title="flower"
$('[title~=flower]')  // Selects all elements with a title attribute containing the word "flower"
$('[title|=fl]')      // Selects all elements with a title attribute value starting with "fl"
;
```

## Operations

```js
// Find an inner element
$("ul").find("span")

// Add class
$( "p" ).addClass( "class1 class2" );

// Get attribute value
$('#A').attr('myattr')
// Check if attribute exists and not empty
if ($('#A').attr('myattr')){}
// Check if attribute exists
if ($('#A').attr('myattr') !== undefined){}
```

## Load
Load an html page as to an element with an optional callback to be called when loading is done.

```js
.load( url [, data ] [, complete ] )

$( "#result" ).load( "ajax/test.html" );
$( "#result" ).load( "ajax/test.html", function() {
  alert( "Load was performed." );
});
```

_______________________________________________________________________________
# Testing

## Unit Tests with Mocha and Chai
Test files are made up of test collections each of which starts with `describe()` function. A test collection can have multiple tests each start with `it()` function.

Tests can be run using `npm test`.

```js
import { expect } from 'chai';
import 'mocha';

describe('divide', () => {

  it('should divide 5 and 2', () => {
    const result = divide(5,2);
    expect(result).to.equal(2.5);
  });

  it('should throw an error if div by zero', () => {
    expect(()=>{ divide(5,0) }).to.throw('div by 0')
  });

});
```

## Integration Tests with Postman
Within Postman, in the `Tests` tab, we can write JS tests that use a syntax similar to `Chai`'s `expect` statements.

```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("Hello world!")
});
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

## Remove all element of a class
```js
$(".limit").each(function(){$(this).removeClass("limit")});
```

## Debounce and Throttle
- *debounce*: Grouping a sudden burst of events (like keystrokes) into a single one.
- *throttle*: Guaranteeing a constant flow of executions every X milliseconds. Like checking every 200ms your scroll position.

The can be obtained from `lodash`:

```html
<script src="lodash.js"></script>
```

```js
npm i -g lodash-cli
lodash include = debounce, throttle

var _ = require('lodash');
```

_Example_

```js
$(window).on('scroll', _.debounce(doSomething, 200));
```

_______________________________________________________________________________
# NPM
```sh
# Install a local package
npm i bcrypt
# Install a local package and save it to package.json
npm i bcrypt --save
# Install a local package and save it as a development dependencies
npm i @types/bcrypt --save-dev
```
_______________________________________________________________________________
# Authorization and Authentication
Useful information <https://auth0.com/blog/navigating-rs256-and-jwks/>

```js
import { verify } from 'jsonwebtoken'

const secretId = process.env.AUTH_0_SECRET_ID
const secretField = process.env.AUTH_0_SECRET_FIELD

interface JwtToken {
  iss: string
  sub: string
  iat: number
  exp: number
}

function verifyToken(authHeader: string, secret: string): JwtToken {
  if (!authHeader)
    throw new Error('No authentication header')

  if (!authHeader.toLowerCase().startsWith('bearer '))
    throw new Error('Invalid authentication header')

  const split = authHeader.split(' ')
  const token = split[1]

  return verify(token, secret) as JwtToken
}

handler.use(
  secretsManager({
    cache: true,
    cacheExpiryInMillis: 60000,
    // Throw an error if can't read the secret
    throwOnFailedCall: true,
    secrets: {
      AUTH0_SECRET: secretId
    }
  })
)
;
```


_______________________________________________________________________________
# Libraries

## Express.js
A Node.js web server framework.

```js
import express, { Request, Response } from 'express';
import bodyParser from 'body-parser';

(async () => {
  // Init the Express application
  const app = express();

  // Set the network port
  const port = process.env.PORT || 8082;
  
  // Use the body parser middleware for post requests (see mddleware section)
  app.use(bodyParser.json());

  // Set up an endpoint
  app.get("/", async (req: Request, res: Response) => {
    res.status(200).send("Welcome!")
  } );

  // Start the Server
  app.listen( port, () => {
      console.log( `server running http://localhost:${ port }` );
      console.log( `press CTRL+C to stop server` );
  } );
})();
```

### Routing
Routing refers to how an application’s endpoints (URIs) respond to client requests. You define routing using methods of the Express `app` object that correspond to HTTP methods passing a path and a handler `app.METHOD(PATH, HANDLER)`.

```js
  // Endpoints with path parameters:
  app.get("/users/:userId/books/:bookId", (req: Request, res: Response) => {
    // req.params: { "userId": "34", "bookId": "8989" }
    let { userId, bookId } = req.params;
    // OR
    let userId = req.params.userId
    if (!userId) {
      return res.status(400).send('userId is required')
    }
    ...
  });

  // Endpoints with query parameters: {{host}}/persons?userId=58?bookId=22
  app.get("/persons/", (req: Request, res: Response) => {
    // req.query: { "userId": "34", "bookId": "8989" }
    let { userId, bookId } = req.query;
    ...
  });

  // Post requests. Use {"userId": "myname"} as an application/json body
  app.post("/persons", (req: Request, res: Response) => {
    // req.body: { "userId": "34", "bookId": "8989" }
    let { userId, bookId } = req.body;
    ...
  });
```

Route handlers can be chained using `app.route`:

```js
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  });
```

#### Route Paths
The characters ?, +, *, and () are subsets of their regular expression counterparts. The hyphen (-) and the dot (.) are interpreted literally by string-based paths.

```
Route path: /ab*cd
Matches: /abcd, /abxcd, /abRANDOMcd, /ab123cd, ...

Route path: /ab(cd)?e'
Matches: /abe and /abcde
```

Route parameters are preceded by a colon:

```json
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

Since the hyphen (-) and the dot (.) are interpreted literally, they can be used along with route parameters for useful purposes.

```json
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }

Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

A regular expression can be appended in parentheses:

```json
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

#### Express Router
An `express.Router` object is an isolated instance of middleware and routes. It is kind of a "mini-app" as it only includes the routing functionality of `app`. It is useful to modularize routing.

```js
// server.ts
import { UserRouter } from './controllers/v0/user.router';
app.use('/api/v0/user/', UserRouter)

// user.router.ts
import { Router } from 'express';
const router: Router = Router();
// Matches "/api/v0/user/"
router.get('/', ...);
export const UserRouter: Router = router;
```

### Middleware
Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the `next` function in the application’s request-response cycle. The `next` function is a function in the Express router which executes the next middleware.

Middleware is added to the stack of `app` or another route using:

- `use(foo())`: `foo` is called for all paths.
- `use(path, foo())`: `foo` is called for the specified path.
- `METHOD(foo())`, where `METHOD` is `get`, `post`, etc.
- `METHOD(path, foo())`, where `METHOD` is `get`, `post`, etc.

```js
// Called upon any message to any path
app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// Called upon any message to '/user/:id'
app.use('/user/:id', function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// Function `requireAuth` is called before handling the request
function requireAuth(req: Request, res: Response, next: NextFunction) {
    if (!req.headers || !req.headers.authorization){
        return res.status(401).send({ message: 'No authorization headers.' });
    }
    return next();
}
router.get('/verification', 
    requireAuth, 
    (req: Request, res: Response) => {
        return res.status(200).send({ auth: true, message: 'Authenticated.' });
});
```

_______________________________________________________________________________
## Object-Relational Mapping (ORM) via Squelize
ORM is a technique that allows writing SQL queries using objected-oriented code.

_Note: Examples are in Typescript_

### Squelize Models
A model is a class that extends `Sequelize.Model`. It usually represents a table.

```js
// ./src/controllers/v0/users/models/User.ts

import {Table, Column, Model, PrimaryKey, CreatedAt, UpdatedAt} from 'sequelize-typescript';

@Table
export class User extends Model<User> {
  @PrimaryKey
  @Column
  public email!: string;

  @Column
  public password_hash!: string; // `!` for nullable fields

  @Column
  @CreatedAt
  public createdAt: Date = new Date();

  @Column
  @UpdatedAt
  public updatedAt: Date = new Date();

  short() {
    return {
      email: this.email
    }
  }
}
```

### Instantiation

```js

// ./src/config/config.ts

export const config = {
  "dev": {
    "username": "udagramdb",
    "password": "udagramdb",
    "database": "udagramdb",
    "host": "db-endpoint",
    "dialect": "postgres",
    "aws_region": "us-east-2",
    "aws_profile": "default",
    "aws_media_bucket": "s3-bucket-name"
  },
  "prod": {
    ...
  }
}

/*************************************/
// ./src/sequelize.ts

import {Sequelize} from 'sequelize-typescript';
import { config } from './config/config';

const c = config.dev;

export const sequelize = new Sequelize({
  "username": c.username,
  "password": c.password,
  "database": c.database,
  "host":     c.host,

  dialect: c.dialect,
  storage: ':memory:',
});

/*************************************/
// ./src/controllers/v0/model.index.ts

import { User } from './users/models/User';
export const V0MODELS = [ User ];

/*************************************/
// ./src/server.ts

import { sequelize } from './sequelize';
import { V0MODELS } from './controllers/v0/model.index';

(async () => {
  // We can of course use addModels([User], but this is more maintainable
  await sequelize.addModels(V0MODELS);
  // Sync applies available migrations
  await sequelize.sync();
})();

```

### Migration


### Operations
```js
import { User } from '../models/User';

// Get a row by primary key (id)
const user = await User.findByPk(1);

// Get rows
const users = await User.findAndCountAll({order: [['id', 'DESC']]});

// Update row
const item = await FeedItem.findByPk(id)
item.set({name:"Joe"})
await item.save()
// OR
await item.update({name:"Joe"})

// New row
const user = await new User({
        email: "xxx@gmail.com"
});
const saved_user = await user.save();
```

_______________________________________________________________________________
## AWS

```sh
npm install aws-sdk --save-dev
```

### S3
```js
import AWS = require('aws-sdk');
// For TS
import * as AWS  from 'aws-sdk'

// Configure AWS credentials ONLY if running locally. If deployed to EC2 the
// credentials will be assigned automatically.
// To do so, define an environment variable and set it differently on EC2,
// e.g. "DEPLOYED" and evaluate it as done below
if (c.aws_profile !== "DEPLOYED") {
  var credentials = new AWS.SharedIniFileCredentials({ profile: c.aws_profile });
  AWS.config.credentials = credentials;
}

const s3 = new AWS.S3({
  signatureVersion: 'v4',
  region: 'us-east-1',
  params: {Bucket: 'my-bucket-name'}
});

// Obtain signed URL
const urlParams = {
    Bucket: 'my-bucket-name',
    // File name when saving/getting it
    Key: 'photo.jpg',
    Expires: (60 * 5)
  };
/* IMPORTANT: See the other usage below */
const downloadUrl = s3.getSignedUrl('getObject', urlParams);
const uploadUrl = s3.getSignedUrl('putObject', urlParams);

// The file will uploaded to
const fileUrl = `https://${bucketName}.s3.${region}.amazonaws.com/${imageName}`
// If the region is 'us-east-1' it can be omitted
const fileUrl = `https://${bucketName}.s3.amazonaws.com/${imageName}`

/* IMORTANT */
// getSignedUrl might not return the url directly if it has to fetch the
// credentials (when running on EC2 for example).
// In such case, use the overload that takes a callback and returns a promise.
const url = new Promise((resolve, reject) => {
  s3.getSignedUrl('getObject', urlParams, (error, url) => {
    if (error) {
      reject(error);
    } else {
      resolve(url);
    }
  })
});
```

_______________________________________________________________________________
### DynamoDB

```js
import * as AWS  from 'aws-sdk'
const docClient = new AWS.DynamoDB.DocumentClient();
```

#### Operations

__Scan__

Scan returns up to 1 MB of data. If the data is larger than that, it also returns `LastEvaluatedKey`, which can be passed to the next Scan.


```js
// Get all
const result = await docClient.scan({
  TableName: tableName,
  // Optional: limit returned fields
  Limit: 20
}).promise();
const items = result.Items;

// Get next page
if (result.LastEvaluatedKey) {
  const newResult = await docClient.scan({
    TableName: tableName,
    Limit: 20,
    ExclusiveStartKey: result.LastEvaluatedKey
  }).promise();
}

// Notice that the value of the LastEvaluatedKey in a DynamoDB result is a JSON object. To pass it in another GET request we convert it to a string and then use URI encoding to allow to pass it in a URL:
const nextKeyStr = encodeURIComponent(JSON.stringify(lastEvaluatedKey));
// To parse it back:
const exclusiveStartKey = JSON.parse(decodeURIComponent(nextKeyStr));
```

__Put__

```js
await docClient.put({
  TableName: tableName,
  Item: {id, field1, field2}
}).promise();
```

__Delete__

```js
await docClient.delete({
  TableName: tableName,
  Key: {id: 1}
}).promise();
```

__Get__

```js
const result = await docClient.get({
  TableName: tableName,
  Key: {id: 1}
}).promise();
return result.Item
```

__Update__

```js
const updated = {name: "Joe", dueDate: "2019", done: true}
await docClient.update({
  TableName: tableName,
  // The key needs to include the sort key as well if present
  Key: { id: 1 },
  UpdateExpression: "set #n = :n, dueDate = :dD, done = :d",
  ExpressionAttributeValues: {
    ":n": updated.name,
    ":dD": updated.dueDate,
    ":d": updated.done
  },
  // `name` is a reserved keyword, so we need to do this to use it
  ExpressionAttributeNames:{
    "#n": "name"
  },
  ReturnValues: "UPDATED_NEW"
}).promise();
```

__Query__

The Query operation finds items based on primary key values. The primary key can be a composite primary key (a partition key and a sort key).

Using a query, we can get all items with a particular partition key and
- filter by the sort key using operators: `<, >, <=, >=, =, BETWEN, BEGINS_WITH`.
- filter by any other attribute.

You MUST specify an EQUALITY condition for the PARTITION key, and you can optionally provide another condition for the SORT key.

```js
const result = await docClient.query({
   TableName: 'GameScore',
   KeyConditionExpression: 'GameId = :gameId',
   ExpressionAttributeValues: {
     ':gameId': '10'
   }
   // (Optional) Reverse order
   ScanIndexForward: false
 }).promise()
 const items = result.Items;
```

#### Enable Streaming
```js

```
_______________________________________________________________________________
### API Gateway
```js
const connectionParams = {
  apiVersion: "2018-11-29",
  endpoint: `${apiId}.execute-api.us-east-1.amazonaws.com/${stage}`
}
const apiGateway = new AWS.ApiGatewayManagementApi(connectionParams);
```

_______________________________________________________________________________
### ElasticSearch

```sh
npm install elasticsearch --save
 npm install @types/elasticsearch --save-dev
```

#### Resources and handler

- Streaming needs to be enabled in DynamoDB. See Resources section for details.
- Deployment make take upto an hour.

```yaml
functions:
  SyncWithElasticsearch:
    environment:
      ES_ENDPOINT: !GetAtt ImagesSearch.DomainEndpoint
    handler: src/lambda/dynamoDb/elasticSearchSync.handler
    events:
      - stream:
          type: dynamodb
          arn: !GetAtt ImagesDynamoDBTable.StreamArn

resources:
  Resources:
    ImageSearch:
      Type: AWS::Elasticsearch::Domain
      Properties:
        ElasticsearchVersion: '6.3'
        DomainName: todo-search-${self:provider.stage}
        ElasticsearchClusterConfig:
          DedicatedMasterEnabled: false
          InstanceCount: '1'
          ZoneAwarenessEnabled: false
          InstanceType: t2.small.elasticsearch
        EBSOptions:
          EBSEnabled: true
          Iops: 0
          VolumeSize: 10
          VolumeType: 'gp2'

        AccessPolicies:
          Version: '2012-10-17'
          Statement:
            - Effect: Allow
              Principal:
                AWS: '*'
              Action: 'es:*'
              Resource: '*'
```

```js
import * as elasticsearch from 'elasticsearch'
import * as httpAwsEs from 'http-aws-es'
const es = new elasticsearch.Client({
  hosts: [ process.env.ES_ENDPOINT ],
  connectionClass: httpAwsEs
});

// Store a document in Elasticsearch
await es.index({
  index: 'images-index',
  type: 'images',
  id: 'id', // Document ID
  body: {   // Document to store
    title: 'title',
    imageUrl: 'https://example.com/image.png'
  }
});
```


Setup an index pattern to configure what indexes to use in Kibana:
- From AWS ElasticSearch -> Kibana -> Management -> Index Patterns -> Create a new pattern.
- Optionally select a time filter which allows to filter by timestamp.

_______________________________________________________________________________
## Serverless

### Project Structure
```
/node_modules
  - plugins, prod. and dev. dependencies
/src
  - function.js
serverless.yml
package.json
package-lock.json
```

### Setup
```sh
# 1. INSTALL
npm install -g serverless
# 2. Create a new IAM user and call it "serverless" for example
# 3. Configure serverless with the created user's credentials
sls config credentials --provider aws --key YOUR_ACCESS_KEY --secret YOUR_SECRET_KEY --profile serverless
# 4. List available project templates
serverless create --template
# 5. Create a project from template
serverless create --template aws-nodejs-typescript --path folder-name
# 6. Make changes and deploy to AWS
sls deploy -v
```

_NOTE_: if you get a permissions error when you run deploy you may need to specify the user profile

```sh
sls deploy -v --aws-profile serverless
```

### Configuration File
```yaml
service:
  name: serverless-app

provider:
  name: aws
  runtime: nodejs12.x
  region: 'us-east-1'

  # APIGateway stage. Use 'deploy' command parameter if given or 'dev' by default
  stage: ${opt:stage, 'dev'}

  iamRoleStatements:
    - Effect: Allow
      Action:
        - dynamodb:Scan
      Resource: arn:aws:dynamodb:${self:provider.region}:*:table/${self:provider.environment.GROUPS_TABLE}

  # Environment variables
  environment:
    ENV_VAR_1: env-var-1
    # Make table name dependent on the stage
    GROUPS_TABLE: Groups-${self:provider.stage}

plugins:
  - serverless-webpack

# Allows defining additional configurations. This can be special commands
# used by plugins (see ##Plugins) or variables we only want to access in this
# file (unlike environment variables which are also accessible by functions).
custom:
  # A variable
  topicName: imagesTopic-${self:provider.stage}

resources:
  Resources:
    # CloudFormation YAML definition

functions:
  # Lambda function name
  GetOrders:
    # <file-path>.<JS-function-name>
    handler: src/orders.handler
    # Environment variables local to the function
    API_ID: WebsocketsApi
    # Events that trigger this function
    events:
      - http:
          method: get
          # A path with path parameter
          path: /shop/{itemId}/orders
          cors: true
          # Request validation without using external plugins
          request:
            # Schema that will be used to validate incoming requests
            # Schema format can found at #####validation-model
            schema:
              application/json: ${file(models/create-todo-model.json)}
```

### CloudFormation Resources

```yaml
resources:
  Resources:
    # DynamoDB
    MyDynamoDBTable:
      Type: AWS::DynamoDB::Table
      Properties:
        # NOTE: DynamoDB is schemaless. Only put the items used in keys.
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
          - AttributeName: timestamp
            AttributeType: S
          - AttributeName: imageId
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH
          - AttributeName: timestamp
            KeyType: RANGE
        BillingMode: PAY_PER_REQUEST
        TableName: ${self:provider.environment.GROUPS_TABLE}

        # (Optional) Global secondary index to allow querying by imageId
        GlobalSecondaryIndexes:
          - IndexName: ImageIdIndex
            KeySchema:
            - AttributeName: imageId
              KeyType: HASH
            Projection:
              # The new table includes projection of all fields in the original
              ProjectionType: ALL

        # (Optional) Enable streaming
        StreamSpecification:
          # Each record in the stream will contain the updated item
          StreamViewType: NEW_IMAGE

# -------------------------------------

    # RequestValidator
    RequestBodyValidator:
      Type: AWS::ApiGateway::RequestValidator
      Properties:
        Name: 'request-body-validator'
        RestApiId:
          Ref: ApiGatewayRestApi
        ValidateRequestBody: true
        ValidateRequestParameters: false

# -------------------------------------
    
    # S3
    AttachmentsBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: ${self:provider.environment.IMAGES_S3_BUCKET}
        # (Optional) Configure notification
        NotificationConfiguration:
          TopicConfigurations:
            - Event: s3:ObjectCreated:Put
              Topic: !Ref ImagesTopic
        CorsConfiguration:
          CorsRules:
            -
              AllowedOrigins:
                - '*'
              AllowedHeaders:
                - '*'
              AllowedMethods:
                - GET
                - PUT
                - POST
                - DELETE
                - HEAD
              MaxAge: 3000

    # S3 Bucket Policy - Allow other resources to access the bucket
    BucketPolicy:
      Type: AWS::S3::BucketPolicy
      Properties:
        PolicyDocument:
          Id: MyPolicy
          Version: "2012-10-17"
          Statement:
            - Sid: PublicReadForGetBucketObjects
              Effect: Allow
              Principal: '*'
              Action: 's3:GetObject'
              Resource: 'arn:aws:s3:::${self:provider.environment.IMAGES_S3_BUCKET}/*'
        Bucket: !Ref AttachmentsBucket

# -------------------------------------

    # SNS

    # SNS Topic
    ImagesTopic:
      Type: AWS::SNS::Topic
      Properties:
        # Human readable name
        DisplayName: Image bucket topic
        TopicName: ${self:custom.topicName}

    # SNS Topic Policy to allow S3 to send events to the topic above
    SNSTopicPolicy:
      Type: AWS::SNS::TopicPolicy
      Properties:
        PolicyDocument:
          Version: "2012-10-17"
          Statement:
            - Effect: Allow
              Principal:
                AWS: "*"
              Action: sns:Publish
              Resource:
                !Ref ImagesTopic
              Condition:
                ArnLike:
                  AWS:SourceArn: arn:aws:s3:::${self:provider.environment.IMAGES_S3_BUCKET}
        Topics:
          - !Ref ImagesTopic

# -------------------------------------

    # KMS

    KMSKey:
      Type: AWS::KMS::Key
      Properties:
        Description: KMS key to encrypt Auth0 secret
        KeyPolicy:
          Version: '2012-10-17'
          Id: key-default-1
          Statement:
            # Allow root user full access
            - Sid: Allow administration of the key
              Effect: Allow
              Principal:
                AWS:
                  Fn::Join:
                  - ':'
                  - - 'arn:aws:iam:'
                    - Ref: AWS::AccountId
                    - 'root'
              Action:
                - 'kms:*'
              Resource: '*'

    # Human readable name for the key
    KMSKeyAlias:
      Type: AWS::KMS::Alias
      Properties:
        AliasName: alias/auth0Key-${self:provider.stage}
        TargetKeyId: !Ref KMSKey

    # The secret we want to store
    Auth0Secret:
      Type: AWS::SecretsManager::Secret
      Properties:
        Name: ${self:provider.environment.AUTH_0_SECRET_ID}
        Description: Auth0 secret
        # Which KMS key to use for encryption
        KmsKeyId: !Ref KMSKey

    # Don't forget to add IAM policies to allow accessing the secrets
    - Effect: Allow
      Action:
        - secretsmanager:GetSecretValue
      Resource: !Ref Auth0Secret
    - Effect: Allow
      Action:
        - kms:Decrypt
      Resource: !GetAtt KMSKey.Arn

# -------------------------------------
    
```

_______________________________________________________________________________
### AWS Lambda Events

#### HTTP Events
```yaml
  GetOrders:
    handler: src/orders.handler
    events:
      - http:
          method: get
          # A path with path parameter
          path: /shop/{itemId}/orders
          cors: true
          # Call MyAuthFunc first to check if the caller is allowed to invoke us
          authorizer: MyAuthFunc
          # Request validation without using external plugins
          request:
            # Schema that will be used to validate incoming requests
            schema:
              application/json: ${file(models/create-todo-model.json)}
```

```js
export const handler: APIGatewayProxyHandler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
  const parsedBody = JSON.parse(event.body)
  return {
      statusCode: 200,
      // Allow CORS
      headers: {
        'Access-Control-Allow-Origin': '*'
      },
      body: "A string body"
  }
}
```

#### S3 Events
We need to:
- Add a new property to the S3 resource.
- Add a permission resource
- Define the function with no event handler.

_NOTE_: S3 allows only one notification target. Meaning no more than one lambda can react to an even. The alternative is to use SNS to receive and then broadcast the event.

```yaml
functions:
  SendUploadNotifications:
    handler: src/lambda/s3/sendNotifications.handler

resources:
  Resources:
    AttachmentsBucket:
      ...
      Properties:
        NotificationConfiguration:
          TopicConfigurations:
            - Event: s3:ObjectCreated:Put
              Topic: !GetAt SendUploadNotificationsLambdaFunction.Arn
              # This can also be an SNS topic as well
              # (see ###CloudFormation Resources - SNS)
              Topic: !Ref ImagesTopic

    SendUploadNotificationsPermission:
      Type: AWS::Lambda::Permission
      Properties:
        FunctionName: !Ref SendUploadNotificationsLambdaFunction
        Principal: s3.amazonaws.com
        Action: lambda:InvokeFunction
        SourceAccount: !Ref AWS::AccountId
        SourceArn: arn:aws:s3:::${self:provider.environment.BUCKET_NAME}
```

```js
// src/lambda/s3/sendNotifications.ts
import { S3Handler, S3Event } from 'aws-lambda'
export const handler: S3Handler = async (event: S3Event) => {}
```

#### WebSocket Events
```yaml
  ConnectHandler:
    handler: src/websocket/connect.handler
    events:
      - websocket:
          route: $connect

  DisconnectHandler:
    handler: src/websocket/disconnect.handler
    events:
      - websocket:
          route: $disconnect
```

```js
export const handler: APIGatewayProxyHandler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
  const connectionId = event.requestContext.connectionId
}
```

To test websockets we can use `wscat`:

```sh
npm install -g wscat
wscat -c wss://<ip>
```

#### DynamoDB Stream Events

```yaml
  NewDBItem:
    handler: src/lambda/dynamoDb/dynamodbNewItem.handler
    events:
      - stream:
          type: dynamodb
          arn: !GetAtt ImagesDynamoDBTable.StreamArn
```

Records contain data in a special format called DynamoDB JSOn, where elements are accessed using their type. For more information: http://bit.ly/dynamo-db-json

```js
export const handler: DynamoDBStreamHandler = async (event: DynamoDBStreamEvent) => {
  for (const record of event.Records) {
    // Item after modification
    const newItem = record.dynamodb.NewImage
    // Item before modification
    const oldItem = record.dynamodb.OldImage
    const id = newItem.id.S         // String attribute
    const count = newItem.count.N   // Number attribute
  }
}
```

#### SNS Events

SNS topic has the following format:

`arn.aws.sns:<region>:<account-id>:<topic-name>`

We use the `Join` function to create it as shown below.

```yaml
  SendUploadNotifications:
    environment:
      STAGE: ${self:provider.stage}
      API_ID:
        Ref: WebsocketsApi
    handler: src/lambda/s3/sendNotifications.handler
    events:
      - sns:
          arn:
            Fn::Join:
              - ':'
              - - arn:aws:sns
                - Ref: AWS::Region
                - Ref: AWS::AccountId
                - ${self:custom.topicName}
          topicName: ${self:custom.topicName}
```

```js
export const handler: SNSHandler = async (event: SNSEvent) => {
  for (const snsRecord of event.Records) {
    const s3EventStr = snsRecord.Sns.Message
    const s3Event = JSON.parse(s3EventStr)
  }
}
```

#### Authorization Event
A custom authorizer is a Lambda function that is executed before processing a request. Custom authorizer returns an IAM policy that defines what Lambda functions can be called by a sender of a request.

Notice, that the result of a custom authorizer call is cached. A good practice is to provide access to all functions an owner of a token can access.

The authoizer has no events in YAML. Instead, it has to be invoked by another handler. See [](####http-events).

The following handler allows the invocation of any lambda function if authorized.

```js
export const handler: CustomAuthorizerHandler = async (event: CustomAuthorizerEvent): Promise<CustomAuthorizerResult> => {
  try {
    // This function checks if the token is valid and throws an error if not
    verifyToken(event.authorizationToken)
    return {
      principalId: 'user-id',
      policyDocument: {
        Version: '2012-10-17',
        Statement: [
          {
            Action: 'execute-api:Invoke',
            // Allow to invoke any lambda function
            Effect: 'Allow',
            Resource: '*'
          }
        ]
      }}} catch (e) {
    console.log('User was not authorized', e.message)
    return {
      principalId: 'user-id',
      policyDocument: {
        Version: '2012-10-17',
        Statement: [
          {
            Action: 'execute-api:Invoke',
            Effect: 'Deny',
            Resource: '*'
          }
        ]
      }}}
    }
```

Even if the authorization was rejected, we still need to return correct CORS headers. To do that, we need to define a `GatewayResponse` resource:

```yaml
    GatewayResponseDefault4XX:
      Type: AWS::ApiGateway::GatewayResponse
      Properties:
        ResponseParameters:
          gatewayresponse.header.Access-Control-Allow-Origin: "'*'"
          gatewayresponse.header.Access-Control-Allow-Headers: "'Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token'"
          gatewayresponse.header.Access-Control-Allow-Methods: "'GET,OPTIONS,POST'"
        ResponseType: DEFAULT_4XX
        RestApiId:
          Ref: ApiGatewayRestApi
```

_______________________________________________________________________________
### Serverless Plugins
Many plugins can be added to extend the functionality of Serverless.

#### Request Validation
_NOTE_: This can be achieved without using plugins. See [](###configuration-file).

This allows us to define models to validate HTTP requests. We need these two plugins:
- `serverless-reqvalidator-plugin`
- `serverless-aws-documentation`

Also see how to create a `RequestValidator` resource above.

```yaml
custom:
  documentation:
    api:
      info:
        version: v1.0.0
        title: Udagram API
        description: Serverless application for images sharing
    models:
      - name: GroupRequest
        contentType: application/json
        schema: ${file(models/create-group-request.json)}

# Specify the functions we want to validate
functions:
  GetOrders:
    handler: src/orders.handler
    events:
      - http:
          method: get
          path: /shop/orders
          cors: true
          # We can set a validator to validate requests
          reqValidatorName: 
          documentation:
            summary: Create a new group
            description: Create a new group
            requestModels:
              'application/json': GroupRequest
```

##### Validation Model

```json
// models/create-group-request.json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "group",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "id": {
      "type": "number"
    }
  },
  "required": ["id"],
  // Whether additional fields are allowed
  "additionalProperties": false
}
```

### Supported events
https://serverless.com/framework/docs/providers/aws/events/apigateway/

- API Gateway: REST/WebSocket API
- SQS (Simple Queue Service)
- CloudWatch Events
- CloudWatch Logs: to process log events
- Kinesis, DynamoDB: to process update streams
- SNS (Simple Notification Service)

_______________________________________________________________________________
## Bcrypt
```js
import * as bcrypt from 'bcrypt';
const saltRounds = 10;
const salt = await bcrypt.genSalt(saltRounds);
const hash = await bcrypt.hash(plainTextPassword, salt);
const compare = await bcrypt.compare(plainTextPassword, hash);
```

_______________________________________________________________________________
## JWT via jsonwebtoken
```js
import * as jwt from 'jsonwebtoken';
jwtToken = jwt.sign(user, config.dev.jst.secret);
 // Verify the token. If an exception is not thrown a JWT is valid
jwt.verify(jwtToken, secret);
```

_______________________________________________________________________________
## Ionic
Ionic is a framework for hybrid mobile/web apps.

### Ionic CLI
```sh
# Build the project into static HTML/CSS/JS files at ./www
ionic build
# Start the Ionic server
ionic serve

```

_______________________________________________________________________________
## UUDI
```js
import * as uuid from 'uuid'
const itemId = uuid.v4();
```

_______________________________________________________________________________
## Middy
A library to add middleware to HTTP handlers. It provides different middleware types:

- `cors`: Return CORS headers.
- `httpErrorHandler`: Return HTTP error if an exception from `http-errors` is thrown.
- `secretsManager`: Read parameters from AWS Secrets Manager.
- `ssm`: Read parameters from AWS Secrets Manager.
- `validator`: Validate incoming requests and outgoing responses.

### `cors` Middleware Example

```js
import * as middy from 'middy'
import { cors } from 'middy/middlewares'
export const handler = middy(
  async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
     ...
  }
)
handler
  .use(cors({
    // Optionally send headers that allow sending credentials from the browser
    credentials: true
  }));
```

### `secretsManager` Middleware Example

```js
import { secretsManager } from 'middy/middlewares'
export const handler = middy(async (event: CustomAuthorizerEvent, context): Promise<CustomAuthorizerResult> => {
  try {
    const decodedToken = verifyToken(
      event.authorizationToken,
      context.AUTH0_SECRET[secretField]
    )
    console.log('User was authorized', decodedToken)

    return {
      principalId: decodedToken.sub,
      policyDocument: {
        Version: '2012-10-17',
        Statement: [
          {
            Action: 'execute-api:Invoke',
            Effect: 'Allow',
            Resource: '*'
          }
        ]
      }
    }
  } catch (e) {
    console.log('User was not authorized', e.message)
    return {
      principalId: 'user',
      policyDocument: {
        Version: '2012-10-17',
        Statement: [
          {
            Action: 'execute-api:Invoke',
            Effect: 'Deny',
            Resource: '*'
          }
        ]
      }
    }
  }
})

function verifyToken(authHeader: string, secret: string): JwtToken {
  if (!authHeader)
    throw new Error('No authentication header')

  if (!authHeader.toLowerCase().startsWith('bearer '))
    throw new Error('Invalid authentication header')

  const split = authHeader.split(' ')
  const token = split[1]

  return verify(token, secret) as JwtToken
}

handler.use(
  secretsManager({
    // If the secret is cached, we won't request it again
    cache: true,
    cacheExpiryInMillis: 60000,
    // Throw an error if can't read the secret
    throwOnFailedCall: true,
    // Secrets to fetch from secretsManager
    secrets: {
      AUTH0_SECRET: secretId
    }
  })
)

```







