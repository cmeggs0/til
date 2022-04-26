# Learning JavaScript through Scrimba's Bootcamp
- Primarily used in the browser
- <script> </script> to embed in an html doc
- Like Ruby, strings need to be contained by "" or ''
- file.js to create a JavaScript file
```{html}
 <script src="file.js"></script>
```
- Use code above to embed js file in html doc
## The Basics 
### Variables
- var is the keyword to define a variable, eg.
```js
 var username;
```
- Creates variable username, default value is null
```js
 var username = "John";
 console.log(username);
```
- Creates and assigns variable username with the string "John"
- Console prints "John"
- Convention for js is to camelCase them
- More concrete rules for variables:
  1. Only contain letters, numbers, symbols $_
  2. First character must not be a number
  3. Cannot use reserved words, such as var
- If we don't use var, then it is assigned to the global object:
  - In the browser, it is called window
  - In the server, it is called global
  - globalThis references either
- 2 modes of js:
  1. Sloppy mode - default in scripts
  2. Strict mode- throws more errors, prevents pitfalls of the language
    - "use strict";
    - Run in strict mode whenever you can
    - Doesn't allow hoisting - the ability to access a variable before it has been created - but it doesn't log an error
- let or const create variables, but don't allow hoisting, gives a ReferenceError
  - Use let when variable can change, can initialize and assign on different lines
  - Use const when variable will never change, best in most cases due to its restrictions:
    1. Must be initialized with value
    2. Cannot be reassigned after declaration
    - Works best with primatives: numbers, strings, etc.
### Template literals
- + adds strings, but easy to forget spaces
```js
let username = "John Smith";
let message = "Hi" + username;
console.log(message);
```
- Prints HiJohn Smith
- Instead:
```js
let username = "John Smith";
let message = `Hi ${username}`;
console.log(message);
```
- Prints Hi John Smith
- Use ` (backticks) to surround template literal
- ${} to interpolate variable within the literal, similar to #{} in ruby
- Can do calculations or conditionals within ${}
- \ to ignore "' within a string, or just use template literal
- \n for new line \r to return within a string, or again use template literals and actually just use return to break into lines
Other thoughts about variable names:
- Should be self-descriptive
- Are case-sensitive
- prefix is- or has- for conditionals
- USE ALL_CAPS AND _ IF YOU NEVER WANT THE VARIABLE CHANGED
### Conditionals
- if statements evaluate boolean values, note else and else if are outside of first set of brackets
```js
if (statementBeingEvaluated) {
  console.log('Will print this string if first statement is true');
} else if (secondStatementBeingEvaluated) {
  console.log('Will print this string if first statement is false and second statement is true')
} else {
  console.log('Will print this string if both statements are false');
}
```
- if both statements are true, it will only print the first statement because it evaluates conditional from top to bottom
- === to check if variable equals a certain string
- Can alternatively use switch statement
```[js}
switch (colorMode) {
    case "solarized":
        console.log('solarized mode set!'); 
        document.body.style.background = 'palegoldenrod';
        break;
    case "dark":
        console.log('dark mode set!');  
        document.body.style.background = 'black';
        break;
    default:  
        console.log('light mode set!');
        document.body.style.background = 'ghostwhite';
}
```
- Note the use of default as the else statement
- Note break; in order to only apply a single case
### Types
- Different data types:
  1. Primitive
    - string
    - number
    - boolean
    - undefinied
    - null
    - symbol
   2. Object
- Can use typeof to check data type
- Data conversion:
  1. Explicit
```
Boolean(message)
String(message)
```
  2. Implicit (coercion)
    - '1' * '2' = 2 - implicitly converts to numbers
    - '10' + 20 = 1020 - here the string takes precedence 
    - Conditionals will try to implicitly convert to boolean
    
- false, 0, '', null, undefined, NaN are the only 6 falsy values 

Some rules for conditionals:
 1. Avoid direct comparisons
 2. Use triple equals === (strict equals operator)
   -  Double equals == (loose equals operator) will convert types
 3. Convert to real Boolean values where need

Turnary operators
```js
const isAuthenticated = true;
const cartItemCount = isAuthenticated ? 1 : 0;
```
- Most useful if not performing an action
- Can chain multiple turnaries, but should avoid due to readability
```js
const greeting = age < 10 ? "Hey there" : age > 18 ? "Greetings" : age > 10 ? "What's up?" : "That's an interesting age!";
console.log(greeting); 
```

Short Circuiting
- || or logical operator
- && and logical operator
- Cutting down our conditionals by using these operators
- Can use () parenthesis to change order of operations

### Functions
- Process that takes an input and produces some kind of output:
 - Performs an action
 - Returns some data
```js
function echo(input) {
  console.log(input)
}
echo(argument)
```
- Creating a function named echo
- Echo console logs whatever the input is
- Lastly, we are calling echo on argument
- Variable created in functions are only scoped to within the function
- Can use return keyword to push result out of function scope, can save the output in a variable when calling the function

**Closure**
- An inner function that is inside its outer function's scope and has access to its variables
- Can keep the variable alive, and closure over the initialization of the variable, for example:
```js
function handleLikePost(step) {
  let likeCount = 0;
  return function addLike() {
    likeCount += step;    
    return likeCount;
  }
  addLike();
  console.log('like count:', likeCount);
}

