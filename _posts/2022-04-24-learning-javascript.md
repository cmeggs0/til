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
```{js}
 var username;
```
- Creates variable username, default value is null
```{js}
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
```{js}
let username = "John Smith";
let message = "Hi" + username;
console.log(message);
```
- Prints HiJohn Smith
- Instead:
```{js}
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
```{js}
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
```{js}
const isAuthenticated = true;
const cartItemCount = isAuthenticated ? 1 : 0;
```
- Most useful if not performing an action
- Can chain multiple turnaries, but should avoid due to readability
```{js}
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
```{js}
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
```{js}
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
```{js}
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
```{js}
const username = 'john';
const capitalize = name => `${name.charAt(0).toUpperCase()}${name.slice(1)}`;
```
- Can be passed to other functions, like so:
```{js}
function greetUser(name, callback) {
  return callback(capitalize(name));  
}

const result = greetUser(username, name => `Hi there, ${name}!`);

console.log(result);
```