const doubleLike = handleLikePost(2);

console.log(doubleLike());
console.log(doubleLike());
console.log(doubleLike());
```
- Rules for closures:
  1. Closures are a property of JS functions
  2. Call function in different scope than where function was originally defined
- Can control num of decimal places by added it as a new argument
- Can set a default value like so:
```js
function convertTemperature(celsius, decimalPlaces = 1) {
  const fahrenheit = celsius * 1.8 + 32;
  return Number(fahrenheit.toFixed(decimalPlaces));
}
```
- Above we are providing the default value of 1 for decimalPlaces, should there be no argument

**Arrow Functions**
- Uses the fat arrow syntax =>
- More consise way to create functions, helps with working objects or classes
- They are all anonymous
- Don't need parentheses if there is only one argument
- Implicit return, don't need explicit return keyword
```js
const username = 'john';
const capitalize = name => `${name.charAt(0).toUpperCase()}${name.slice(1)}`;
```
- Can be passed to other functions, like so:
```js
const countdown = (startingNumber, step) => {
  let countFromNum = startingNumber + step;
  return () => countFromNum -= step;
}

const countingDown = countdown(20, 2);
```
**Partially Applied Functions**
- Reduces the total number of arguments for a function
- Locks initial data in place through a closure
```js
function getData(baseUrl) {
  return function(route) { 
    return function(callback) {    
      fetch(`${baseUrl}${route}`)
        .then(response => response.json())
        .then(data => callback(data));  
    }     
  }  
}

const getSocialMediaData = getData('https://jsonplaceholder.typicode.com');

const getSocialMediaPosts = getSocialMediaData('/posts');
const getSocialMediaComments = getSocialMediaData('/comments');

getSocialMediaPosts(posts => {
  posts.forEach(post => console.log(post.title));  
});
// converted to arrow functions
const getData = baseUrl => route => callback =>  
      fetch(`${baseUrl}${route}`)
        .then(response => response.json())
        .then(data => callback(data));
```
- Since functions are actions, name them using verbs
- eg. function updateTodo() {} function checkCompleteTodo() {}
- Use consistent naming conventions throughout

### Objects
- Stored in unchangeing key: 'value'
- Allows us to manage and organize multiple pieces of data
- All keys are strings
- Object creation:
```js
const objectName = {
  key: 'value',
  key2: {
    nestedKey: 'value'
    },
  sayHi() {
    console.log('hi')
  }
};
objectName.methodName();
```
**Primatives vs Object Types**
- Primatives are the same as long as their values are the same
- 42 = variable1 === variable2 = 42, true
- This is not the case for objects, each has a totally unique value even if their contents is the same
- Another way to say this is that objects are reference types
- Manipulating objects
```js
object.newKey = "value"
object['new key'] = "value"
// Alternative notation, allows for spaces in keys or to use variables in key, can also do directly during object creation
const newKey = 'new key';
const value = 'value';
const object = {[newKey]: value};
// For deletion
delete object['new key']
delete object.newKey
```
- Object destructuring allows us to pluck off the attributes we want from an object
```js
const user = {
  name: "Reed",
  username: "Reedbarger",
  email: "reed@gmail.com",
  details: {
    title: "Programmer"  
  }  
};

const { username, details: { title } } = user; 
// variable name matches the key name, username and title, nested notation allowed

function displayUser() {
  console.log(`username: ${username}, job: ${title}`);  
}

displayUser()
```
**Assigning bulk data**
- Object.assign({}, originalObject, newObject);
- Remember to use empty object, otherwise you will mutate the originalObject
- This way we can pass the data from newObject, into a newerObject, with the attributes of the originalObject
- Alternatively const newerObject = { ...originalObject, ...newObject, addedKey: 'value' }
- This ... is known as the spread operator, generally more straightforward than Object.assign
- Order matters in both cases

### Maps
- Like objects+
- Main benefit that we don't need keys to be strings
- Created by
```js
const map1 = new Map([
  [1, 1],
  [true, true],
]);
// Mutate map
map1.set('key', 'value');
[...map1.keys()] // [1, true, 'key']
// Iterate over ordered maps
map1.forEach((value,key) => {
  console.log(key, value);
});
```
- Maps order matters
- WeakMap, use for situations where it is easily sent to garbage
- .size can easily check size of maps
- this keyword, don't have to use variable name, dynamic
  - Determined how function is called
  - Arrow functions can be used to set this to the surrounding scope

### Arrays
- More flexibility than objects, when orders are important
- Created w/ [], index notes position in array
- array.push(obj1, obj2) - adds to end of array
  - array.unshift() - adds to the front of an array 
  - array.concat() - creates a new array and adds to end 
- array.length - check size of array
- array.pop() - removes last obj of array
- array.indexOf(value) - to search an array for a certain value and provide an index reference
  - array.findIndex(idea => idea === 'value')
- array.includes(value) - returns true/false for whether value is in the array, but only works for primative values
- array.some(() => ) - just one element needs to match the condition
- array.every() - if every element matches to match the condition
- array.map() - transforms entire array, but creates a new array, can use to transform existing values or add new ones
- array.forEach() - transforms existing array
- Methods can be chained
- array.filter() - searches within an array and creates a new array with the results, but if none match, creates empty array
- array.find() - searches array for just one result
- array.reduce((accumulator, value) => callback function, value of accumulator) 
  - transforms an array into any data type, remembers the value of the accumulator
  - almost every array method is a specific instance of reduce
- newArray = [...oldArray, 'other values'] - creates a new array with oldArray values, can add other values
- array.slice(starting index, ending index)
- const [first, second, third] = array
  - const [first, ...rest] = array
**Converting objects to arrays**
- Object.keys(object) - returns all the keys
- Object.values() - returns all the values
  - const values = Object.keys(object).map(key => object[key]) 
- Object.entries - returns an array of arrays, [key, value] in each nested array
```js
const users = {
  '2345234': {
    name: "John",
    age: 29 
  },
  '8798129': {
    name: "Jane",
    age: 42
  },
  '1092384': {
    name: "Fred",
    age: 17 
  }
};

const usersOver20 = Object.entries(users).reduce((acc, [id, user]) => {
  if (user.age > 20) {
    acc.push({ ...user, id });
  }  
  return acc;
}, []);
console.log(usersOver20); 
// returns [{name: "John", age: 29, id: "2345234"}, {name: "Jane", age: 42, id: "8798129"}]
```
**Sets**
- Set is a special data structure that forces uniqueness
- set.size - gives set size
- const newArray = [...new Set(oldArray)] - creates a newArray with unique values within oldArray

### Classes
**Constructor functions**
- Allows us to construct functions on demand, and add any methods we like
- Convention is to capitalize first letter of function
```js
function Student(id, name, subjects =[]) {
  this.id = id;
  this.name = name;
  this.subjects = subjects;  
}
// add methods using prototype keyword
Student.prototype.addSubject = function(subject) {
  this.subjects = {...this.subjects, subject]
}
Student.prototype.removeSubject = function(subject) {
    let index = this.subjects.findIndex(idea => idea === subject);
    this.subjects = [...this.subjects.slice(0, index), ...this.subjects.slice(index + 1)]
}
// call it to create new object
const student1 = new Student(1, 'Gerald')
// call method on student1
student1.addSubject('Math')
```
- Prototypical inheritance - each instantiated object (from constructor function) inherits from prototype
- Every object has prototype
- Don't change the Object constructor prototype
**Classes**
- classes are cleaner types of constructor functions
- class keyword
- class Class {add methods here}
```js
class Student {
  constructor(id, name, subjects = []) {
    this.id = id;
    this.name = name;
    this.subjects = subjects;      
  }   
    
  addSubject() {}  
}
```
- **Will** get an error if we forget new keyword
- Everything is currently public
- Can create new classes that copy features from other class through extend keyword, in conjunction with super();
- class newClass extends oldClass {}
- Add keyword get to turn method into a getter and then can use it syntactically like a property
- Setter can be done similarly, need to be paired with a getter
- Prefix with _ to create bridge property
```js
class Product {
  constructor(name, price, discountable) {
    this._name = name;
    this._price = price;
    this.discountable = discountable;
  }

  get price() {
    return this._price;
  }
  
  set price(price) {
    if (typeof price !== "number") {
      return this._price;
    } else {
      this._price = price; 
    }
  }
  
  get name() {
      return this._name;
  }
  
  set name(name) {
      if (typeof name !== 'string') {
          return this._name;
      } else {
          this._name = name;
      }
  }
}

const product1 = new Product("Coffee Maker", 99.95, false);
product1.price = 30;
product1.name = 'Whisk'
console.log(product1.name);
```
- Set the this context with .bind method
- Can add bind in the constructor
- Class fields proposal could change future syntax to rely on the () =>
### DOM
- Document Object Model - A way to connect JS to the HTML and CSS
- Turn HTML nodes into JS objects
- Can dynamically add static html
- To get a particular element, use getElementById() NB: IDs should be unique:
```js
const el = document.getElementById('home')
```
- To get the first element of a certain type, use querySelector();
```js
const link = document.querySelector('a');
```
- To get all the elements of a certain type, use querySelectorAll(). This creates a node list.
```js
const links = document.querySelectorAll('a');
```
- `forEach()` and `matches()` can be used to select a particular element from the node list: 
```js
links.forEach(link => {
  if (link.matches('a[href="/login"]')) {
    const loginLink = link;
  }
})
```
- getElementsByTagName can be used instead of querySelectorAll() to get all the elements of a certain type. This produces an HTMLCollection which cannot be iterated over with forEach().
```js
const divs = document.getElementsByTagName('div')
```
- Use createElement() to create an element:
```js
const newPost = document.createElement('div');
```
use innerHTML to modify an element's HTML:
```js
newPost.innerHTML = "<strong>This is a new post</strong>"
```
use append() and prepend() to add elements to the end or start of an HTML document respectively:
```js
document.body.append(newPost);

document.body.prepend(newPost);
```
To put an element anywhere else, first query for the element which is where you want to place the new element and then prepend() the new element to it:
```js
const post = document.querySelector('.post');

post.prepend(newPost);
```
- .style is used to modify and element's style
- Named in camelCase
- Style declarations must be declared as a string
- We listen for events in JS with addEventListener()
```js
const posts = document.querySelectorAll(".post");
posts.forEach(post => {  
  post.addEventListener('click', event => {
  //   console.log(event.target);  
    console.log('Do you want to edit this post?')
  });
}); 
/// Won't update with our new posts, instead can do the following:
document.body.addEventListener('click', event => {
  if (!event.target.closest('.post')) return;
  
  console.log('Do you want to edit this post?')  
})
``` 
- Events:
  - mouseover
  - mouseout
  - keyup
  - keydown
  - keypress
