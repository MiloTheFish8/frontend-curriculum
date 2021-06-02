# JavaScript
<details>
<summary>Fundamentals</summary>

- [Basic definitions](#basic-definitions)
- [Good practices](#good-practices)
- [Code quality](#code-quality)
- [Constants and variables](#constants-and-variables)
- [Expressions, Control structures and Operators](#expressions-control-structures-and-operators)

</details>

<details>
<summary>Data types and structures</summary>

- [Data types and structures](#data-types-and-structures)
- [Numbers](#numbers)
- [Strings](#strings)
- [Objects](#objects)
- [Iterables](#iterables)
- [Arrays](#iterables-arrays)
- [Arrays: Add or remove items](#arrays-add-or-remove-items)
- [Arrays: Iterate](#arrays-iterate)
- [Arrays: Search](#arrays-search)
- [Arrays: Transform](#arrays-transform)
- [Arrays: Implementing Stack and Queue](#arrays-implementing-stack-and-queue)
- [Sets and WeakSets](#iterables-sets-and-weaksets)
- [Maps and WeakMaps](#iterables-maps-and-weakmaps)

</details>

<details>
<summary>Functions</summary>

- [Functions](#functions)
- [Scope](#scope)

</details>

<details>
<summary>Prototypes and inheritance</summary>

- [Constructors and prototypes](#constructors-and-prototypes)
- [Classes](#classes)

</details>

<details>
<summary>Modules</summary>
  
- [Modules](#modules)

</details>

<details>
<summary>Browser</summary>

- [Window Object](#window-object)
- [DOM](#dom)
- [Events](#events)
- [Forms](#forms)
- [Working with data](#working-with-data)
- [Loading scripts to the page](#loading-scripts-to-the-page)
- [Location API](#location-api)
- [History API](#history-api)
- [Navigator API](#navigator-api)
- [Browser storage](#browser-storage)
- [Service Workers, Web Workers and Worklets](#service-workers-web-workers-and-worklets)

</details>

<details>
<summary>Asynchronous JS</summary>

- [Timers and intervals](#timers-and-intervals)
- [Asynchronous JavaScript](#asynchronous-javascript-http-requests)

</details>

<details>
<summary>Performance, security, advances concepts, other info</summary>

- [Meta-programming](#meta-programming)
- [Performance and optimizations](#performance-and-optimizations)
- [Security](#security)
- [Regular expressions](#regular-expressions) - refactor the questions
- [Deploying](#deploying)
- [Testing](#testing)
- [Debugging](#debugging)
- [Browser support](#browser-support) - refactor the questions
- [Tools and workflow](#tools-and-workflow) - refactor the questions
- [Libraries](#libraries) - refactor
- [Frameworks](#frameworks) - refactor
- [Resources](#resources) - refactor

</details>

## Basic definitions
<details>
<summary>What is API?</summary>

- API (Application Public Interface)
  - a set of available properties and methods to solve a particular task
  - frequent implementation - objects

</details>

<details>
<summary>What is a dynamically typed variable?</summary>

- can store any value at any time (even when reassigning)
```JavaScript
// types are not set explicitly
let a = 10;
a = 'text';
```

</details>

<details>
<summary>What are statements?</summary>

- syntax constructs and commands that perform actions
- can be separated with `;`
- usually written on separate lines
```JavaScript
console.log('Hello!');
```

</details>

<details>
<summary>What is operand?</summary>

- what operators are applied to: 5 * 2 there are two operands: the left operand is 5 and the right operand is 2 (sometimes called arguments instead of operands)

</details>

<details>
<summary>What are unary, binary and ternary operators?</summary>

- unary - single operand
- binary - has 2 operands
- ternary - has 3 operands

</details>

<details>
<summary>What does alert() do?</summary>

- shows a message

</details>

<details>
<summary>What does prompt() do?</summary>

- shows a message asking the user to input text
- returns the text or, if `Cancel` button or `Esc` is clicked, `null`
```JavaScript
// undefined in the input in IT
const name = prompt('What is your name?');
// for IE
const name = prompt('What is your name?', '');
// preset input (optional)
const name = prompt('What is your name?', 'Dia');
```

</details>

<details>
<summary>What does confirm() do?</summary>

- shows a message and waits for the user to press `OK` or `Cancel`
- returns `true` for `OK` and `false` for `Cancel`/`Esc`

</details>

## Good practices
<details>
<summary>What values is better to pass as arguments and why?</summary>

- don't pass the reference type, pass the id when possible (primitive value)

</details>

## Code quality
<details>
<summary>Where are semi-colons placed?</summary>

- Semi-colons `;` are placed after every expression except blocks of code `{}` (exceptions are objects and everything declared with `var`, `let` or `const`, basically variables)

</details>

## Constants and variables
<details>
<summary>What were the issues with var?</summary>

- bad practice (not allowed with `'use strict';`)
```JavaScript
// works without strict mode
name = 'Mary';
// converted into
var name = 'Mary';
```
- hoisting
- recreating
```JavaScript
var i = 21;
// ... some code here
var i = 45;
```
- function and global scope (but no block scope)
- reserved names usage (not allowed with `'use strict';`)
```JavaScript
var undefined = 67;
```

</details>

<details>
<summary>What are the differences between vars, lets and consts?</summary>

- `let`, `const` - no hoisting, no recreating, block scope, using reserved names is not allowed
```JavaScript
// not any const = constant
// declares a variable with immutable link
const element = document.querySelector('p');
const arr = [1, 2, 3, 4];
```

</details>

<details>
<summary>How to declare different types of immutable constants?</summary>

  <details>
  <summary>Primitive value</summary>

  - immutable (code agreement: protected, hardcoded) constant primitive value (physical constants, coefficients, etc)
  ```JavaScript
  const LIGHT_SPEED = 255792458;
  ```

  </details>
  
  <details>
  <summary>Immutable constant array</summary>

  ```JavaScript
  const DEFAULT_NAMES = ['Michael', 'Anna', 'Chris'];
  ```

  </details>

  <details>
  <summary>Enumeration</summary>

  - enumeration (immutable constant) is a complete list of constants grouped by some sign
  ```JavaScript
  const Code = {
    SUCCESS: 200,
    CACHED: 302,
    NOT_FOUND: 404,
    SERVER_ERROR: 500
  };
  ```

  </details>

  <details>
  <summary>Immutable constant object</summary>

  ```JavaScript
  const Earth = {
    RADIUS: 6.371,
    GRAVITATION: 6.67408
  };
  ```

  </details>

</details>

<details>
<summary>Learn more</summary>

- [Let on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [Const on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

</details>

## Expressions, Control structures and Operators
<details>
<summary>What are the basic math operators?</summary>

- `=`
 ```JavaScript
// assignment returns a value
// x = value writes the value into x and then returns it
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);

console.log(a); // 3
console.log(c); // 0

// chaining assignment
// evaluate from right to left
// 1. the rightmost expression 2 + 2 is evaluated 
// 2. and then assigned to the variables on the left: c, b and a
let a, b, c;

a = b = c = 2 + 2;
console.log(a); // => 4
console.log(b); // => 4
console.log(c); // => 4
 ```
- `+` or `+=`
- `-` or `-=`
- `*` or `*=`
- `/` or `/=`
- `%`
- `**` exponentiation operator (not supported in IE)
```JavaScript
console.log(2 ** 2); // => 4 (2 pow 2)
console.log(4 ** (1 / 2)); // => square root
console.log(8 ** (1 / 3)); // => cubic root
```

</details>

<details>
<summary>How increment and decrement operators can be applied?</summary>

- only to variables, `5++` will cause an error

</details>

<details>
<summary>What is the difference between postfix and prefix increment and decrement?</summary>

- `return result++;` returns first the result and then increments
- `return --result;` decrements and then returns the changed value
```JavaScript
let initialNumber = 1;
let counter = initialNumber++;
let counter2 = ++initialNumber;
console.log(counter); // => 1
console.log(counter2); // => 2
```

</details>

<details>
<summary>How to use increment and decrement inside the expression?</summary>

```JavaScript
let counter = 1;
console.log(2 * ++counter); // => 4

let counter = 1;
console.log(2 * counter++); // => 2
// if you need multiply and then increase, more readable
console.log(2 * counter);
counter++;
```

</details>

<details>
<summary>What are bitwise operators?</summary>

- treat arguments as 32-bit integer numbers and work on the level of their binary representation
- used very rarely, when we need to fiddle with numbers on the very lowest (bitwise) level
- in some special areas, such as cryptography, they are useful
- AND `&`
- OR `|`
- XOR `^`
- NOT `~`
- LEFT SHIFT `<<`
- RIGHT SHIFT `>>`
- ZERO-FILL RIGHT SHIFT `>>>`

</details>

<details>
<summary>What does comma operator do?</summary>

- allows to evaluate several expressions, dividing them with `,`
- each of them is evaluated but only the result of the last one is returned
```JavaScript
// the first expression 1 + 2 is evaluated and its result is thrown away
// then, 3 + 4 is evaluated and returned as the result
let a = (1 + 2, 3 + 4);
console.log(a); // => 7

// comma operator has very low precedence, lower than =
// so parentheses are important in the example above
// evaluates + first, summing the numbers into b = 3, 7
// then the assignment operator assigns b = 3
// and the rest is ignored
let b = 1 + 2, 3 + 4;
console.log(b); // => 3

// why do we need an operator that throws away everything except the last expr?
// sometimes it is used to put several actions in one line
for (a = 1, b = 2, c = a * b; a < 10; a++) {}
```

</details>

<details>
<summary>What is the difference between `if ... else` and ternary operator?</summary>

- `if ... else` - returns no value
- `? :` - always returns a value

</details>

<details>
<summary>How to use `switch` operator and how does it compare?</summary>

- always uses `===` to compare
```JavaScript
switch (+expression) {
  case value + 1: 
    console.log(value);
    break;
  // grouping cases
  case value2:
  case value3:
    console.log(value2, value3);
    break;
  default:
    // default is optional
    console.log('default');
}
```

</details>

<details>
<summary>What are the 'falsy' values?</summary>

- `0`
- `''`
- `NaN`
- `null`
- `undefined`

</details>

<details>
<summary>What are the 'truthy' values?</summary>

- numbers `!== 0`
- not empty strings (even `'   '` and `'0'`)
- `[]`, `{}` and all other objects and arrays

</details>

<details>
<summary>What are the comparison operators?</summary>

- `==` and `===`
- `!=` and `!==`
- `>` and `<`
- `>=` and `<=`

</details>

<details>
<summary>How does JS compare strings?</summary>

```JavaScript
// JS compares strings based on standard lexicographical ordering (Unicode)
console.log('b' > 'a'); // => true

// JS always looks at the first char and only considers other chars if the 1st
// chars are the same
console.log('ab' > 'aa'); // => true

// uppercase chars are smaller than lowercase
console.log('a' > 'B'); // => true
```

</details>

<details>
<summary>How does JS compare different types (except === and !==)?</summary>

- converts the values to numbers
```JavaScript
console.log('3' > 1); // true
console.log('04' == 4); // true
console.log(true == 1); // true
console.log(false == 0); // true

// the strange thing because of this conversion
const a = 0;
const b = '0';

console.log(Boolean(a)); // false
console.log(Boolean(b)); // true
console.log(a == b); // true
```

</details>

<details>
<summary>How does JS compare with === and !==?</summary>

- compares without type conversion
```JavaScript
console.log(0 === false); // false
```

</details>

<details>
<summary>How to compare with null or undefined?</summary>

```JavaScript
console.log(null === undefined); // false
// special rule for == equal to each other but not to any other value
console.log(null == undefined); // true
// for other math and comparison operator
// null => 0
// undefined => null

// null vs 0 works strange
console.log(null > 0); // false
console.log(null == 0); // false
console.log(null >= 0); // true

// undefined shouldn't be compared to other values
// converted to NaN which returns false for all comparisons
console.log(undefined > 0); // false
console.log(undefined < 0); // false
console.log(undefined == 0); // false
```

</details>

<details>
<summary>What are logical operators?</summary>

- `||` or
- `&&` and
- `!` not (precedence is the highest of all logical)
- `??` nullish coalescing
- can be applied to values of any type
- the result can be of any type

</details>

<details>
<summary>What is `not` operator and how to convert into boolean?</summary>

- `!`
- `!!userName` converts into a boolean

</details>

<details>
<summary>How to use OR and AND, which one is higher?</summary>

- `a && b` if both are true
- `a || b` if at least one is true
- `&&` precedence is higher than `||`
- do not convert value into a boolean
```JavaScript
// returns the 1st falsy value
const userName1 = null && 'Mary'; // => null
// use value if the condition is true
const isLoggedIn = true; // if false => false
const userName0 = isLoggedIn && 'Mary'; // => 'Mary'
// if all are truthy, the last one is returned
const userName2 = 'Lily' && 'Max' && 'Mary'; // => 'Mary'
```
```JavaScript
// default value assignment
// getting the first truthy value from a list of variables or expressions
// returns 1st truthy value
const userName1 = '' || 'Mary' || 'Maya'; // => 'Mary'
const userName2 = 'Max' || 'Mary' || ''; // => 'Max'
// if all falsy, the last value is returned
const userName3 = null || 0 || ''; // => ''

// short-circuit evaluation
true || console.log('Will not be logged!');
false || console.log('Logged!');
```

</details>

<details>
<summary>How does nullish coalescing work and the cases?</summary>

- to provide a default value
```JavaScript
// returns the first argument if it's not `null` or `undefined`
// otherwise the second
const result = user ?? 'Unknown';
// is the same
const result = (user !== null && user !== undefined) ? user : 'Unknown';
// can be used in a sequence
const first = null;
const second = null;
const third = 'Third';
console.log(first ?? second ?? third ?? 'Unknown'); // => Third
// is the same (but for all falsy values)
console.log(first || second || third || 'Unknown');
```

</details>

<details>
<summary>How to use `??` with `&&` or `||`?</summary>

- due to safety reasons, JS forbids using `??` with `&&` and `||` operators unless the precedence is explicitly specified with `()`
```JavaScript
// Syntax error
let text = 'one' && 'two' ?? 'three';
// Works just fine
let text = ('one' && 'two') ?? 'three';
```

</details>

<details>
<summary>How to check if the value is `NaN`?</summary>

- `isNaN()` to check if NaN or not
- `isNaN(value) || value <= 0` if the first part is `true`, JS doesn't go further

</details>

<details>
<summary>How to use destructuring with iterables?</summary>

- for iterable structures only (doesn't work on strings!)
- works like `for ... of`
- all the elements go in an order, can't address the last one
```JavaScript
const numbers = [1, 2, 3, 4, 5];
// before 
const first = numbers[0];
const third = numbers[2];
// with destructuring
const [first, , third] = numbers;
// can use any 'assignables'
const user = {};
const [user.firstName, user.lastName] = numbers;
// when there is no value, can use defaults
const [first, , , , , sixth = 45] = numbers;
// when we want specific values and an array of the rest
const [first, ...otherNumbers] = numbers;
// good for swapping the values
let first = 'Harry';
let second = 'Ron';
[first, second] = [second, first];
// can destruct the function result
const [first, , third] = getNumbers();
// or function parameters
const printValues = ([first = 4, , third = 7]) => {
  console.log(`${first} ${third}`);
};
printValues(document.querySelectorAll('li'));
printValues([1, 2]);
printValues([]);
printValues(); // error: undefined is not iterable
```

</details>

<details>
<summary>How to use destructuring with Object?</summary>

```JavaScript
const cat = {
  name: 'Mini',
  location: 'London',
  color: 'Auburn',
  address: {
    street: 'Some street'
  },
  'home city': 'London'
};
// propOfAnObject: varName = default
// what : goes where
const {name: catName, color: catColor = 'White'} = cat;
// with folded objects
// no const for address, only for the content
const {address: {street: catStreet}} = cat;
// for combined prop use quotes
const {'home city': catCity} = cat;
// creates name and object of remained properties
const {name, ...otherProperties} = cat;

// great to use for DOM nodes
const elements = document.querySelectorAll('li');
for (let i = 0; i < elements.length; i++) {
  const {textContent: text} = elements[i];
  console.log(text);
}

// can combine [] and {} destructuring
const [, {textContent: text}] = document.querySelectorAll('li');
```

</details>

<details>
<summary>What if we try to use destructuring without creating a variable at the same time?</summary>

```JavaScript
let one, two, three;
// error (JS treats {} as a code block)
{one, two, tree} = {one: 1, two: 2, three: 3};
// will work if wrapped in ()
({one, two, tree} = {one: 1, two: 2, three: 3});
```

</details>

<details>
<summary>What is better: loop or recursion?</summary>

- in most cases loop is more efficient than a recursion (call stack overflow)
- any recursion could be rewritten into a loop

</details>

<details>
<summary>What are the general loops?</summary>

- `for (let i = 0; i < 5; i++) {}`
- `for (const item of items) {}`
  - almost the same as `for` loop
  - can use `break` and `continue`
  - could be used with every iterable (not only `Array`)
- `for (const key in someObject) {}`
  - requires additional check, otherwise can go through the whole prototype chain
- `while (isEdit) {}` as long as the condition is true
- `do { ... } while (isEdit);` runs at least once

</details>

<details>
<summary>What do `break` and `continue` do?</summary>

- `break;` stops the loop execution
  - if inside the nested loop - stops only the nested one, outer continues
- `continue;` skips only the current iteration and moves to the next

</details>

<details>
<summary>How and why to use a labeled statement?</summary>

- labeled statements could be used with any expression but mostly used with loops
- to break or continue the outer loop from inner
```JavaScript
outerLoop: for (const item of items) {
  console.log('Outer', item);

  innerLoop: for (let i = 0; i < 5; i++) {
    if (i === 2) {
      break outerLoop;
      // or
      continue outerLoop;
    }

    console.log('Inner', i);
  }
}

// could also break from somewhere else in the code
const button = document.querySelector('.button');

button.addEventListener('click', () => {
  break outerLoop;
  // or
  continue outerLoop;
});
```

</details>

<details>
<summary>How to use rest and spread operators?</summary>

- rest collects several values into one iterable structure
- rest must be last parameter in the function (or error)
```JavaScript
// before
function doSomething() {
  return Array.from(arguments);
}
// with rest
const doSomething = (...values) => {
  return values;
};
// destructuring + rest = first and an array of others
const [first, ...others] = doSomething();
```

```JavaScript
// spread - any iterable into separate values
// before
const values = [1, 2, 40, 73, 5];
// find max
Math.max.apply(null, values);
// merge arrays
const newValues = [];
newValues.concat(values);

// with spread
// find max
Math.max(...values);
// merge arrays
const newValues = [...values];
const filteredValues = [...values].filter();
```

</details>

<details>
<summary>What can be used with the `throw` operator?</summary>

- `throw { message: 'some message' };` can throw anything as an error, not only `new Error()`

</details>

<details>
<summary>When is it good to use `try catch finally`?</summary>

- use `try {} catch (error) {}` only for the code you can't control (ex: server errors, user input)

</details>

<details>
<summary>In what variations can we use `try catch finally`?</summary>

- `try ... catch` or `try ... finally` but never `catch ... finally`

</details>

<details>
<summary>When does `catch` get executed?</summary>

- if `try` doesn't throw an error, `catch` won't be executed

</details>

<details>
<summary>Why to use and when does `finally` run?</summary>

- when we want to throw the error from inside the `catch` block to send to some statistics etc
- some cleanup work (release data, clear the variables, etc)
- if the error is thrown from `catch`, only finally executes, code after `try ... catch ... finally` block won't be executed
- `finally` always runs

</details>

<details>
<summary>How does `try catch finally` work in details?</summary>

```JavaScript
function doSomething() {
  try {
    console.log(0); // => 0
    throw 'error ocurred';
  } catch(error) {
    // error => 'error ocurred' (what was used with 'throw')
    console.log(1); // => 1
    // this return statement is suspended till finally block completes
    return true;
    // not reachable
    console.log(2);
  } finally {
    console.log(3); // => 3
    // overwrites the return from catch block
    // function returns this value
    return false;
    // not reachable
    console.log(4);
  }
  // the function returns false from finally block
  // not reachable 
  console.log(5);
}

console.log(doSomething()); // => 0, 1, 3, false
```

</details>

<details>
<summary>Learn more</summary>

- [Operator precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
- [Control flow and error handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [Loops and iteration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [For ... of on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [Rest on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Spread on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Destructuring on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Bitwise on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#bitwise_operators)

</details>

## Data types and structures
<details>
<summary>What data types are available?</summary>

```JavaScript
// 1 - undefined
console.log(typeof undefined); // => undefined
// 2 - null
console.log(typeof null); // => object
// 3 - Boolean
console.log(typeof false); // => boolean
// 4 - Number
console.log(typeof 10); // => number
// 5 - String
console.log(typeof 'text'); // => string
// 6 - Symbol
console.log(typeof Symbol('sym')); // => symbol
// 7 - Object
// iterable lists: Array
// collections: NodeList, HTMLElementsList, classList, arguments
// iterable dictionaries: Map, WeakMap
// iterable sets: Set, WeakSet
// function is also an object, but of type function
console.log(typeof {}); // => object
console.log(typeof []); // => object
console.log(typeof function() {}); // => function
// 8 - BitInt
console.log(typeof 1n); // => bigint
console.log(typeof BigInt(9)); // => bigint
console.log(typeof BigInt('9')); // => bigint
```

</details>

<details>
<summary>What is a typeof operator and how to use it?</summary>
- returns the type of the argument

```JavaScript
typeof undefined; // => undefined
typeof(Symbol('id')); // => symbol
typeof Math; // object
```

</details>

<details>
<summary>How and why can we access methods of primitives?</summary>

- the main idea is to provide extra functionality but remain lightweight (that's why 'object wrappers' are used)
- JavaScript engines are well tuned to optimize that internally, so they are not expensive to call
```JavaScript
// str is a primitive
const str = 'Some text';
// in the moment of accessing its property, a special object is created
// that knows the value of the string, and has useful methods, like toUpperCase()
// that method runs and returns a new string (logged to console)
console.log(str.toUpperCase());
// the special object is destroyed, leaving the primitive str alone
```

</details>

<details>
<summary>Why is it unrecommended to use constructor function to create a primitive?</summary>

```JavaScript
// number
console.log(typeof 9);
// object
console.log(typeof new Number(9));

// objects are always truthy
// false
console.log(!!0);
// true
console.log(new Number(0));
```

</details>

<details>
<summary>Is it ok to use constructor functions for primitives (without new) to convert a value to the corresponding type?</summary>

```JavaScript
// it is totally normal to use those functions
const someNumber = Number('132');
```

</details>

<details>
<summary>Do null and undefined have any methods?</summary>

- special primitives `null` and `undefined` have no 'wrapper objects' and provide no methods (error when you try to access such method)

</details>

## Numbers
<details>
<summary>How are the numbers stored?</summary>

- every number is a float
- numbers are stored as 64-bit format IEEE-754 (double precision floating point numbers)

</details>

<details>
<summary>How to write a number?</summary>

```JavaScript
// the same number
const num = 1000000000;
const num2 = 1_000_000_000;
// 1 * 1000000000
const num3 = 1e9;

// the same small number
const num = 0.000001;
// 1 / 1000000
const num2 = 1e-6;
```

</details>

<details>
<summary>In what other bases can we write numbers and how?</summary>

```JavaScript
// hexadecimal (colors, encode characters, and many other things)
// prefix with 0x
// 255 (case doesn't matter)
console.log(0xff);
console.log(0xFF);
// binary 0b (255)
console.log(0b11111111);
// octal 0o (255)
console.log(0o377);
// true
console.log(0b11111111 == 0o377);
// for other systems parseInt is used
// works without prefix
parseInt('0xff', 16); // 255
parseInt('ff', 16); // 255
parseInt('2n9c', 36); // 123456
```

</details>

<details>
<summary>How do parseInt and parseFloat work?</summary>

```JavaScript
// read a number from a string till the not-number
console.log(+'100px'); // NaN
parseInt('100px'); // 100
parseInt('14.6'); // 14
parseFloat('15.5pt'); // 15.5
parseFloat('15.5.6'); // 15.5
```

</details>

<details>
<summary>What system JS uses to work with numbers?</summary>

- JS works with binary numbers and converts into decimal

</details>

<details>
<summary>What are the maximum and infinite numbers?</summary>

```JavaScript
// infinite number
1 / 0; // => Infinity
// max numbers
Number.MAX_SAFE_INTEGER; // 2^53 - 1
Number.MIN_SAFE_INTEGER; // -(2^53 - 1)
// floats
Number.MAX_VALUE;
// > or < calculations won't work, only display
// if we do such calculations, no errors
// but strange results because of binary system
```

</details>

<details>
<summary>What are the strange number cases and why do they occur?</summary>

- 
```JavaScript
// if a number is too big it would overflow the 64-bit storage
// potentially giving an infinity
// Infinity
console.log(1e500);

// because JS works with binary and converts into decimal
0.2 + 0.4 === 0.6; // => false (0.6000...1)
// something similar to 1/3 happens (0.33333(3))
(1).toString(2); // => 1
(5).toString(2); // => 101
(1/5).toString(2); // => 0.001100110011...
(0.2).toString(2); // => 0.001100110011...
0.2; // => 0.2
0.2.toFixed(20); // => 0.2000...1110

// there are 64 bits for the number, 52 of them can be used to store digits
// but that’s not enough so the least significant digits disappear
// no error, JS does its best to fit the number into the desired format
// but unfortunately, this format is not big enough
// => 10000000000000000
console.log(9999999999999999);

// two zeroes because a sign is represented by a single bit
// so it can be set or not set for any number including a zero
0;
-0;
// false
Object.is(0, -0);
```

</details>

<details>
<summary>How does BigInt work and when do we use it?</summary>

- to work with > max or < min numbers
- only integer, decimal => error
```JavaScript
// to create add n
9007199254740991985392n;
10n;
// can't mix with numbers
10n - 5; // => error
// but can use like this
10n - 5n; // => 5n
parseInt(10n) - 5; // => 5
10n - BigInt(5); // => 5n
// omits decimal
5n / 2n; // => 2n (not 2.5n)
```

</details>

<details>
<summary>How does toString() work with a number?</summary>

```JavaScript
// converts the number into a string
// with given base (from 2 to 36)
const num = 255;
// ff
console.log(num.toString(16));
// 11111111
console.log(num.toString(2));
// maximum (0...9, A...Z)
console.log(num.toString(36));
```

</details>

<details>
<summary>How to round a number to integer with Math?</summary>

```JavaScript
// down
Math.floor(3.1); // 3
Math.floor(-1.1); // -2
// up
Math.ceil(3.1); // 4
Math.ceil(-1.1); // -1
// nearest
Math.round(3.1); // 3
Math.round(3.5); // 4
// removes after . (IE not supported)
Math.trunc(3.1); // 3
```

</details>

<details>
<summary>How to create a random number?</summary>

```JavaScript
// number from 0 to 1 (included)
Math.random();
```

</details>

<details>
<summary>How to find min/max number?</summary>

```JavaScript
Math.max(2, 3, -19, 6, 10); // 10
Math.min(-14, 5, -6); // -14
```

</details>

<details>
<summary>How to raise a number into a given power?</summary>

```JavaScript
// with ** operator or with Math
Math.pow(2, 10); // 2 in power of 10 => 1024
```

</details>

<details>
<summary>How to round a number to decimal?</summary>

```JavaScript
// multiply and divide
// => 123.456 => 123 => 1.23
console.log(Math.round(1.23456 * 100) / 100);

// using toFixed(n) digits after the point
// returns a string (round up and down)
const num = 12.34;
console.log(num.toFixed(1)); // '12.3'
console.log(num.toFixed(5)); // '12.34000'
```

</details>

<details>
<summary>How to convert to a number?</summary>

```JavaScript
Number(undefined); // => NaN
Number(null); // => 0
Number(false); // => 0
Number(true); // => 1
Number('1'); // => 1
Number(' 1 '); // => 1
Number(' \t 1 \n '); // => 1
Number('1s'); // => NaN
// but parseInt/parseFloat work different
parseInt('100px'); // 100
parseFloat('1.5.5'); // 1.5
```

</details>

<details>
<summary>How to test for infinity and NaN?</summary>

```JavaScript
// both checks convert to a number
// true
console.log(isNaN(NaN));
console.log(isNaN('text'));
Object.is(NaN, NaN);
// false
console.log(NaN === NaN);
console.log(isNaN('15'));

// true if it's regular number (not NaN, Infinity. -Infinity)
console.log('15'); // => true
console.log('text'); // => false (NaN)
console.log(Infinity); // => false (NaN)
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Number on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)

</details>

## Strings
<details>
<summary>How to get the length of a string?</summary>

```JavaScript
const text = 'Hello\nWorld!';
// => 12 (\n counts as single special character)
console.log(text.length);
```

</details>

<details>
<summary>How to access the characters?</summary>

```JavaScript
const text = 'Hello';
// H
console.log(text[0]); // modern
console.log(text.charAt(0)); // old
// last character => 0
console.log(text[text.length - 1]);
// => undefined
console.log(text[10]);
// => ''
console.log(text.charAt(10));
```

</details>

<details>
<summary>How to iterate over a string?</summary>

- for pairs (like smiles) also works correct
```JavaScript
const text = 'Hello';

for (let char of text) {
  // => H => e => l => l => o
  console.log(char);
}
```

</details>

<details>
<summary>Are strings immutable and how to change the specific character?</summary>

```JavaScript
// strings are immutable, to change the char have to change the string
let text = 'Hello';
// => error
text[0] = 'h';
// replace the string
text = 'h' + text.slice(1);
```

</details>

<details>
<summary>How to change the case of only one character?</summary>

```JavaScript
const text = 'hello';
// => H
console.log(text[0].toUpperCase());
```

</details>

<details>
<summary>How to remove spaces from the beginning and the end of a string?</summary>

```JavaScript
str.trim();
```

</details>

<details>
<summary>How to repeat a string?</summary>

```JavaScript
str.repeat(2);
```

</details>

<details>
<summary>How to check if a string contains, starts, ends with some text?</summary>

```JavaScript
const playerName = 'Harry Potter';
// all are case sensitive
console.log(playerName.includes('rr')); // => true
console.log(playerName.includes('h')); // => false
console.log(playerName.includes('rr', 5)); // => false
// start (string, ?position)
console.log(playerName.startsWith('Ha')); // => true
console.log(playerName.startsWith('rr', 2)); // => true
console.log(playerName.startsWith('ha')); // => false
// end (string, ?length)
console.log(playerName.endsWith('er')); // => true
console.log(playerName.endsWith('tt')); // => false
console.log(playerName.endsWith('tt', 10)); // => true
```

</details>

<details>
<summary>How to get the index of the substring?</summary>

```JavaScript
const text = 'Widget with id';
// by default from 0 position
// as it's in the beginning => 0
console.log(text.indexOf('Widget'));
// case sensitive => -1
console.log(text.indexOf('widget'));
// from the given position => 12
console.log(text.indexOf('id', 3));
// or from the end => 12
console.log(text.lastIndexOf('id'));
// => 1
'canal'.lastIndexOf('a', 2);
// limits only the beginning of the match => 2
'abab'.lastIndexOf('ab', 2);
```

</details>

<details>
<summary>How to get all the indexes of the substring?</summary>

```JavaScript
const text = `As sly as a fox, as strong as an ox`;
const target = 'as';

let position = 0;

while (position !== -1) {
  position = text.indexOf(target, position);
  console.log(position);
  position++;
}
```

</details>

<details>
<summary>How to get a substring of a given position(s)?</summary>

```JavaScript
const text = 'sensitive';
// from till the end => ensitive
const str = text.slice(1);
// from to (not included) => ensi
const str1 = text.slice(1, 5);
// from the end => si
const str2 = text.slice(-6, -4);
// => ''
const str3 = text.slice(6, 2);

// between the given positions (greater one not included)
// => ensitive
const str = text.substring(1);
// from to (not included) => ensi
const str1 = text.substring(1, 5);
// negative are not supported (mean 0) => ''
const str2 = text.substring(-6, -4);
// => nsit
const str3 = text.substring(6, 2);

// some non-browser environments may not support this method
// but in practice works everywhere
// from the given position of the given length
// => ensitive
const str = text.substr(1);
// => ensit
const str1 = text.substr(1, 5);
// position from the end => siti
const str2 = text.substr(-6, 4);
```

</details>

<details>
<summary>How to shorten the -1 check (mostly in the old code)?</summary>

```JavaScript
// bitwise NOT operator ~ converts number to a 32-bit integer
// removes decimal part if exists
// and then reverses all bits in it's binary representation
// in practice: ~n === -(n + 1), so that ~-1 => -(-1 + 1) => 0
// but this method has a downside
// ~4294967295 === 0 so don't use for larger numbers
const text = 'Some text here';

if (~text.indexOf('text')) {
  console.log('Found!');
}
```

</details>

<details>
<summary>How to remove duplicates?</summary>

- easy way is to convert into an array and use `Set`

</details>

<details>
<summary>How are strings compared?</summary>

- in alphabetical order (UTF-16 codes)
- the lowercase letter is always `>` than the uppercase
- letters with diacritical marks are out of order (comes after letters and some symbols)
```JavaScript
// true
console.log('a' > 'Z');
console.log('Österreich' > 'Zealand');

// for correct comparison in different languages
// negative if str < (str2)
// positive if str > (str2)
// 0 if equal
console.log('Österreich'.localeCompare('Zealand')); // => -1
```

</details>

<details>
<summary>How to get the UTF-16 code of the letter and backwards?</summary>

```JavaScript
// code for the character at the given position
console.log('z'.codePointAt(0)); // => 122
console.log('Z'.codePointAt(0)); // => 90
// character from code
console.log(String.fromCodePoint(90)); // => Z
// 90 === 5a in hexadecimal system
console.log('\u005a'); // Z
```

</details>

<details>
<summary>What are paired letters?</summary>

- all frequently used characters have 2-byte codes (letters in most european languages, numbers, and even most hieroglyphs, have a 2-byte representation)
- 2 bytes only allow 65536 combinations and that’s not enough for every possible symbol
- rare symbols are encoded with a pair of 2-byte characters
```JavaScript
// the length of all those characters is 2
console.log('𝒳'.length);
console.log('😂'.length);
console.log('𩷶'.length);
// pairs did not exist at the time when JS was created
// thus are not correctly processed by the language
// String.fromCodePoint and str.codePointAt are new (work right)

// getting a symbol can be tricky, because pairs are treated as two chars
// strange symbols - pieces of the pair have no meaning without each other
// this actually displays garbage
console.log('𝒳'[0]);
console.log('𝒳'[1]);

// technically, pairs are also detectable by their codes
// code in the interval of 0xd800..0xdbff - first part of the pair
// next character (second part) must have the code in interval 0xdc00..0xdfff
// these intervals are reserved exclusively for pairs by the standard
console.log('𝒳'.charCodeAt(0).toString(16)); // d835 (between 0xd800 and 0xdbff)
console.log('𝒳'.charCodeAt(1).toString(16)); // dcb3, between 0xdc00 and 0xdfff

// can use conversion to and array or for...of loop to work with pairs
const text = '𝒳😂𩷶';
const letters = Array.from(text);
```

</details>

<details>
<summary>What are diacritical marks and normalization?</summary>

- symbols that are composed of the base char with a mark above or(and) under it (`a` and `àáâäãåā`)
- most common have their own UTF-16 code (but not all as there are too many combinations)
- there are UTF-16 codes to add (decorate) marks to a letter
```JavaScript
console.log('S\u0307'); // => Ṡ

const s1 = 'S\u0307\u0323'; // => Ṩ
const s2 = 'S\u0323\u0307'; // => Ṩ
// but there is a problem
console.log(s1 == s2); // => false
// unicode normalization => true
console.log('S\u0307\u0323'.normalize() == 'S\u0323\u0307'.normalize());
// brings to one character (but not always as Ṩ has own UTF-16 code)
console.log('S\u0307\u0323'.normalize().length); // => 1
console.log('S\u0307\u0323'.normalize() == '\u1e68'); // => true
```

</details>

## Objects
<details>
<summary>What data structures could be used as a key in an Object?</summary>

- strings
- numbers (positive int or floats)
- symbols

</details>

<details>
<summary>Is an Object iterable and how to iterate (not using keys/values/entries)?</summary>

- not iterable (can use `for ... in` old loop, has some issues, not `for ... of`)

</details>

<details>
<summary>How to use an Object as a dictionary (naming convention)? </summary>

```JavaScript
const filterValueToScale = {
  'smallest': 0.25,
  'small': 0.5,
  'normal': 1,
  'large': 2
};
```

</details>

<details>
<summary>How to create an Object (ES5, ES6 creation of the properties)?</summary>

```JavaScript
// ES5
// simple object
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// ES6+
// creation with variable
const name = 'Harry';
const user = {
  name,
  level: 1
};
// complex keys (could be useful for dictionaries)
const potter = 'Harry Potter';
const voldemort = 'Tom Riddle';
const antagonist = {
  [potter]: voldemort,
  ['Sirius Black']: 'Bellatrix Lestrange'
};
// new syntax for methods
const character = {
  go() {}
};
```

</details>

<details>
<summary>How the keys of an Object are ordered when logging?</summary>

```JavaScript
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

// collapsed = not all keys are numbers - not sorted
// collapsed = if all numbers - ascending
// expanded = always sorted, numbers first
console.log(person);
```

</details>

<details>
<summary>How to access the values in an Object?</summary>

```JavaScript
const person = {
  'short-name': 'Ron',
  age: 22,
  level: 3,
  3.2: 'some value',
  walk: function() {}
};

console.log(person.age);
console.log(person['short-name']);
console.log(person[3.2]);
console.log(person['3.2']);
```

</details>

<details>
<summary>What if we access the prop/method which doesn't exist in an object?</summary>

```JavaScript
const person = {
  name: 'Ron',
  age: 22,
  level: 3
};

// if no property or method => undefined (not an error)
console.log(person.hobbies);
```

</details>

<details>
<summary>What is optional chaining and why is it useful?</summary>

- to get `undefined` or `null` instead of error when accessing the properties of an object
```JavaScript
const user = {};
// fail with an error as we try to get the street of undefined
console.log(user.address.street);
// can be solved with &&
console.log(user.address && user.address.street && user.address.street.name);
// with optional chaining
// the variable must be declared
// otherwise ReferenceError: user is not defined
// stops if the value before ?. is undefined or null
// and returns undefined
console.log(user?.address?.street);
// don't overuse (it's only for optional properties)
// don't silence the errors
// if user supposed to be created and address is optional
console.log(user.address?.street);

// or with DOM elements when there is no element (returns null)
// error if it's null
const element = document.querySelector('.element').textContent;
```

</details>

<details>
<summary>How does optional chaining work with () and []?</summary>

```JavaScript
const user = {};
const player = {
  play() {}
};

// nothing happened
// the evaluation just stops, doesn't go to ()
user.play?.();
user['play']?.();
// calls the method
player.play?.();
player['play']?.();
```

</details>

<details>
<summary>Can we use an optional chaining to delete or create a new property?</summary>

- can be used for deleting but not for creating (error, because returns undefined and tries to assign the value to undefined)

</details>

<details>
<summary>What are the 'hint's to convert Object to primitive and how does the conversion work?</summary>

- not always return the hinted primitive (ex: for hint `"number"` can return a string)
- if the return value is not a primitive, it's just ignored (for historical reasons)
- `"string"` - an operation on the object that expects a string
- `"number"` - mostly maths operations
- `"default"` - rare cases when the operator is not sure what type to expect, for built-in objects usually handled the same as `"number"`
- there is no `"boolean"` as the Object is always `true`

</details>

<details>
<summary>What is the algorithm for converting an Object to primitive?</summary>

1. call `obj[Symbol.toPrimitive](hint)` if such method exists
2. otherwise if hint is `"string"` - try `obj.toString()` and `obj.valueOf()` whatever exists
3. otherwise if hint is `"number"` or `"default"` - try `obj.valueOf()` and `obj.toString()` whatever exists

</details>

<details>
<summary>How to use Symbol.toPrimitive?</summary>

```JavaScript
let user = {
  name: 'Harry',
  age: 30

  [Symbol.toPrimitive](hint) {
    // handles all conversion cases
    return hint === 'string' ? this.name : this.age;
  }
};

// string => Harry
console.log('' + user);
// number => 30
console.log(+user);
// default => 35
console.log(user + 5);
```

</details>

<details>
<summary>How to use toString and valueOf?</summary>

```JavaScript
// default implementation for an Object
const user = {
  name: 'Harry'
};
// [object Object]
console.log(user.toSting());
// object itself
console.log(user.valueOf() === user);

// can implement those methods
const player = {
  name: 'Harry',
  age: 30,
  // for "string" hint
  toString() {
    return this.name;
  },
  // "number" or "default"
  valueOf() {
    return this.age;
  }
};

// string => Harry
console.log('' + player);
// number => 30
console.log(+player);
// default => 35
console.log(player + 5);
```

</details>

<details>
<summary>How to add and use getters and setters?</summary>

```JavaScript
const character = {
  // creation of a property is not required (can be omitted)
  _level: 1,

  // can't use getter/setter + property
  // can't address itself = infinite cycle
  get level() {
    return this._level;
  },
  // always strictly 1 parameter
  set level(value) {
    if (value < 0) {
      this._level = this._level;
      // or set the default value
      // or throw an error
    }
    this._level = value;
  }
  // can create of some complex data
  get [`other ${this._level}`]() {
    return this._level;
  }
};

// addressing the getter or setter
// if there is only setter, can't access the value
const level = character.level;
character.level = 100;
```

</details>

<details>
<summary>How to iterate (entries, values, keys) over an Object?</summary>

- those methods ignore the symbolic properties as keys (like the `for ... in` loop)
```JavaScript
// ES5
// for ... in - deprecated (additional check)

// ES6
// for ... of works if using Symbol.iterator protocol
const player = {
  name: 'Harry',
  level: 10
};
// [['name', 'Harry'], ['level', 10]]
const playerEntries = Object.entries(player);
// ['Harry', 10]
const playerValues = Object.values(player);
// ['name', 'level']
const playerKeys = Object.keys(player);
```

</details>

<details>
<summary>How to transform/filter etc. objects?</summary>

- `Object.entries(obj)` to get an array
- use array method to do the required operation
- `Object.fromEntries(array)` to turn the resulting array back into an object

</details>

<details>
<summary>How to get all keys or only symbolic keys of an Object?</summary>

```JavaScript
// only symbolic
Object.getOwnPropertySymbols(obj);
// all keys
Reflect.ownKeys(obj);
```

</details>

<details>
<summary>How to add, modify, delete a property or a method of an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

player.age = 33;
player.level = 20;
delete player.name;
```

</details>

<details>
<summary>How to check if the property exists in an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

// but if the property = undefined, also returns false
const hasNameTricky = player.name !== undefined;
// true even if undefined
const hasName = 'name' in player;
// true even if undefined
const hasName2 = player.hasOwnProperty('name');
```

</details>

<details>
<summary>How to copy an Object?</summary>

- not a deep copy
```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

// {} - where
// player - what
const newPlayer = Object.assign({}, player);
// for several
const newPlayer = Object.assign({}, player, {options: 'code'});

// ES6
const newPlayer = {...player};
```

</details>

<details>
<summary>How to deep copy an object?</summary>

- copying deep - recursive with checking typeof function or object
  - lodash has deep copy
  - also there is a hack with `json.parse`, `json.stringify`

</details>

<details>
<summary>How to work with Object Descriptors?</summary>

```JavaScript
const character = {
  name: 'Harry',
  printName: function() {
    console.log(this.name);
  }
};

const descriptors = Object.getOwnPropertyDescriptors(character);
Object.defineProperty(character, 'name', {
  // defaults
  // can delete or define property
  configurable: true,
  // is accessible in for ... in loop
  enumerable: true,
  value: character.name,
  // can rewrite
  writable: true
});

// if writable === false
// no error but won't change, stays the same (Harry)
character.name = 'Ron';

// if configurable === false
// no error but won't delete, stays the same (Harry)
// can't reset configuration also, be careful
delete character.name;

// if enumerable === false
for (const key in character) {
  // will skip the name key, logs only printName
  console.log(key);
}
```

</details>

### What will be logged to the console?
```JavaScript
function createUser() {
  return {
    name: 'Harry',
    ref: this
  };
}

const user = createUser();

console.log(user.ref.name);
```

<details>
<summary>Answer</summary>

- `this` doesn't look at an object definition, only the moment of call matters
```JavaScript
// => Error: Cannot read property 'name' of undefined
console.log(user.ref.name);
// this will work
function createUser() {
  return {
    name: 'Harry',
    ref() {
      return this;
    }
  };
}

console.log(user.ref().name);
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [ES6 in Action: Enhanced Object Literals](https://www.sitepoint.com/es6-enhanced-object-literals/)
- [ ] [Objects on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects)
- [ ] [Object.create on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

</details>

## Iterables
<details>
<summary>What is an iterable (and examples)?</summary>

- objects that implement the 'iterable' protocol (have an `@@iterator` method (ex: `Symbol.iterator`))
- basically objects where you can use `for ... of` loop
- Array, NodeList, String, Map, Set, etc.

</details>

<details>
<summary>What is the difference between an iterable and an array-like?</summary>

- iterables are objects that implement the `Symbol.iterator` method
- array-like is an object that have indexes and length (looks like an array)
- an iterable may be not array-like and vice versa
- in JS there are iterables, array-likes or both (strings)
```JavaScript
// array-like
const arrayLike = {
  0: 'game',
  1: 'code',
  length: 2
};

// error (no Symbol.iterator)
for (let item of arrayLike) {}
```

</details>

<details>
<summary>What are the characteristics of an array?</summary>

- store data of any kind and length
- has many special methods
- order is guaranteed
- duplicates are allowed
- index-based access

</details>

<details>
<summary>What are the characteristics of a set?</summary>

- store data of any kind and length
- has own special methods
- order is not guaranteed
- duplicates are not allowed
- no index-based access

</details>

<details>
<summary>What are the characteristics of a map?</summary>

- store key-value data of any kind and length
- any key values are allowed
- has own special methods
- order is guaranteed (as the values were inserted)
- duplicate keys are not allowed
- key-based access

</details>

<details>
<summary>Learn more</summary>

- [7 Tips to Handle undefined in JavaScript](https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/)
- [Array vs Set vs Map vs Object — Real-time use cases in Javascript](https://codeburst.io/array-vs-set-vs-map-vs-object-real-time-use-cases-in-javascript-es6-47ee3295329b)
- [Iteration protocols on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)

</details>

## Iterables: Arrays
<details>
<summary>How to create an Array?</summary>

```JavaScript
// ES5
// 1
var numbers = new Array(3, 5); // => [3, 5]
// not === [undefined, undefined, undefined]
// has no indexes, only the length property
var emptyArray = new Array(3); // => [] with length === 3
// 2
var numbers2 = Array(3, 5);
var emptyArray2 = Array(3);
// 3
var letters = ['a', 'r']; // => ['a', 'r']
// 4 clones array and adds values from another array
const newNumbers = numbers.concat([8, 5, 2]);

// ES6+
// 5 makes an array of any iterable or array-like
// takes the object, examines for being an iterable or array-like
// makes a new array and copies items to it
// Array.from(iterable[, mapFunction, thisArg]);
const elements = Array.from(document.querySelectorAll('li'));
const letters = Array.from('string');
// [ss, ts, rs, ...]
const lettersWithS = Array.from('string', (l) => l + 's');
// 6 of separate values
const values = Array.of(1, 2, 3);
// 7
const items = [...elements, ...values];
```

</details>

<details>
<summary>How to fill an empty array (when created with length only)?</summary>

```JavaScript
const arr = new Array(5).fill();
// if used like this, calls the function only once
// and fills other items with the same value
const arr = new Array(5).fill(getTaskTemplate());
```

</details>

<details>
<summary>What if we leave some values empty in the middle?</summary>

```JavaScript
const numbers = [1, 2, 5];

// items in between will be empty of undefined value
numbers[5] = 23;
```

</details>

<details>
<summary>What are the ways to misuse an array? (bad for performance)</summary>

```JavaScript
// array optimizations stop working if we use an array like that
const arr = [];
// add a non-numeric property
arr.name = 'John';
// make holes
arr[0] = 8;
arr[990] = 10;
// fill the array in the reverse order
arr[1000] = 90;
arr[999] = 7;
```

</details>

<details>
<summary>What if we change the length property of an Array manually?</summary>

- if we increase it manually, nothing interesting happens
- if we decrease it, the array is truncated (irreversible)
```JavaScript
const arr = [1, 2, 3, 4, 5];
// => [1, 2]
arr.length = 2;
// => [1, 2, undefined]
arr.length = 3;
// the simplest way to clear the array
arr.length = 0;
```

</details>

<details>
<summary>How to fill an array with the same values?</summary>

```JavaScript
const arr = new Array(7);
// value, start, end
arr.fill('text'); // the whole array
arr.fill('text', 1, 3);
```

</details>

<details>
<summary>How to make an Array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
// also has the second arg - length (other items are ignored)
const words2 = text.split(' ', 2); // => ['One', 'two']
const symbols1 = Array.from(text); // => ['O', ..., ' ', 't', ...]
const symbols2 = [...text]; // => ['O', ..., ' ', 't', ...]
```

</details>

<details>
<summary>How to make a string of an Array?</summary>

```JavaScript
const words = ['one', 'two', 'three'];
// by default separates with ,
const text = words.join();
const text2 = words.join(' ');
```

</details>

<details>
<summary>How does conversion to a primitive work on an array?</summary>

```JavaScript
const arr = [1, 2, 3, 4];
console.log(String(arr) === '1,2,3,4'); // => true
// array doesn't have Symbol.toPrimitive or valueOf
// only toString that's why:
console.log([] + ''); // ''
console.log([] + 1); // '1'
console.log([1] + 1); // '11;
console.log([1, 2] + 1); // '1,21'
```

</details>

<details>
<summary>How to compare different arrays?</summary>

- don't use `==` to compare arrays (as well as `>`, `<` and others)
- two objects are equal `==` only if they’re references to the same object
- if one of the arguments of `==` is an object, and the other one is a primitive, then the object gets converted to primitive
- exception of `null` and `undefined` that equal `==` each other and nothing else
- <b>compare arrays item-by-item in a loop or using iteration methods</b>
```JavaScript
console.log([] == []); // => false
console.log([1] == [1]); // => false
// to primitive (to string as it has no other methods to convert to a primitive)
console.log(0 == []); // 0 == '' => 0 == 0 => true
console.log('0' == []); // '0' == '' => false
```

</details>

<details>
<summary>How to check if the data structure is an Array?</summary>

```JavaScript
console.log(Array.isArray([]));
```

</details>

<details>
<summary>How to pass `this` to be used inside the iterator function for some array methods?</summary>

```JavaScript
const arr = [1, 2, 3];
// but not with sort
arr.find(f, thisArg);
arr.filter(f, thisArg);
arr.map(f, thisArg);
// better to use an arrow function
arr.map(() => {});
```

</details>

## Arrays: Add or remove items

<details>
<summary>How to delete or add an element from (to) an Array at the start or the end?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// add/remove to the end/last of the array
const newNumbersLength = numbers.push(7, 9);
const newNumbersLength2 = numbers.push(...numbers);
const removedItem = numbers.pop();
// add/remove first, slower than push and pop
const newNumbersLength3 = numbers.unshift(9, 12, 15);
const newNumbersLength4 = numbers.unshift(...numbers);
const removedItem2 = numbers.shift();
```

</details>

<details>
<summary>How to delete or add an element from (to) an Array at any position?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// works but leaves an empty space
delete numbers[1]; // => [1, , 5]
// start index, delete count, value to add (or more 10, 15)
const removedElements = numbers.splice(1, 0, 10); // => [1, 10, 2, 5]
// removes from the end
const removedElements2 = numbers.splice(-1, 1); // => [1, 2]
// will delete all items starting with the provided index
const removedElements3 = numbers.splice(0);
```

</details>

<details>
<summary>How to copy an Array or a part of it?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// copy an array
const clonedNumbers = numbers.slice();
// copy starting from index till the end
const clonedNumbers2 = numbers.slice(2);
// end item not included
const clonedNumbers3 = numbers.slice(0, 2); // => [1, 2]
// [] if nothing is in between
const emptyNumbers = numbers.slice(3, 2);
const emptyNumbers2 = numbers.slice(-3, -4);
// from the end
const clonedPartOfNumbers = numbers.slice(-3, -1); // => [1, 2]
```

</details>

<details>
<summary>How to copy a whole Array and add new items?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// clones array and adds values from another array or just values
const newNumbers = numbers.concat([8, 5, 2]);
const newNumbers2 = numbers.concat([7, 8], [9, 10]);
const newNumbers3 = numbers.concat([7, 8], 9, 10);
const newNumbers3 = numbers.concat(7, 8, 9, 10);
// normally copies elements from arrays, not objects arrays-like
const arrLike = {
  0: 1,
  1: 2,
  length: 2
};
// => [1, 2, 5, {whole object}]
console.log(numbers.concat(arrLike));
// but with Symbol.isConcatSpreadable copies like an array
const arrLike = {
  0: 1,
  1: 2,
  [Symbol.isConcatSpreadable]: true,
  length: 2
};
// => [1, 2, 5, 1, 2]
console.log(numbers.concat(arrLike));
```

</details>

<details>
<summary>How to copy values in an array into itself?</summary>

```JavaScript
const arr = [1, 2, 3];
// target, start, end
arr.copyWithin(1, 0, 2);
```

</details>

<details>
<summary>How to create a flat array of a multidimensional array?</summary>

```JavaScript
// depth
const arrFlat = arr.flat(depth);
// function
const arrFlat2 = arr.flatMap(fn);
```

</details>

## Arrays: Iterate

<details>
<summary>What iteration method do we use to iterate over the whole Array and don't need to create something of the Array?</summary>

- doesn't change the initial array
```JavaScript
const numbers = [1, 2, 5];
numbers.forEach((item, index, array) => {});
```

</details>

## Arrays: Search
<details>
<summary>How to check if the Array includes some item?</summary>

```JavaScript
const numbers = [1, 2, 5, NaN];
// preferred over indexOf if we only need to check the inclusion
// the same numbers.indexOf(5) !== -1
// has the 2nd argument (from)
// uses === to compare
const isNumberInNumbers = numbers.includes(5);
// works correctly with NaN (unlike indexOf)
console.log(numbers.includes(NaN)); // => true
console.log(numbers.indexOf(NaN)); // -1
```

</details>

<details>
<summary>How to get the index of an item in an Array?</summary>

```JavaScript
// both methods have the 2nd argument (from)
// use === to compare
// if several same values => returns the index of the first
const index = numbers.indexOf(5);
// if several same values => returns the index of the last
const lastIndex = numbers.lastIndexOf(5);
```

</details>

<details>
<summary>How to find an item or an index in an Array?</summary>

```JavaScript
const numbers = [1, 2, 5];
// first element in the array or undefined => 2
const number = numbers.find((number, index, array) => {
  return number > 1;
});
// index of the first element or -1 => 1
const numberIndex = numbers.findIndex((number, index, array) => {
  return number > 1;
});
```

</details>

<details>
<summary>How to filter the items in an Array?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
// [] if nothing is found
const filteredNumbers = numbers.filter((item, idx, arr) => {});
```

</details>

<details>
<summary>How to remove all the falsy values from an array?</summary>

```JavaScript
const arr = [];
const noFalsyArr = arr.filter(Boolean);
```

</details>

<details>
<summary>How to check the array for some or every values?</summary>

```JavaScript
// if any results are true, immediately returns true and stops
// otherwise false (like ||)
const isInArray = arr.some((item) => item === 20);
// if all are true => true, if any false => false and stops
const checkArrEqual = (arr1, arr2) => {
  if (arr1.length !== arr2.length) {
    return false;
  }

  return arr1.every((item, index) => item === arr2[index]);
};
```

</details>

## Arrays: Transform
<details>
<summary>How to reverse items in an Array?</summary>

- changes the initial array
```JavaScript
const numbers = [1, 2, 5];
const reversedNumbers = numbers.reverse();
```

</details>

<details>
<summary>How to sort items in an Array?</summary>

- changes the initial array
```JavaScript
const numbers = [1, 2, 5];
// by default converts to a string and sorts characters
const sortedDefault = numbers.sort();
const sortedNumbers = numbers.sort((a, b) => {
  if (a > b) {
    // or any positive value
    return 1;
  } else if (a === b) {
    return 0;
  } else {
    // or any negative value
    return -1;
  }

  // or
  return a - b;
});
```

</details>

<details>
<summary>How to create a new changed Array based on the given Array?</summary>

- returns a new array
```JavaScript
const numbers = [1, 2, 5];
const newTransformedNumbers = numbers.map((item, ids, arr) => {});
```

</details>

<details>
<summary>How to get the single output value of an Array?</summary>

```JavaScript
const numbers = [1, 2, 5];

// if there is no initial value, takes the 1st item as accumulator
// and starts the loop from the 2nd (but if the arr is empty => error)
const sum = numbers.reduce((accumulator, number, index, numbers) => {
  return accumulator + number;
}, 0);

const sum2 = numbers.reduceRight((accumulator, number, index, numbers) => {
  return accumulator + number;
}, 0);
```

</details>

## Arrays: Implementing Stack and Queue
<details>
<summary>How and why to create a stack using an Array (LIFO)?</summary>

- for tasks, when we have to store previous item (history, browser history, games)
- also available to 'go forward' the history (have to store the removed action back to the stack)
```JavaScript
const questions = [{
  question: 'Which class has a different teacher every year?',
  answers: [{
    answer: 'Defence against the dark arts',
    isCorrect: true
  }, {
    answer: 'Potions',
    isCorrect: false
  }]
}, {
  question: 'What animal represents Hufflepuff house?',
  answers: [{
    answer: 'The Burrow',
    isCorrect: true
  }, {
    answer: 'The Fox',
    isCorrect: false
  }]
}];

const history = [];

const changeQuestion = (newQuestion) => {
  const oldQuestion = questions[0].question;

  questions[0].question = newQuestion;
  
  // store the action (function) and add to the history array
  // works because of closures
  history.push(() => questions[0].question = oldQuestion);
};

console.log(questions[0].question);
changeQuestion('What was the original question?');
console.log(questions[0].question);
changeQuestion('Who is Harry Potter?');
console.log(questions[0].question);

// to get back the stored value
history.pop()();
console.log(questions[0].question);
history.pop()();
console.log(questions[0].question);
```

</details>

<details>
<summary>How and why to create a queue using an Array (FIFO)?</summary>

- for tasks to be executed in a row after some async event
- for unique actions can use `Set` instead of `Array`
```JavaScript
const callbacks = [];

const addAsyncListener = (fn) => {
  // check if the callback exists (used before set was created)
  if (!callbacks.find((it) => it === fn)) {
    callbacks.push(fn);
  }
};

const startAsync = () => {
  setTimeout(() => {
    for (const cb of callbacks) {
      callbacks.delete(cb);
      cb();
    }

    console.log('Done');
  }, 500);
};

const log2 = () => console.log(2);

addAsyncListener(() => console.log(1));
addAsyncListener(log2);
addAsyncListener(log2); // won't be added to array
addAsyncListener(() => console.log(3));

console.log('Start!');
startAsync();

addAsyncListener(() => console.log(4));
addAsyncListener(() => console.log(5));

// the log will be: Start! 1 2 3 4 5 Done
```

</details>

<details>
<summary>Learn more</summary>

- [Array on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Which Array Function When?](https://dev.to/andrew565/which-array-function-when)
- [map() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [find() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [findIndex() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- [filter() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [reduce() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)
- [concat() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b)
- [slice() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- [splice() on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

</details>

## Iterables: Sets and WeakSets
<details>
<summary>How to create a Set and add items?</summary>

```JavaScript
const data = new Set();
// add items, returns the set itself, can chain
data.add(1);
// does nothing if value exists
data.add(1);

// based on array or any other iterable
const data = new Set([1, 4, 8]);
```

</details>

<details>
<summary>How to check if the item is in the Set?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// => true
console.log(data.has(1));
```

</details>

<details>
<summary>How to delete an item and what if there is no such item?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// => true
data.delete(1);
// => false
data.delete(15);
```

</details>

<details>
<summary>How to delete all the items from a Set?</summary>

```JavaScript
data.clear();
```

</details>

<details>
<summary>How to get the items count of a Set?</summary>

```JavaScript
data.size;
```

</details>

<details>
<summary>Is a Set an iterable and how to iterate?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
// iterable
for (const item of data) {
  // => 1 => 4 => 8
  console.log(item);
}
```

</details>

<details>
<summary>What are the entries, keys and values of a Set?</summary>

```JavaScript
const data = new Set([1, 4, 8]);
const entries = data.entries();

for (const entry of entries) {
  // => [1, 1] => [4, 4] => [8, 8]
  console.log(entry);
}
// those are the same (for compatibility with Map)
const values = data.values();
const keys = data.keys();
```

</details>

<details>
<summary>What is the difference between Object.entries(obj) and set.entries()?</summary>

- different syntax (for compatibility - created object may have it's custom `.values` method)
- `.entries()` returns an iterable, `Object.entries(obj)` returns an actual array

</details>

<details>
<summary>How to iterate over a Set with forEach?</summary>

```JavaScript
const data = new Set([1, 4, 8]);

data.forEach((value, valueSame, set) => {
  // => 1 => 4 => 8
  console.log(value);
});
```

</details>

<details>
<summary>What is a WeakSet and how is it different from a Set?</summary>

- less methods available
```JavaScript
const users = new WeakSet();
const john = {name: 'John'};
let harry = {name: 'Harry'};

// values must be objects, not primitives
users.add(john);
users.add(harry);
// Error: 'string' is not an object
users.add('string');

// object exists in the WeakSet while it is reachable from somewhere else
// doesn’t prevent garbage-collection of values
// will be removed from memory (and from the WeakSet)
// by garbage collector automatically
harry = null;

// less methods available
// doesn't support iteration
// has no .size .keys() .values() .entries()
users.has(john);
users.delete(john);
```

</details>

<details>
<summary>What are the use cases for a WeakSet?</summary>

- additional storage for yes/no facts (ex: if `.has()` returns `true` - user visited, if `false` - not)

</details>

<details>
<summary>Learn more</summary>

- [Set on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [WeakSet on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Weakset)

</details>

## Iterables: Maps and WeakMaps
<details>
<summary>Why a Map, not just an Object?</summary>

- any keys possible (even objects, if we use an object as a key in the Object, it would be converted to the string `[object Object]`)
- compares the keys `===` except `NaN` (here `NaN` is equal to `NaN` so that it could be used as a key)
- iterable
- pairs are objects
- better performance (than object) for large quantities of data
- better performance when adding / removing data frequently

</details>

<details>
<summary>How to create a Map and add items?</summary>

```JavaScript
const pairs = new Map();
// add items
pairs.set('John', 'May');
pairs.set('Ichigo', 'Rukiya');
// every .set call returns a map itself, so we can chain the calls
pairs.set('Mary', 'Kay').set('Lily', 'James');

// or with iterable
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
```

</details>

<details>
<summary>How to get the item from a Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

// get the value (undefined if no such key)
const pair = pairs.get('John');
```

</details>

<details>
<summary>How to check if the item is in the Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

// => true
console.log(pairs.has('John'));
// => false
console.log(pairs.has('Mary'));
```

</details>

<details>
<summary>How to remove an item from the Map?</summary>

```JavaScript
map.delete('key');
```

</details>

<details>
<summary>How to remove all the items from the Map?</summary>

```JavaScript
map.clear();
```

</details>

<details>
<summary>How to get the elements count in the Map?</summary>

```JavaScript
map.size;
```

</details>

<details>
<summary>Is a Map an iterable and how to iterate?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
// pairs.entries() is used by default
for (const pair of pairs) {
  console.log(pair); // => ['John', 'May'] => ['Ichigo', 'Rukiya']
}
```

</details>

<details>
<summary>What are the entries, keys, values of a Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

// entries
for (const entry of pairs.entries()) {
  console.log(entry); // => ['John', 'May'] => ['Ichigo', 'Rukiya']
}
for (const [key, value] of pairs.entries()) {
  console.log(key, value);
}

// keys
for (const key of pairs.keys()) {
  console.log(key);
}

// values
for (const value of pairs.values()) {
  console.log(value);
}
```

</details>

<details>
<summary>Is there a forEach method for Map?</summary>

```JavaScript
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);

pairs.forEach((value, key, map) => {
  // => 'John' - 'May' => 'Ichigo' - 'Rukiya'
  console.log(`${key} - ${value}`);
});
```

</details>

<details>
<summary>What is a WeakMap and how is it different from a Map?</summary>

```JavaScript
const users = new WeakMap();
const john = {name: 'John'}
let harry = {name: 'Harry'};

// keys must be objects, not primitives
users.set(john, 'Info');
users.set(harry, 'Some info');
// Error: 'string' is not an object
users.set('string', 'error');

// doesn’t prevent garbage-collection of key objects
// will be removed from memory (and from the WeakMap)
// by garbage collector automatically
harry = null;

// less methods available
// doesn't support iteration
// has no .size .keys() .values() .entries()
users.get(john);
users.delete(john);
users.has(john);
```

</details>

<details>
<summary>Why is there a limitation of the available methods in a WeakMap?</summary>

- for technical reasons: if a reference type has lost all other references, it is to be garbage-collected automatically, but technically it’s not exactly specified when the cleanup happens
- the JS engine decides that (immediately or waits and do it later when more deletions happen) 
- so, technically, the current element count of a WeakMap is not known (the engine may have cleaned it up or not, or did it partially) 
- so methods that access all keys/values are not supported

</details>

<details>
<summary>What are the use cases for a WeakMap?</summary>

- additional data storage (ex: user object as a key and visit counts as a value)
- caching (ex: store the results from a function so that future calls on the same object can reuse it)

</details>

<details>
<summary>How to convert an Object into a Map and back from a Map to an Object?</summary>

```JavaScript
const player = {
  name: 'Harry',
  level: 10
};

const playerMap = new Map(Object.entries(player));
const newPlayer = Object.fromEntries(playerMap.entries());
// also works
const newPlayer = Object.fromEntries(playerMap);
```

</details>

<details>
<summary>Learn more</summary>

- [Map on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [WeakMap on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

</details>

## Functions
<details>
<summary>What does function without `return` statement or with empty `return` return?</summary>

- function without `return` statement or with empty `return` returns `undefined`

</details>

<details>
<summary>How to use the return with a long expression?</summary>

```JavaScript
// not like this
// transfers into return;
return
  a + b;

// use ()
return (
  a + b
);
```

</details>

<details>
<summary>What is the difference between parameters and arguments?</summary>

- parameters are variables, which are specified when defining a function
```JavaScript
function printMsg(msg) {}
```
- arguments are the concrete values passed to a function when calling it
```JavaScript
printMsg('Some message');
```

</details>

<details>
<summary>What if the argument is not provided?</summary>

- its value becomes `undefined`

</details>

<details>
<summary>What will be the function name in the console error if thrown from an anonymous function?</summary>

- when there is an error inside the anonymous function, name of the function will be `<anonymous>`
```JavaScript
button.addEventListener('click', function() {});
```
- the only case why to add a name to anonymous function is for debugging, in that case the name of the function will be specified
```JavaScript
button.addEventListener('click', function onClick() {});
```

</details>

<details>
<summary>What are the default parameters of a function and how to use them?</summary>

```JavaScript
// ES5
var doSomething = function (caption, amount, isChecked) {
  if (typeof isChecked === 'undefined') {
    isChecked = false;
  }
};

// ES6
// even if we explicitly pass instead of isChecked undefined,
// the default value will be assigned
const doSomething = (caption, amount, isChecked = false) => {
  // some code here
};

// can also use the previous parameter in default value assignment
const doSomething = (amount, isChecked = amount > 5 ? true : false) => {};
```

</details>

<details>
<summary>How to set up the parameter validation with default parameters?</summary>

```JavaScript
const isRequired = () => {
  throw new Error('The parameter is required!');
};

const doSomething = (text = isRequired()) => {};
```

</details>

<details>
<summary>What are the differences between Function Declaration and Function Expression?</summary>

- the syntax is different
- declaration 'bubbles' (can be used before the declaration), expression is created when the execution flow reaches it
- in strict mode, when a declaration is within a code block, it's visible everywhere inside that block but not outside
```JavaScript
const age = 18;

if (age < 18) {
  function sayHello() {
    console.log('Hello!');
  }
} else {
  function sayHello() {
    console.log('Welcome!');
  }
}

sayHello(); // error (not defined)
```

</details>

<details>
<summary>What are the arrow functions and how do they differ from a normal function?</summary>

- doesn't have it's own scope (only lexical) - when global, `this === window`
- doesn't have `arguments` object
- can't rewrite `this` (`bind` and `call` won't work)
  - can't be used as a constructor, no `new` keyword
  - can't be method of an object or prototype

```JavaScript
// only 1 param?
const doSomething = param => console.log(param);

// only 1 expression?
// = return left * right;
const doSomething = (left, right) => left * right;

// return object?
const getWizard = (name, level) => ({
  name,
  level
});
```

</details>

<details>
<summary>What is the arguments keyword in a function?</summary>

- don't have to pass as a parameter (accessible as a keyword inside any function)
- iterable structure
- arrow functions do not have arguments keyword

</details>

<details>
<summary>What do bind, call, apply do and how are they different?</summary>

- `call` (values) and `apply` (array) call the function (as `()`)
- `bind` doesn't call the function
- the arguments passed after context are preset arguments, when the arguments are passed on function call, append to the end
```JavaScript
const addNumbers = (cb, ...numbers) => {
  // sum numbers
  let result = 100;

  cb(result);
};

const printResult = (text, result) => console.log(`${text} ${result}`);

addNumbers(printResult.bind(this, 'The sum is:'), 10, 90);
```
- more info in [scope](#scope) section

</details>

<details>
<summary>How to call a function with template literals (tagged templates)?</summary>

- with tagged template literals the value of the first argument is always an array of the string values, the remaining arguments are of the passed expressions
```JavaScript
const getPlayerInfo = (first, second, third) => {
  console.log(first); // ['', ' is ', ' for now']
  console.log(second); // 'Harry'
  console.log(third); // 10
};

const name = 'Harry';
const level = 10;

getPlayerInfo`${name} is ${level} for now`;
```

</details>

<details>
<summary>What are pure functions and the side effects?</summary>

- for the same input always give the same output
- no side effects
```JavaScript
// pure function
const addNumbers = (num1, num2) => {
  return num1 + num2;
};

// impure - output changes
const addRandomNumber = (num) => {
  return num + Math.random();
};

// impure - side effect
let result = 0;

const addNumber = (num) => {
  result += num;
  return result;
};

// impure - side effect
const books = ['If I Never Met You', 'Atomic Habits'];

const addBook = (book) => {
  books.push(book);
};
```

</details>

<details>
<summary>What are factory functions and why to use them?</summary>

- functions which create a function
- good for pre-configuring some values
```JavaScript
// for not to pass the tax rate all the time
const createCalculateTax = (tax) => {
  return (amount) => {
    return amount * tax;
  };
};

const calculateVatAmount = createCalculateTax(0.19);
const calculateIncomeTaxAmount = createCalculateTax(0.25);

console.log(calculateVatAmount(100));
console.log(calculateIncomeTaxAmount(100));
```

</details>

<details>
<summary>What are closures?</summary>

- all functions in JS are closures
- function locks in all surrounding variables
- mostly used for factory functions

</details>

<details>
<summary>What is a recursion and why to use it?</summary>

- sometimes it's shorter than other ways
- if too many calls => stack overflow
```JavaScript
const getPower = (a, n) => {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= a;
  }

  return result;
};

const getPowerRec = (a, n) => {
  // don't forget to add an exit condition
  if (n === 1) {
    return a;
  }

  return a * getPowerRec(a, n - 1);
};

// even shorter
const getPowerRec = (a, n) => {
  return n === 1 ? a : a * getPowerRec(a, n - 1);
};
```
- where do we need the recursion?
- when there are some nested objects but we don't know exactly how many
```JavaScript
const player = {
  name: 'Harry',
  teamMembers: [{
    name: 'Ron',
    teamMembers: [{
      name: 'Ginny'
    }]
  }, {
    name: 'Hermione',
    teamMembers: [{
      name: 'Luna',
      teamMembers: [{
        name: 'Mary'
      }]
    }]
  }, {
    name: 'Sirius'
  }, {
    name: 'Ellie'
  }]
};

const getTeamMemberNames = (player) => {
  const names = [];

  if (!player.teamMembers) {
    return [];
  }

  for (const teamMember of player.teamMembers) {
    names.push(teamMember.name);
    names.push(...getTeamMemberNames(teamMember));
  }

  return names;
};

console.log(getTeamMemberNames(player));
```

</details>

<details>
<summary>Learn more</summary>

- [Functions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [Bind on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
- [Closures on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [Recursion on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Recursion)
- [Tagged templates on  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates)
- [Arrow functions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Arrow function expressions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#No_binding_of_this)

</details>

## Scope
<details>
<summary>What is a scope and a context?</summary>

- scope is where the function runs
- context depends on how the function is called
- while the function is not called, it doesn't have any context
- context is being created upon the function call

</details>

<details>
<summary>What is `this` and how to change it?</summary>

- it is a context
- created upon the function call
- depends on how the function is called
- could be changed, also with `apply`, `call`, `bind`

</details>

<details>
<summary>How does `use strict` affect `this` keyword?</summary>

- no `use strict`, `this` = `window`, with `this` = `undefined` (for global this inside the function)
```JavaScript
const doWithoutStrict = function() {
  console.log(this);
};

const doWithStrict = function() {
  'use strict';
  console.log(this);
};

// => window
doWithoutStrict();
// => undefined
doWithStrict();
```

</details>

<details>
<summary>What is `this` inside an Object?</summary>

- in an object (method) `this` is the reference to the object itself (but remember, in depends on how the function is called)

</details>

<details>
<summary>What will be `this` in case of outer function (call on object and in global scope)?</summary>

```JavaScript
const greet = function() {
  console.log(`My name is ${this.firstName}`);
};

const player = {
  firstName: 'Ron',
  greet
};

// => My name is Ron
player.greet();
// => My name is undefined
greet();
```

</details>

<details>
<summary>What will be `this` if we use destructuring and call the function in the global scope?</summary>

```JavaScript
const player = {
  firstName: 'Harry',
  age: 28,
  run() {
    console.log(`${this.firstName} runs!`);
  }
};

const {run} = player;
// => undefined runs!
run();
```

</details>

<details>
<summary>What if we use closures inside the object method?</summary>

- with closure the result is more obvious
```JavaScript
const guitarPlayer = {
  firstName: 'Michael',
  lastName: 'Lantsov',
  play() {
    console.log(`${guitarPlayer.firstName} ${guitarPlayer.lastName}`);
  }
};

const anotherPlayer = {
  firstName: 'Anna',
  lastName: 'Starkov'
  play: guitarPlayer.play
};

// output will be the same
guitarPlayer.play();
anotherPlayer.play();
```

</details>

<details>
<summary>What is `this` in an instance of a class or when using a constructor function?</summary>

- `this` refers to current instance of an object in a `class`
- binds `this` in the constructor

</details>

<details>
<summary>What is the issue with using array methods inside the object methods and `this`?</summary>

```JavaScript
const players = {
  team: 'Griffindor',
  members: ['Harry', 'Ron', 'Hermione'],
  getMembers() {
    this.members.forEach(function(member) {
      // here this is created when the forEach calls it
      // it is called not on players object
      // so this here === global scope or undefined
      // could be solved with arrow function
      console.log(this);
    });
  }
};
```

</details>

<details>
<summary>How and why do we use `bind`, `call` and `apply`?</summary>

- `bind` creates a new function, the initial function stays the same
- `bind` context can't be changed even with `apply` and `call`
```JavaScript
// here `this === obj` instead of `a` (respects the first binding)
obj.getThis4 = obj.getThis2.bind(obj);
obj.getThis4.call(a);
```
- calling a function with bound context (1st param in those functions is always context, the 2nd parameter differs)
```JavaScript
// arguments separated with ',' will be function params
// perfect when there are not many params
play.call(anotherPlayer, '20.02.1967');
// array, which values will be function params
// good for many params or undefined number of params
play.apply(guitarPlayer, ['20.02.1967']);
```
```JavaScript
const numbers = [1, 3, 100, 5];

// we don't need context here, so pass 'null'
console.log(Math.max.apply(null, numbers));
```

</details>

<details>
<summary>What is the context inside the event listener?</summary>

- listener's context is always === the element, to which the listener is applied `document.body` or `evt.currentTarget` (the browser binds `this` (on event listeners) to the DOM element that triggered the event)
```JavaScript
// even in this case
const cart = {
  item: 'Book',
  price: 6,
  print() {
    console.log(`${this.item} \$${this.price}`)
  }
};

item.addEventListener('click', cart.print);
// browser will store the function
item.callback = cart.print;
// and executes the callback
// so just won't work (because it's not cart.callback(), but callback())
item.callback();
```
- can override if create the event handler and execute the method
```JavaScript
item.addEventListener('click', function() {
  cart.print();
});
```
- with bind (but careful, `bind` returns a new function, store first in a separate variable to unsubscribe if needed)
```JavaScript
// can't remove the listener
item.addEventListener('click', cart.print.bind(cart));

// to remove a listener
const printCart = cart.print.bind(cart);

item.addEventListener('click', printCart);
item.removeEventListener('click', printCart);
```
```JavaScript
// custom binder (like the bind works)
const customBind = function(fn, context) {
  return function() {
    return fn.apply(context, arguments);
  };
};
```

</details>

<details>
<summary>What are the differences of scope related to arrow functions?</summary>

- arrow functions do not have their own context (even when we use `call`, `apply` or `bind`)
- arrow functions passed as a callback to event listeners also have no context
- even with strict mode `this` won't be undefined but referred to the global scope (arrow functions do not have `this` property)
- arrow functions **NEVER** have their own context
```JavaScript
const players = {
  team: 'Griffindor',
  members: ['Harry', 'Ron', 'Hermione'],
  getMembers() {
    this.members.forEach((member) => {
      // works fine because arrow function
      // doesn't bind this
      // so this is the same as in getMembers function
      console.log(member, this.team);
    });
  }
};

players.getMembers();
```

</details>

<details>
<summary>Practical questions</summary>

  ### 1. What will be logged to the console?
  ```JavaScript
  const guitarStore = function() {
    this.guitarCount = 2;

    (function() {
      this.guitarCount = 1;
    })();

    console.log(this.guitarCount);
  };

  const guitarShop = {
    guitarCount: 3,
    showMeAnswer: function () {
      console.log(this.guitarCount);
    },
  };

  guitarStore();
  new guitarStore();
  guitarShop.showMeAnswer();
  new guitarShop.showMeAnswer();
  guitarStore.apply(guitarStore);
  guitarShop.showMeAnswer.apply(guitarStore);
  guitarStore.bind({})();
  ```

  <details>
  <summary>Answer</summary>

  Код работает в нестрогом режиме. Значением this будет ссылка на объект Window. Поэтому, в Window будет создано свойство guitarCount и изменено дважды: внутри guitarStore() и во вложенной IIFE. Поэтому в консоли получим значение 1.

  Мы вызываем функцию с new, то есть внутри this будет новый объект. По факту мы создаём экземпляр guitarStore. Таким образом, в объект (this) запишется значение 2. Дальше будет вызов IIFE. Она будет вызвана без new, код работает в нестрогом режиме. Следовательно, внутри IIFE, this будет ссылаться на Window. Будет создано свойство guitarCount со значением 1. То есть мы работаем с другим объектом, а не с тем, в который записали 1. Поэтому значением будет 2;

  Метод вызван в контексте объекта. Следовательно, this будет содержать ссылку на объект. Поэтому значение 3 (у объекта есть одноимённое свойство).

  Здесь пытаемся вызвать метод showMeAnswer как функцию-конструктор. Поэтому в this будет новый объект. У него нет свойства guitarCount, поэтому в консоль выводится undefined.

  Вызов функции происходит с помощью apply. Мы принудительно устанавливаем в виде контекста саму функцию guitarStore. Функции — это объекты, поэтому внутри функции мы просто добавляем ей (функции) свойство guitarCount со значением 2. IIFE будет вызвана как обычная функция, следовательно контекстом для неё будет Window (код работает в нестрогом режиме). Поэтому она не изменит содержимое guitarCount. Здесь важно понять, что мы фактически добавили для функции новое свойство. Вы можете в этом убедиться так:

  guitarStore.apply(guitarStore); // Первый вызов
  console.log(guitarStore.guitarCount); // 2
  Мы вызываем метод showMeAnswer с помощью метода apply. Контекстом устанавливаем функцию guitarStore. Следовательно, если внутри метода showMeAnswer мы обратимся к this.guitarCount, то получим undefined (у функции нет такого свойства). НО! Если мы раскомментируем предыдущий вызов функции (guitarStore.apply(guitarStore);), то в консоли увидим вместо undefined значение 2. Почему? Предыдущий код добавит функции одноимённое свойство, которое мы сможем считать в showMeAnswer. Чтобы лучше визуализировать, перечитайте предыдущий пункт.

  Значением будет 2, так как мы биндим в качества контекста пустой объект. Следовательно, значением this внутри guitarCount будет пустой объект, к которому мы добавим свойство guitarCount со значением 2. IIFE будет вызвана как обычная функция и её контекстом будет Window. Поэтому она просто добавит в Window новое свойство guitarCount со значением 1.

  </details>

</details>

<details>
<summary>Learn more</summary>

- [this on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [What is `this`? The Inner Workings of JavaScript Objects](https://medium.com/javascript-scene/what-is-this-the-inner-workings-of-javascript-objects-d397bfa0708a)

</details>

## Constructors and prototypes
<details>
<summary>What is `__proto__` of an Object constructor?</summary>

- base `Object` doesn't have a `__proto__`

</details>

<details>
<summary>When the constructor prototype is assigned?</summary>

- constructor prototype is assigned to the instance upon creation

</details>

<details>
<summary>Where does prototype exist? (On what type of object?)</summary>

- `prototype` property exists only on function object

</details>

<details>
<summary>How the prototype chain works?</summary>

```JavaScript
const Player = function(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
};

// == extends in classes
Player.prototype.play = function() {};

const harryPotter = new Player('Harry', 'Potter');
const ronWeasley = new harryPotter.__proto__.constructor('Ron', 'Weasley');

// first looks inside the instance
// than in Player prototype (harryPotter.__proto__.play())
harryPotter.play();
console.log(harryPotter.__proto__ === Player.prototype); // => true
// than in the Player's prototype's prototype
// till it reaches the Object.prototype
// harryPotter.__proto__.__proto__.toString();
harryPotter.toString();
```

</details>

<details>
<summary>How to create and use a constructor function?</summary>

- naming `Player`
- creation of an instance with `new` keyword
- add a method to the prototype
```JavaScript
const Player = function(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
};

// to add a static method
Player.describe = function() {
  console.log('Creating players.');
};

// __proto__: { play: function() {} }
Player.prototype.play = function() {};

// will add method to object Player
// available Player.play() only
// if called on instance = TypeError
Player.play = function() {};

const harryPotter = new Player('Harry', 'Potter');
```

</details>

<details>
<summary>What if we return something from a constructor function?</summary>

- if `return` is called with an object, the object is returned instead of `this`
- if `return` is called with a primitive, it's ignored

</details>

<details>
<summary>What the `new` keyword does?</summary>

- `new` keyword doesn't call the function, it creates an object with it's fields (when we use `this.name = name`)
```JavaScript
const Player = function(firstName, lastName) {
  // new 'creates' this as an object
  this = {};
  // adds properties and methods
  this.firstName = firstName;
  this.lastName = lastName;
  this.greet = function() {
    console.log(`Hello! I'm ${this.firstName} ${this.lastName}`);
  };
  // returns the object
  return this;
};
```

</details>

<details>
<summary>What if we try to create an instance without the `new` keyword?</summary>

- without `new` => `undefined` (void = return undefined) will not be created
```JavaScript
const ron = Player('Ron', 'Weasley'); // undefined, not created
```

</details>

<details>
<summary>How to check if the instance was created with a `new` keyword?</summary>

```JavaScript
// ES6+
const Player = function(firstName, lastName) {
  // undefined for regular calls
  // equals the function if called with new
  if (!new.target) { 
    throw new Error('Should be called with new operator.'); 
  }

  // to create an object even if new is not used
  if (!new.target) {
    return new Player(firstName, lastName);
  }
};
```

</details>

<details>
<summary>How to check what constructor was used to create an instance?</summary>

```JavaScript
console.log(harryPotter instanceof Player); // => true
```

</details>

<details>
<summary>Why `new` if we can just return an object or this?</summary>

- `instanceof` becomes useless
- inheritance (prototype) won't work
- if you try to imitate a constructor and `return this;`, `this` would be a global object

</details>

<details>
<summary>Learn more</summary>

- [Prototypal Object-Oriented Programming using JavaScript](https://alistapart.com/article/prototypal-object-oriented-programming-using-javascript/)
- [Inheritance in JavaScript on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

</details>

## Classes
<details>
<summary>How to create a class and what method is better?</summary>

- `class` better than `const` when creating a class
```JavaScript
class Player {
  // is optional (only one or none)
  // helps to create an instance of a class
  // is called when creating an instance with a new keyword
  constructor() {}

  // for every instance
  onClick = () => {}

  // inside prototype
  play() {}
}

// don't create classes like this
const Singer = class {};
```

</details>

<details>
<summary>What are properties and fields of a class and are they different?</summary>

- properties and fields are basically the same thing
```JavaScript
class Player {
  // fields (still poor support)
  // for now use methods only
  // and add all the properties inside of constructor
  level = 2;

  // all properties are defined here
  constructor(name) {
    // properties
    this.name = name;
    this.onButtonClickArrowFn = () => {
      // this === current instance of a class
      console.log(this);
    };
  }
}

```

</details>

<details>
<summary>How to create an instance of a class?</summary>

- `new` for creating an instance (or type error due to built-in `new.target` check)
```JavaScript
const player = new Player('Harry');
```

</details>

<details>
<summary>What if you try to access the field or property which is not defined in the class?</summary>

- `undefined`

</details>

<details>
<summary>Can we use getters and setters in a class?</summary>

- getters / setters can be used

</details>

<details>
<summary>How to add private fields?</summary>

- private fields, soon to use `this.#skill = value;`

</details>

<details>
<summary>How to deal with event listeners if we need `this` reference to an instance of a class?</summary>

```JavaScript
class Player {
  constructor() {
    this.onButtonClickArrowFn = () => {
      // this === current instance of a class
      console.log(this);
    };
  }

  onButtonClick() {
    console.log(this);
  }

  play() {
    // this === button
    button.addEventListener('click', this.onButtonClick);
    // this === current instance of a class
    button.addEventListener('click', this.onButtonClick.bind(this));
    button.addEventListener('click', () => this.onButtonClick());
    // but is created for every instance
    button.addEventListener('click', this.onButtonClickArrowFn);
  }
}

```

</details>

<details>
<summary>How do classes actually work (under the hood)?</summary>

```JavaScript
class Person {}

// extends works like a __proto__
// Player.__proto__ === Person.prototype
class Player extends Person {
  name = 'Harry';

  constructor() {
    super();
    this.age = 33;
    // if created like this => part of any instance (like a property)
    this.play = function() {};
  }

  // methods are added to prototype
  greet() {
    console.log(`Hi! My name is ${this.name}.`);
  }

  // if created like this => part of any instance (like a field/property)
  play = function() {};
  // if we use an arrow function here, context will stay the same
  // even when added as an event handler (don't have to bind)
  play = () => {};
}
```

</details>

<details>
<summary>How to create static properties, fields and methods?</summary>

- properties can also be static (but still poor browser support)
- not inherited, accessible on a class without instantiation
```JavaScript
class Player {
  constructor(level, weaponsCount) {
    this.level = level;
    this.weaponsCount = weapons;
  }

  static createJuniorPlayer() {
    return new this(5, 2);
  }
}

const juniorPlayer = Player.createJuniorPlayer();
```

</details>

<details>
<summary>What are the differences between a class and a constructor function?</summary>

- `class` can't be used without `new` (could be imitated inside the constructor function with `new.target`)
- different log to console (function and class)
- class methods are not iterable
```JavaScript
for (const prop in player) {
  console.log(prop);
}
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [OOP notes](./oop.md)
- [ ] [Classes on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [ ] [ES6 Classes in Depth](https://ponyfoo.com/articles/es6-classes-in-depth)

</details>

## Modules
<details>
<summary>What problems do modules solve?</summary>

- namespace
  - no global scope
  - encapsulation
- dependencies
  - easy to follow on what module depends on
- interface
  - methods and props export, easy to navigate

</details>

<details>
<summary>What methods to write modules were used in ES5 (and what are the downsides)?</summary>

- manual configuration
- have to remember dependencies order
- is not clear, what dependencies are used

```JavaScript
// IIFE
'use strict';
// slider.js
(function() {
  window.slider = {
    name: 'Eve'
  };
})();
```

- better module approaches were found (AMD, CommonJS, UMD)

</details>

<details>
<summary>What about `use strict` inside the module?</summary>

- `'use strict;'` by default

</details>

<details>
<summary>How to create a module?</summary>

- syntax looks like destructuring but not the same
- better export const or class (if you export let, can't reassign in the other module anyway)
- do not fold `export` and `import` into code blocks `{}`
```JavaScript
// module-name.js
// named - names should be the same (or error, module won't get loaded)
// could import not all the export
// can't export the same variable 2x
// better not to combine inline and group exports
export { name, age };
// or
export const name = 'Max';
export const age = 40;
// renamed
export { name as userName };
// default
// better for classes
// could be hard to debug (imported by any name)
export default name;
export default { name };
export { name as default };
```

</details>

<details>
<summary>How to import a module?</summary>

- syntax looks like destructuring but not the same
- imported variable is not created (the same link to the exported variable)
- do not fold `export` and `import` into code blocks `{}`
- no hoisting, so that's why `import` is always on top
```JavaScript
// other-module.js
// import using the same variable name
import { name } from './module-name.js';
// import all as child (ignores default, insecure, have no control on import)
import * as child from './module-name.js';
// renamed
import { name as userName } from './module-name.js';
// default
import name from './module-name.js';
import { default as name } from './module-name.js';
// import without a variable if we only need to execute the code from module
import './log.js';
```

</details>

<details>
<summary>What if we import an inexistent variable or some error occurs while importing a module or children?</summary>

- `import` of inexistent variable = error, module won't get loaded
- if there is an error while downloading the module or its children => all connected modules won't get loaded

</details>

<details>
<summary>What are the dynamic imports?</summary>

- there are dynamic imports, but browser support is still pretty poor

</details>

<details>
<summary>What if you import the same module for several times?</summary>

- even when you import the same module several times, browser loads only once

</details>

<details>
<summary>What paths can be used in imports?</summary>

- both `''` and `""` available
- path is an immutable constant, can't generate the path
- if 2 same imports => browser downloads only one
- paths abs or rel
  - `https://google.com` url
  - `/utils/helpers.js` abs domain-name
  - `./helpers.js` rel
  - `../helpers.js` rel
- `helpers.js` or `utils/helpers.js` is not supported (reserved for libs from package managers)

</details>

<details>
<summary>What are the module loaders?</summary>

- browsers: ES modules in browsers
```HTML
<!-- adding modules to the page -->
<!-- by default works like defer -->
<script type="module">
  // some code here
</script>
<script src="module-1.js" type="module"></script>
<!-- fallbacks (ignored by browsers, which support modules) -->
<script src="module-1.js" nomodule></script>
```
- static: webpack, rollupJS, parcel, ...

</details>

<details>
<summary>What does the module loader do?</summary>

- orders files
- downloads, stores files
- builds, minifies, packs
- all dependencies are loaded relatively to the 1st loaded module
- browser cashes not only a file, but also the result of executing the module + returned values

</details>

<details>
<summary>What is a proxy module?</summary>

```JavaScript
// module-1.js
export { name as nameOne };

// module-2.js
export { name as nameTwo };

// module-3.js
export * from './module-1.js';
export * from './module-2.js';

// module-target.js
import { nameOne, nameTwo } from './module-3.js';

// if the proxy is named index.js
import { nameOne, nameTwo } from './folder';
```

</details>

<details>
<summary>Learn more</summary>

- [IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
- [What is AMD, CommonJS, and UMD?](https://www.davidbcalhoun.com/2014/what-is-amd-commonjs-and-umd/)
- [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)
- [Common.js](http://www.commonjs.org/)
- [UMD](https://github.com/umdjs/umd)
- [ECMAScript modules in browsers](https://jakearchibald.com/2017/es-modules-in-browsers/)
- [ES6 In Depth: Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
- [ES6 Modules in Depth](https://ponyfoo.com/articles/es6-modules-in-depth)
- [import on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
- [export on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [Exploring ES6 - 16. Modules](https://exploringjs.com/es6/ch_modules.html)
- [ ] [Modules on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

</details>

## Window Object
<details>
<summary>What is the `window` object and how do we use it?</summary>

- browser API, contains all the global properties and methods
```JavaScript
// can call both ways
alert('Say something');
window.alert('Say something');
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Window on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window)

</details>

## DOM
<details>
<summary>What is DOM?</summary>

- a part of `window` object

</details>

<details>
<summary>How does the browser searches through the DOM?</summary>

- browser searches DOM in depths, so that the first tag is being found (otherwise not obvious)

</details>

<details>
<summary>How to select the elements with query methods?</summary>

- if no matching => `null` for single or empty collection
```JavaScript
// any css selector
// returns first matching element in the DOM
document.querySelector('ul li:last-child');
// any css selector
// returns NodeList - static collection (snapshot)
// DOM changes doesn't affect 
// (nodes, not only DOM elements, also text, spaces, etc)
document.querySelectorAll('li');

// all those methods could be called only on document, not on element
document.getElementById('title');
// return HTMLCollection - live collection
document.getElementsByClassName('class');
document.getElementsByTagName('li');
```

</details>

<details>
<summary>How to select parents, children, descendants, ancestors?</summary>

```JavaScript
const element = document.querySelector('ul');

// parent node (any parent node: element, text etc)
// but in many cases works the same
element.parentNode;
// selects document
document.documentElement.parentNode;
// parent html element
element.parentElement;
// returns null
element.documentElement.parentElement;
// ancestor
element.closest('selector');

// child nodes (any: element, text etc)
element.childNodes;
// returns HTMLCollection - live collection (only DOM elements)
element.children;

// first or last child node
element.firstChild;
element.lastChild;
// first or last child html element
element.firstElementChild;
element.lastElementChild;

// siblings
element.previousSibling;
element.previousElementSibling;
element.nextSibling;
element.nextElementSibling;
```

</details>

<details>
<summary>How to select some html elements with special properties?</summary>

```JavaScript
// to select the <html>
document.documentElement;
// to select the <body>
document.body;
// to select the <head>
document.head;
```

</details>

<details>
<summary>How do some attribute changes work (changes UI/value)?</summary>

```JavaScript
const input = document.querySelector('input');

// UI changes but value html attribute stays the same
// classes, ids etc do change the html attribute
input.value = 'Some new text';
// UI stays the same but value attribute changes
input.setAttribute('value', 'Other text');
```

</details>

<details>
<summary>How to work with data attributes?</summary>

```JavaScript
// html attribute data-cat-name="Cat" can be accessed
const catName = element.dataset.catName;
```

</details>

<details>
<summary>What are data attributes good for?</summary>

- works great for tooltips

</details>

<details>
<summary>How to insert some text to HTML?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.textContent = 'Some text';
// increments the content
element.textContent++;
// is the same
element.textContent = element.textContent++;
```

</details>

<details>
<summary>How to insert an element to HTML using an HTML string?</summary>

```JavaScript
const element = document.querySelector('section');
// replaces all the content inside the element
element.innerHTML = '<p>Description</p>';
// add html to a specific position
element.insertAdjacentHTML('beforeend', '<p>Description</p>');
```

</details>

<details>
<summary>How to create an element?</summary>

```JavaScript
const newElement = document.createElement('p');
newElement.textContent = 'Description';
```

</details>

<details>
<summary>How to add / move the element to the DOM?</summary>

```JavaScript
// all these methods remove the element (if existed)
// and move to the new position
// (need to clone not to be removed)
// append new DOM element or node
// any node, several nodes (IE not supported)
// last inside the element
element.append('Some text', newElement);
// first inside the element
element.prepend(newElement);
// before the element (as sibling) (problems with Safari)
element.before(newElement);
// after the element (as sibling) (problems with Safari)
element.after(newElement);
// replace existing DOM element or node with a new one
element.replaceWith(newElement);

// only one element (older methods, have IE support)
// = append();
element.appendChild(newElement);
// = before();
// if referenceNode === null, newElement is inserted
// at the end of the element's child nodes
const newNode = element.insertBefore(newElement, referenceNode);
const newNode1 = element.insertBefore(newElement, null);
// = replaceWith();
const oldNode = element.replaceChild(newElement, oldElement);

// alternative method (supports IE, Safari)
element.insertAdjacentElement('beforeend', newElement);
```

</details>

<details>
<summary>How to clone the DOM Node?</summary>

```JavaScript
// deep? boolean
// better to pass an argument
// (default could be different for some browsers)
const newElement = element.cloneNode(true);
```

</details>

<details>
<summary>How to remove the elements from the DOM?</summary>

```JavaScript
const element = document.querySelector('p');

element.innerHTML = '';
// IE is not supported
element.remove();
// works with IE
element.parentElement.removeChild(element);
```

</details>

<details>
<summary>What happens to the event listeners when the element is removed from the DOM?</summary>

- when the element is deleted (no reference left), all the listeners are also cleaned up - no memory leaks

</details>

<details>
<summary>How to work with styles in JS?</summary>

- `style` to get styles but only the inline styles
```JavaScript
const element = document.querySelector('p');

// for CSS properties in several words camelCase is used in JS
element.style.backgroundColor = 'green';
element.style['backgroundColor'] = 'green';
element.style['background-color'] = 'green';
```
- `window.getComputedStyle` to get all styles applied to the element

</details>

<details>
<summary>How to work with the element coordinates relative to the document?</summary>

- always relative to the start of the document, not the viewport (doesn't change upon scrolling)
```JavaScript
// readonly property
const topPosition = element.offsetTop;
```

</details>

<details>
<summary>How to work with the element inner coordinates?</summary>

- inner coordinates of the element do not include the border
- rounds the value to an integer
- the distance from where the margin area ends and the padding and content begins
```JavaScript
// readonly integer property
const innerTop = element.clientTop;
const innerLeft = element.clientLeft;
```

</details>

<details>
<summary>How to work with the element measurements?</summary>

- height of an element's content (including the content not visible on the screen due to overflow)
```JavaScript
// readonly property
const elementFullHeight = element.scrollHeight;
```

</details>

<details>
<summary>How to get the window width and height with and without scroll?</summary>

- in pixels
```JavaScript
// readonly properties
const viewportWidthWithScroll = window.innerWidth;
const viewportHeightWithScroll = window.innerHeight;

// real available window sizes not including the scroll
const viewportWidth = document.documentElement.clientWidth;
const viewportHeight = document.documentElement.clientHeight;
```

</details>

<details>
<summary>How to scroll the content into the viewport?</summary>

```JavaScript
element.scrollIntoView();
```

</details>

<details>
<summary>How to work with templates?</summary>

- `importNode` (learn more)

</details>

<details>
<summary>Learn more</summary>

- [Introduction to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- [querySelector on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [querySelectorAll on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [getElementById on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
- [getElementsByClassName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [getElementsByTagName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)
- [getElementsByName on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByName)
- [insertAdjacentHTML on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)
- [append on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/append)
- [appendChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
- [prepend on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/prepend)
- [insertBefore on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)
- [before on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/before)
- [after on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/after)
- [insertAdjacentElement on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement)
- [replaceWith on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/replaceWith)
- [replaceChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/replaceChild)
- [remove on MDN](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove)
- [removeChild on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
- [getBoundingClientRect on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)

</details>

## Events
<details>
<summary>What is the general constructor for the event?</summary>

- made with `Event` constructor

</details>

<details>
<summary>What are the specific event constructors?</summary>

- specific constructors inherited from `Event` (ex `MouseEvent`, `DragEvent`)

</details>

<details>
<summary>To what element can you add the event?</summary>

- can be added to any element (even div)

</details>

<details>
<summary>When are the event listeners removed?</summary>

- event listeners are removed when there is no reference to the element left (either in code or DOM)

</details>

<details>
<summary>How to add the listener (2 ways)?</summary>

- `onclick` attribute or adding via JS `element.onclick = console.log();` overrides previous handler (can't add 2 handlers)
- the best way to add events is `element.addEventListener();`

</details>

<details>
<summary>What is the difference between `change` and `input`?</summary>

- `change` works when `field.value` changed and the user finished to enter the value (moved the handle and released)
- `input` works with every value change

</details>

<details>
<summary>How to implement the scroll event?</summary>

- useful for infinite loading
```JavaScript
let currentElementNumber = 0;

const onScroll = () => {
  // measure the distance between our viewport (top left corner)
  // and the end of the page (not viewport)
  const distanceToBottom = document.body.getBoundingClientRect().bottom;
  const viewportHeight = document.documentElement.clientHeight;

  // compare to the window height + threshold
  // if we have < 100px to the end of the content,
  // append new data
  if (distanceToBottom < viewportHeight + 100) {
    const newElement = document.createElement('div');

    currentElementNumber++;
    newElement.innerHTML = `<p>Add element ${currentElementNumber}</p>`;
    document.body.append(newElement);
  }
};

window.addEventListener('scroll', onScroll);
```

</details>

<details>
<summary>What are the event phases?</summary>

- (1) capturing (out - in) => (2) bubbling (in - out)

</details>

<details>
<summary>In what phase does `addEventListener` register the event by default and how to switch the behavior?</summary>

- `addEventListener` by default registers event in a bubbling phase (when we have a listener on button and it's wrapper, first fires button, second wrapper)
- third parameter of `addEventListener(, , true);` switches to the capturing phase (can add to only one listener in a chain)

</details>

<details>
<summary>How to stop the event phases?</summary>

- to prevent propagation
```JavaScript
evt.stopPropagation();
evt.stopImmediatePropagation();
```

</details>

<details>
<summary>What is the event delegation and what are `target` and `currentTarget`?</summary>

- `event.target` is referred to the actual item triggered the event
- `event.currentTarget` always referred to the element, where the listener is added
- `event.target.closest('li');` can also get the item itself

</details>

<details>
<summary>How to trigger DOM events programmatically?</summary>

```JavaScript
// if triggered like that, the event listener added
// is skipped (won't get executed)
// but triggering click event on submit button will work
form.submit();
// works with added listeners
button.click();
```

</details>

<details>
<summary>What is `this` inside the event handler?</summary>

- with arrow functions as handlers `this === window`
- with regular function as handler `this === evt.currentTarget`

</details>

<details>
<summary>How to implement Drag & Drop?</summary>

1. set attribute to `draggable="true"`
2. listen to `dragstart` event (describe the operation and append some data here)
```JavaScript
elementToDrag.addEventListener('dragstart', evt => {
  evt.dataTransfer.setData('text/plain', id);
  evt.dataTransfer.effectAllowed = 'move';
});
```
3. allow to drop into the droppable area (add `preventDefault()` to `dragenter` and `dragover` events)
```JavaScript
// if in drop area we won't prevent default,
// drop event won't be triggered
containerDroppable.addEventListener('dragenter', evt => {
  // can get the data type
  // but not the actual data
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
    // add some visual effect to indicate
    // it's droppable (on dragenter)
    containerDroppable.parentElement.classList.add('droppable');
  }
});

containerDroppable.addEventListener('dragover', evt => {
  if (evt.dataTransfer.types[0] === 'text/plain') {
    evt.preventDefault();
  }
});
```
4. (optional) listen to `dragleave` event (ex. to update some styles)
```JavaScript
containerDroppable.addEventListener('dragleave', evt => {
  // check if only left the element, not just moved
  // to it's children 
  // (w/o this will be triggered when move over the children elements)
  if (evt.relatedTarget.closest('ul') !== containerDroppable) {
    containerDroppable.parentElement.classList.remove('droppable');
  }
});
```
5. listen to `drop` event and update data and UI
```JavaScript
// to react to the drop event need to add a listener
// to the droppable container
containerDroppable.addEventListener('drop', evt => {
  // can get any data we set in dragstart event
  // (now it's available)
  const id = evt.dataTransfer.getData('text/plain');

  // check if the item is in the list and do nothing
  // if not - add item to the list and remove where it was
});
```
6. (optional) listen to `dragend` event and update data and UI (triggered event when the drag was canceled)
```JavaScript
// is added to a draggable element
elementToDrag.addEventListener('dragend', evt => {
  // check if the drag wasn't done
  evt.dataTransfer.dropEffect === 'none';
});
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Introduction to events on MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [ ] [Event reference on MDN](https://developer.mozilla.org/en-US/docs/Web/Events)
- [ ] [Event on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event)
- [ ] [Drag and drop API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)

</details>

## Forms
<details>
<summary>What is the basic implementation of show password case?</summary>

- change type of input from `password` to `text`

</details>

<details>
<summary>Learn more</summary>

- [How to Build and Validate Beautiful Forms with Vanilla HTML, CSS, & JS](https://www.freecodecamp.org/news/build-and-validate-beautiful-forms-with-vanilla-html-css-js/)

</details>

## Working with data
<details>
<summary>What are the main problems when working with data?</summary>

- user input - user can enter unsafe data for the view and UI has to be ready for it
- storing and passing data formats could be different to the format needed on the UI, so we need to convert data in our app
  - some ES6 objects (Date, Sets, Maps) could not be converted to JSON, so have to convert into standard data types (primitives, arrays, objects)

</details>

<details>
<summary>What is JSON (and the restrictions)?</summary>

- JavaScript Object Notation
- can't use functions here
- for keys only `" "`
- for values `"string"` (double quotes only), `10`, `true`, `{...}`, `[...]`, `null`

</details>

<details>
<summary>How to get the parameters from the link?</summary>

```JavaScript
const url = new Url(location.href);
const queryParams = url.searchParams;
const data = queryParams.get('data');
```

</details>

<details>
<summary>How to convert into a link?</summary>

- `encodeURI('some text');`

</details>

<details>
<summary>Learn more</summary>

- [ ] [Why Mutation Can Be Scary](https://alistapart.com/article/why-mutation-can-be-scary/)

</details>

## Loading scripts to the page
<details>
<summary>How to load script files from JS dynamically?</summary>

- basically generate html and add it to the page

</details>

## Location API
<details>
<summary>What is the location API used for?</summary>

- for the app url and navigation

</details>

<details>
<summary>Learn more</summary>

- [ ] [Location on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Location)

</details>

## History API
<details>
<summary>What is history API used for?</summary>

- works with location
- can use `history.back()` to navigate back (ex different cases with questions like age)

</details>

## Navigator API
<details>
<summary>Why do we use the navigator API?</summary>

- don't use for defining browser version
- could be useful when we need
  - geolocation

</details>

<details>
<summary>Learn more</summary>

- [ ] [Navigator on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

</details>

## Browser storage
<details>
<summary>What are local and session storages and what is the difference?</summary>

- simple key-value store
- local storage lives till either user or browser (when ran out of space) clears it
- session storage lives in the browser while you don't close the tab

</details>

<details>
<summary>What are local and session storages good for?</summary>

- manage user preferences or basic user data
- simple, easy to use, but bad for complex data

</details>

<details>
<summary>How are local and session storages being cleared?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to work with the local storage?</summary>

```JavaScript
// local storage works sync
const userId = '775';
const user = {
  name: 'Harry',
  age: 33
};

// JS converts data into a string
localStorage.setItem('userId', userId);
localStorage.setItem('user', user); // => [object Object]
localStorage.setItem('user', JSON.stringify(user));

// to get item
localStorage.getItem('user');
```

</details>

<details>
<summary>How to work with the session storage?</summary>

```JavaScript
// session storage works sync

// JS converts data into a string
sessionStorage.setItem('userId', userId);
sessionStorage.setItem('user', JSON.stringify(user));

// to get item
sessionStorage.getItem('user');
```

</details>

<details>
<summary>What are cookies and the difference from local/session storage?</summary>

- cookie stored to server
- simple key-value store with some config options
- not as easy to use
- the advantage is that you can set it to expire or send to a server
- available only if your app is served on a running server

</details>

<details>
<summary>What are cookies good for?</summary>

- manage user preferences or basic user data
- bad for complex data

</details>

<details>
<summary>How to clear the cookies?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use cookies?</summary>

```JavaScript
// cookies work sync
const userId = 'fd3928';
const user = {
  name: 'Harry',
  age: 33
};
// data stored as a string
// under the hood uses a setter
// so adds new cookie, not overrides
document.cookie = `userId=${userId}; max-age=360`; // => seconds
document.cookie = `user=${JSON.stringify(user)}; expires=date`; // => date

// to get info
// returns all the cookies stored in one string
document.cookie;
```

</details>

<details>
<summary>What is IndexedDB?</summary>

- client-side database

</details>

<details>
<summary>What is IndexedDB good for?</summary>

- manage complex data your app needs
- not as easy to use, great for complex (non-critical) data, good performance (good for usage like google sheets)

</details>

<details>
<summary>How to clean the IndexedDB?</summary>

- can be cleared by the user and via JS

</details>

<details>
<summary>How to use IndexedDB?</summary>

```JavaScript
// indexedDB works sync
// 1. open a database
// pass name and version
// creates or opens an existed DB
const dbRequest = indexedDB.open('Name', 1);
let db;

// to be able to change the data from a button too
dbRequest.onsuccess = function(evt) {
  // access to the created database
  db = evt.target.result;
};

// for better browser support not .addEventListener, but:
// this event runs when the db is created or the version is upgraded
dbRequest.onupgradeneeded = function(evt) {
  db = evt.target.result;

  // 2. create an object store
  const objStore = db.createObjectStore('products', {keyPath: 'id'});

  // 3. start a transaction and make a request to do some db operation
  // 4. wait for the operation to complete
  // 5. do something with the results
  // oncomplete triggers when createObjectStore is finished
  objStore.transaction.oncomplete = function(evt) {
    // connecting to the data base
    // name of the store + mode (readonly, readwrite, etc)
    const productsStore = db.transaction('products', 'readwrite')
      .objectStore('products');
    // adding a new item, has to have the property from keyPath
    productsStore.add({
      id: 'pr1',
      name: 'Product 1',
      price: 1.22,
      tags: ['Vegetarian', 'No-Sugar']
    });
  };
};

dbRequest.onerror = function() {};

addButton.addEventListener('click', () => {
  if (!db) {
    return;
  }

  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  productsStore.add({
    id: 'pr2',
    name: 'Product 2',
    price: 1.42,
    tags: ['Vegetarian', 'No-Sugar']
  });
});

// to retrieve the data
getButton.addEventListener('click', () => {
  const productsStore = db.transaction('products', 'readwrite')
    .objectStore('products');

  const request = productsStore.get('pr1');

  request.onsuccess = function() {
    console.log(request.result);
  };
});
```

</details>

<details>
<summary>How to work with cache?</summary>

```JavaScript
// create the cache name (could be any)
const CACHE_PREFIX = 'app-cache';
// add the version if you need to track versions
const CACHE_VER = 'v1';
const CACHE_NAME = `${CACHE_PREFIX}-${CACHE_VER}`;

const HTTP_STATUS_OK = 200;
const RESPONSE_SAFE_TYPE = 'basic';

// add statics to cache
caches.open(CACHE_NAME)
  .then((cache) => {
    // can't use folders, have to specify the path for each
    return cache.addAll([
      '/',
      '/index.html',
      'styles.css',
      'scripts.js',
      '/fonts/font-name-400.woff2',
      '/img/pic.png',
    ]);
  });
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [localStorage on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- [ ] [cookie on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)
- [ ] [Using IndexedDB on MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)

</details>

## Service Workers, Web Workers and Worklets
<details>
<summary>How to check if the internet is available?</summary>

- ping the server
- `window.navigator.onLine`
- events `window`: `online`, `offline` - if there is a connection but the internet is off, won't work

</details>

<details>
<summary>What is a proxy server?</summary>

- the server between the browser and the server
- accepts the client requests and sends them to the server
- can cache the response
- can modify the requests and the responses

</details>

<details>
<summary>What is a Service Worker?</summary>

- acts as proxy server that sit between web applications, the browser, and the network (when available)
- runs on a different thread to the main JavaScript that powers your app, so it is non-blocking
- no DOM access
- sync API can't be used (XHR, LocalStorage, etc) but can work with IndexedDB
- context is not `this` but `self`
- enable the creation of effective offline experiences
- intercept network requests and take appropriate action based on whether the network is available
- update assets residing on the server
- allow access to push notifications and background sync APIs
- works only with https

</details>

<details>
<summary>What is the Service Worker lifecycle?</summary>

- registration
- setting
- activation
- interception

</details>

<details>
<summary>How to register the Service Worker?</summary>

```JavaScript
window.addEventListener('load', () => {
  // path to service worker code
  navigator.serviceWorker.register('/sw.js');
});
```

</details>

<details>
<summary>How to set a service worker?</summary>

```JavaScript
// combined with cache API
const CACHE_PREFIX = 'app-cache';
const CACHE_VER = 'v1';
const CACHE_NAME = `${CACHE_PREFIX}-${CACHE_VER}`;

const HTTP_STATUS_OK = 200;
const RESPONSE_SAFE_TYPE = 'basic';

self.addEventListener('install', (evt) => {
  // set the resources we want to cache
  // waitUntil guarantees that the actions inside
  // (waits till the promise if resolved)
  // will be executed till the install event ends
  // pass the async code
  // if no waitUntil is used or
  // if the promise inside will be rejected,
  // the service worker won't be registered
  evt.waitUntil(
    caches.open(CACHE_NAME)
      .then((cache) => {
        // can't use folders, have to specify the path for each
        return cache.addAll([
          // to be able to navigate without index.html
          '/',
          '/index.html',
          'styles.css',
          'scripts.js',
          '/fonts/font-name-400.woff2',
          '/img/pic.png',
        ]);
      });
  );
});
```

</details>

<details>
<summary>How to activate a service worker?</summary>

```JavaScript
self.addEventListener('activate', (evt) => {
  evt.waitUntil(
    // get all the cache names
    caches.keys()
      .then((keys) => Promise.all(keys
        .map((key) => {
          // delete only our caches but the ver is different
          // just to store only the actual ver and avoid conflicts
          // and release the storage
          if (key.startsWith(CACHE_PREFIX) && key !== CACHE_NAME) {
            return caches.delete(key);
          }

          // skip the other
          return null;
        })
        .filter((key) => key !== null)
      ));
  );
});
```

</details>

<details>
<summary>How to intercept a request with a service worker?</summary>

```JavaScript
// fires every time when our app tries to send a request
// (get files, get data, update data)
self.addEventListener('fetch', (evt) => {
  const {request} = evt;

  // check the request with the cache registered resources
  evt.respondWith(
    caches.match(request)
      .then(cacheResponse => {
        // if the response is cached
        // return cached instead of going to the server
        if (cachedResponse) {
          return cachedResponse;
        }

        // if no response, all fetch one more time
        // with the same request
        // and return it
        return fetch(request)
          .then((response) => {
            // if no response or status !== 200 OK
            // or the response is unsafe (not basic)
            // just pass the response and do not intercept
            if (!response 
              || response.status !== HTTP_STATUS_OK
              || response.type !== RESPONSE_SAFE_TYPE) {
              return response;
            }

            // if the response is correct, clone it
            const clonedResponse = response.clone();

            // save to cache
            caches.open(CACHE_NAME)
              .then((cache) => cache.put(request, clonedResponse));

            // and return the original response
            return response;
          });
      });
  );
});
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Web workers vs Service workers vs Worklets](https://bitsofco.de/web-workers-vs-service-workers-vs-worklets/)
- [ ] [Chrome service worker inspector](chrome://inspect/#service-workers)
- [ ] [Chrome service worker internals](chrome://serviceworker-internals)
- [ ] [MDN: Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
- [ ] [Google: Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers)

</details>

## Timers and intervals
<details>
<summary>How to cook a dish using callbacks and timeouts?</summary>

```JavaScript
const Timeout = {
  GET: 9000,
  WASH: 3000,
  CUT: 8000,
  ADD_SPICES: 1000,
  COOK: 5000
};

const makeTheDish = () => {
  console.log('1. Getting the products');
  const products = ['pumpkin', 'tomato', 'celery', 'spices', 'nuts'];

  setTimeout(() => {
    console.log('2. Washing the products');
    setTimeout(() => {
      console.log('3. Cutting the products');
      setTimeout(() => {
        console.log('4. Adding the spices');
        setTimeout(() => {
          console.log('5. Cooking the dish');
          setTimeout(() => {
            console.log('Ready to eat!');
          }, Timeout.COOK);
        }, Timeout.ADD_SPICES);
      }, Timeout.CUT);
    }, Timeout.WASH);
  }, Timeout.GET);
};

makeTheDish();
```

</details>

<details>
<summary>How to cook a dish using promises and timeouts?</summary>

- we have the promise to get a dinner (money to buy some food)
- the fact that we have the money gives us an opportunity to get the dinner
- but it happens not right away (we have to get the products and cook them)
```JavaScript
const Timeout = {
  GET: 9000,
  WASH: 3000,
  CUT: 8000,
  ADD_SPICES: 1000,
  COOK: 5000
};

const getProducts = () => {
  console.log('1. Getting the products');

  return new Promise((resolve) => {
    setTimeout(() => {
      const products = ['pumpkin', 'tomato', 'celery', 'spices', 'nuts'];
      resolve(products);
    }, Timeout.GET);
  });
};

const washProducts = (products) => {
  console.log('2. Washing the products');

  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(products);
    }, Timeout.WASH);
  });
};

const cutProducts = () => {
  console.log('3. Cutting the products');

  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(products);
    }, Timeout.CUT);
  });
};

const addSpices = () => {
  console.log('4. Adding the spices');

  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(products);
    }, Timeout.ADD_SPICES);
  });
};

const cookTheDish = () => {
  console.log('5. Cooking the dish');

  return new Promise((resolve, reject) => {
    setTimeout(() => {
      return Math.random() > 0.5
        ? resolve('Ready to eat!')
        : reject('Overcooked!');
    }, Timeout.COOK);
  });
};

getProducts()
  .then(washProducts)
  .then(cutProducts)
  .then(addSpices)
  .then(cookTheDish)
  .then((result) => console.log(result))
  .catch((error) => console.log(error));
```

</details>

## Asynchronous JavaScript, Http requests
<details>
<summary>What is async in JS?</summary>

- async in JS is about two activities, where one activity triggers another, which will be completed in future
- async - run the operation without blocking the main script process

</details>

<details>
<summary>What is AJAX?</summary>

- Asynchronous JavaScript And XML
- is used to communicate between client and server

</details>

<details>
<summary>What is the event loop and how it works?</summary>

- JS is single threaded
- browser is multi threaded
- all kind of async tasks (like timers, event listeners, etc) are going to browser (message queue)
- micro - promises (run first), macro - timeouts (run second)
- when the call stack is empty, event loop goes through message queue and executes the functions from there

</details>

<details>
<summary>How to implement synchronous data loading using AJAX?</summary>

```JavaScript
const getResponse = (url) => {
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url, false);
    xhr.send();
    // we can do it like that, because it's a sync request
    // return will happen after we get the response
    return xhr.response;
};
const data = getResponse('https://data.com/users');
```

</details>

<details>
<summary>When is the xhr.onreadystatechange called?</summary>

- whenever there is a change in the HttpConnection

</details>

<details>
<summary>What is the xhr.readyState?</summary>

- tells about the state of the HttpConnection
- changes its value (0-4) whenever there is any change in the connection and request
- 3 - data starts coming from the server
- 4 - all the data has come, server has processed the request completely, the connection is closed, at this moment we can check if our request was processed successfully or if there was an error

</details>

<details>
<summary>How was async request implemented in ES5 and what are the issues?</summary>

- complex interface, have to add all possible callbacks, difficult to make optional manipulation for some cases
- difficult to read the code, recreate the methods sequence is quite hard
- callback hell - several chained async methods turn into nested sequences of callbacks, too hard to support (ex: when we want to get several data structures from the server, depending on each one - users => articles => comments) https://callbackhell.ru/
```JavaScript
const getResponse = (url, onload, onerror) => {
  const xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.onload = () => onload(xhr.response);
  xhr.onerror = () => onerror(xhr.status);
  xhr.send();
};

getResponse('data.json',
  (response) => console.log(response),
  (errorStatus) => console.log(errorStatus)
);
```

</details>

<details>
<summary>How is async implemented in ES6?</summary>

- promise is a way to work with an async function as if it's sync
- can be resolved or rejecter only one time
- different states of a promise object
<img src="../images/promise.jpg" alt="promises" width="400">

```JavaScript
// inside async function:
// 1 - Promise object is created
// 2 - async function returns this Promise
// 3 - calls the resolve/reject callbacks
const getResponse = (url) => new Promise(
  // the executor function runs immediately
  (resolve, reject) => {
    console.log('Will be logged upon the promise creation.');
    // the async code should be written inside the executor function
    // it will be sent to the queue immediately

    // the state of the promise is changed automatically
    // depends on which callback we call (resolve or reject)
    // we can't go back to the previous state (can't call both callbacks)
    resolve('success');
    // will be executed but won't affect the state (stays fulfilled)
    reject('error');

    // Object => Pending...
    // neither then() or catch() executes at this moment
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    // Object => Fulfilled
    // then() executes
    xhr.onload = () => resolve(xhr.response);
    // Object => Rejected
    // catch() executes
    xhr.onerror = () => reject(xhr.status);
    xhr.send();
  }
);

// outside async function:
// 1 - call the function and get the Promise object
// 2 - attach the success and error handlers using then and catch
getResponse('data.json')
  // then method lets you to define a callback on success (fulfilled)
  // could work with several promises
  // returns new Promise()
  .then(
    // pass the resolve callback
    (data) => console.log(data),
    // pass the reject callback
    // but better to use catch
    (error) => console.warning(error)
  );

getResponse('data.json')
  // if there is anywhere in then chain reject is called
  // it's going to be caught in catch and all thens in between skipped
  .then((data) => console.log(data))
  // catches all the errors before
  // the blocks before are skipped but
  // doesn't stop the chain (if there are some then after)
  // returns new Promise()
  .catch((error) => console.warning(error))
  // if there are no more then() blocks left
  // promise enters the final mode: settled
  // once settled, you can use the special block finally()
  // to do some cleanup work
  // this block is reached anyways (resolve or reject before)
  // optional, executes always
  // will not return a promise in the end (like then() and catch())
  .finally(cb);

// you can work with promises chaining then
// every then returns a promise, where we can also call then
// every next then can get the result of the callback
// from the previous then
Promise.resolve('a') // 'a'
  .then((val) => val.concat('b')) // 'ab'
  // when we have another then() or catch()
  // the promise re-enters pending mode
  .then((val) => val.concat('c')) // 'abc'
  .then((val) => val.concat('d')); // 'abcd'
```

</details>

<details>
<summary>What are Promise.resolve and Promise.reject and why do you use them?</summary>

- static methods let you immediately change the promise state to fulfilled or rejected
```JavaScript
// both return a promise
const getData = () => Promise.resolve('Some data');
// the same as
const getData = () => new Promise((resolve) => resolve('Some data'));
// and reject
const getDataR = () => Promise.reject('Error!');
// the same as
const getDataR = () => new Promise((resolve, reject) => reject('Error!'));

getData() 
  .then((data) => console.log(data))
  .then(getDataR)
  .catch((error) => console.log(error));
```

</details>

<details>
<summary>What is Promise.race?</summary>

```JavaScript
const getData = (number) => new Promise((resolve) => setTimeout(() => {
  resolve(`Get data ${number}`);
}, 5000));

const getFirst = getData(1);
const getSecond = getData(2);
const getThird = getData(3);

// returns a new promise which will be
// fulfilled - after the fastest is fulfilled
// the other promises are not canceled!
// just ignored (in case of the http request will still be sent)
Promise.race([getFirst, getSecond, getThird])
  // => 'Get data 1'
  .then(valueFastest => console.log(valueFastest));
```

</details>

<details>
<summary>What is Promise.all?</summary>

```JavaScript
// used when we first to wait for some async operations
// to complete and then start working with the data
const getData = (number) => new Promise((resolve) => setTimeout(() => {
  resolve(`Get data ${number}`);
}, 5000));

const getFirst = getData(1);
const getSecond = getData(2);
const getThird = getData(3);

// the only parameter - an array of promises
// returns a new promise which will be
// fulfilled - after all the promises in the array are fulfilled
// rejected - if only one is rejected
Promise.all([getFirst, getSecond, getThird])
  // meets the order in the .all array
  // => ['Get data 1', 'Get data 2', 'Get data 3']
  .then((value) => console.log(value));
```

</details>

<details>
<summary>What is the difference between Promise.all and Promise.allSettled?</summary>

- when you need an array of requests at the same time 
  - `Promise.all(<Array.Promise>)`
    - executed when all the promises are resolved
    - if one with error, drops, can't access the data
    - returns an array
  - `Promise.allSettled(<Array.Promise>)`
    - waits till all the promises are completed (success/error)
    - can access the data even when some promises complete with an error
    - poor browser support
- `Promise.then` could return
  - just value/array - goes to the next promise
  - object Promise
  - array of values / promises - can turn into something else

</details>

<details>
<summary>What is async await?</summary>

- uses promises under the hood
- can be used only with functions
```JavaScript
// can't use like that
await setTimer(1000);
// but can wrap into IIFE
(async function() {
  await setTimer(1000);
})();
```
- when `async` is added, function automatically returns a promise
- wraps everything inside into a promise
```JavaScript
const setTimer = async () => {
  // waits till the promise is resolved and goes to the next line
  const data = await getData();
  const otherData = await getOtherData();
  // won't get executed till the await block resolved
  // as if wrapping into then() block
  console.log('Done!');
  // returns promise
};

async function setTimer() {
  // to handle errors can use try ... catch
  try {
    // if anything here yields an error,
    // the block fails into the catch
    // if error is in the 1st line, 2nd won't be executed
    const data = await getData();
    const otherData = await getOtherData();
  } catch (error) {
    console.log(error);
  }
  // this code will be executed anyways
  console.log('Done!');
  // returns promise
}

// creates a wrapping promise
function setTimer() {
  return new Promise((resolve, reject) => {
    // all the code here
  });
}
```
- `await` wraps everything into a `then()` block
- not good for cases when we need to run some code and not wait for promise to resolve or reject

</details>

<details>
<summary>How to send the http request with XMLHttpRequest?</summary>

```JavaScript
// can be used on its own
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://google.com');
xhr.send();

// or inside a function
const sendRequest = (method, url) => {
  const xhr = new XMLHttpRequest();

  xhr.open(method, url);
  xhr.responseType = 'json';
  // to add more headers use the method multiple times
  xhr.setRequestHeader('Content-Type', 'application/json');
  
  // to get and use the data have to listen to onload event
  // for XHR .addEventListener is not supported in some browsers
  xhr.onload = function() {
    // check if the status is success
    if (xhr.status >= 200 && xhr.status < 300) {
      // JSON data (mostly, depends on server)
      console.log(xhr.response);
      // either parse JSON.parse(...)
      // or configure responseType (will be parsed automatically)
    } else {
      console.log(xhr.response);
      console.log('Something went wrong.');
    }
  };
  
  // not for sent requests (when we get a response)
  // only for the errors of sending the request
  // like timeout or wasn't sent
  xhr.onerror = function() {
    console.log(xhr.response);
    console.log(xhr.status);
  };
  
  xhr.send();
};

// with using a promise
const sendHttpRequest = (method, url, data) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();

    xhr.setRequestHeader('Content-Type', 'application/json');
    xhr.open(method, url);
    xhr.responseType = 'json';

    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.response);
      } else {
        reject(new Error('Something went wrong!'));
      }
    };

    xhr.onerror = function() {
      reject(new Error('Error while sending a request!'));
    };

    xhr.send(JSON.stringify(data));
  });
};

const fetchPosts = () => {
  sendHttpRequest('GET', 'https://...')
    .then(responseData => console.log(responseData))
    .catch(error => console.log(error));
};

const addPosts = async () => {
  try {
    const responseData = await sendHttpRequest(
      'POST',
      'https://...',
      post
    );
  } catch (error) {
    console.log(error);
  } 
};
```

</details>

<details>
<summary>How to use fetch API?</summary>

- `fetch` is a wrapper around promise
- function for sending/fetching data (`XMLHttpRequest` under hood)
```JavaScript
// response.json(); returns promise
// resolves when the string will parse json into an object
// if no 2nd param, get request, returns Promise
// resolves into response object
// if fetch => error, but the response is received,
// fetch doesn't count it as a throw new Error (for catching inside catch)
// and returns that response into then
// because the request is fulfilled and response received from server
// 404 / redirect / etc - for fetch those are normal server responses
// so have to add our own status handling
fetch('https://data.com', {
  method: 'POST',
  body: JSON.stringify({
    'date': Date.now(),
    'time': 402,
    'lives': 3
  }),
  headers: {
    'Content-Type': 'application/json'
  }
});

const sendHttpRequest = (method, url, data) => {
  // returns a JSON (unparsed), have to parse
  // with .json() available in fetch API
  return fetch(url, {
    method: method,
    body: JSON.stringify(data)
  })
    .then(response => {
      if (response.status >= 200 && response.status < 300) {
        return response.json();
      } else {
        // if we need the response, error handling could be tricky
        return response.json()
          .then(errorData => {
            console.log(errorData);
            throw new Error('Something went wrong on the server side!');
          });
      }
    })
    .catch(error => {
      console.log(error);
      throw new Error('Something went wrong with the request!');
    });
};
```

</details>

<details>
<summary>How to send the cross domain request?</summary>

- both require some server changes
- using CORS
- using JSONP

</details>

<details>
<summary>What is CORS?</summary>

- CORS is the new way to deal with cross origin AJAX request
- to enable CORS response should contain Access-Control-Allow-Origin header with the domain value or `*` to work with any domain

</details>

<details>
<summary>What is JSONP and when do we use it?</summary>

- if CORS can't be enabled by server or for old browsers
- uses script tag to get the data from the server
- script is allowed to be fetched from any domain, so we need to create a script with the url as src and the server has to wrap the response in a callback function
- response sent by server is actually a JS code which contains data inside a wrapper function
- <b>there is no ajax call being made</b>

</details>

<details>
<summary>What are the good parts for feedback in the UI?</summary>

- When you sync data with a server, don't change control state, change only if the request was successful (returned 200+ codes)
- View => Model => Server => Model => View
- click on favorites - gone on update, if there was an error response from server
- comment doubles if you don't disable the submit button

</details>

<details>
<summary>Learn more</summary>

- [ ] [HTTPS on Wiki](https://en.wikipedia.org/wiki/HTTPS)
- [ ] [JavaScript Promises: An introduction](https://web.dev/promises/)
- [ ] [async function on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [ ] [HTTP request methods on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [ ] [HTTP Messages on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
- [ ] [HTTP response status codes on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [ ] [HTTP Headers on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [ ] [Using XMLHttpRequest on MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
- [ ] [Fetch API on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [ ] [Using files from web applications on MDN](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
- [ ] [MDN: HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
- [REST client for VS Code](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
- [Data prototyping service (mocks)](https://jsonplaceholder.typicode.com)

</details>

## Meta-programming
<details>
<summary>When do you need to use meta-programming?</summary>

- advanced concepts used mostly when you create libraries

</details>

<details>
<summary>What are Symbols and how to use them?</summary>

- primitive value (represents a unique identifier)
- used as keys in objects
- built-in symbols and creatable symbols
- uniqueness is guaranteed
- do not auto-convert to a string
- skipped by `for ... in` loop, `Object.keys`
```JavaScript
const userId = Symbol(); // => Symbol()
// can give a name
// mostly useful for debugging (symbol with the description 'id')
const playerId = Symbol('id');
console.log(playerId.toString()); // => Symbol(id)

const player = {
  [playerId]: 1, // can't access this property out of library
  name: 'Harry',
  level: 11
};

// can use inside the library
player[playerId] = 2;

console.log(playerId === Symbol('id')); // => false

// built-in symbol
const user = {
  name: 'Ron',
  level: 9,
  [Symbol.toStringTag]: 'User'
};

console.log(user.toString()); // => [object User]
```

</details>

<details>
<summary>What are global symbols?</summary>

```JavaScript
// read or create in the global registry
const id = Symbol.for('id');
const id2 = Symbol.for('id');
const idNotGlobal = Symbol('id');
// true
console.log(id === id2);
// id
console.log(Symbol.keyFor(id));
// undefined
console.log(Symbol.keyFor(idNotGlobal));
// id
console.log(idNotGlobal.description);
```

</details>

<details>
<summary>What is an Iterator and how to use it?</summary>

- iterator is an object which has `next()` method
```JavaScript
const player = {
  currentFriend: 0,
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  // we can have a next method without iterator function
  next() {
    if (this.currentFriend >= this.friends.length) {
      return {value: this.currentFriend, done: true};
    }

    const result = {
      value: this.friends[this.currentFriend],
      done: false
    };

    this.currentFriend++;
    return result;
  }
};

console.log(player.next());
console.log(player.next());
console.log(player.next());
console.log(player.next());

// still can't use for loop, but while is ok
let friend = player.next();

while(!friend.done) {
  console.log(friend.value);
  friend = player.next();
}
```

</details>

<details>
<summary>How to create an iterable and why?</summary>

- to work with `for ... of` loop
- iterables use it internally
- infinite iterable is also possible, can use `break` to stop
```JavaScript
// the core feature of iterables is the separation of concerns
// the player itself doesn't have the next()
// instead another object (iterator) is created player[Symbol.iterator]()
// and next() generates the values for the iteration
const player = {
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  // 1. when for...of starts, it calls this once
  // must return an iterator (an object with method next)
  [Symbol.iterator]: function() {
    // 2. onward for...of works only with this iterator object
    // asking it for the next values
    return {
      currentFriend: 0,
      friendList: this.friends,
      // 3. next() is called on each iteration of the for...of loop
      next() {
        // 4. should return an object of type
        // {done: Boolean, value: any}
        if (this.currentFriend >= this.friendList.length) {
          return {done: true, value: this.currentFriend};
        }

        const result = {
          done: false,
          value: this.friendList[this.currentFriend]
        };

        this.currentFriend++;
        return result;
      }
    };
  }
};

// we can merge iterator and player to make the code simpler
// the downside - impossible to have two for...of loops
// running over the object simultaneously: they’ll share the iteration state
// because there’s only one iterator – the object itself
// but two parallel for-ofs is a rare thing, even in async scenarios
const player2 = {
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],

  next() {
    if (this.currentFriend >= this.friends.length) {
      return {done: true, value: this.currentFriend};
    }

    const result = {
      done: false,
      value: this.friends[this.currentFriend]
    };

    this.currentFriend++;
    return result;
  },
  
  [Symbol.iterator]() {
    this.currentFriend = 0;
    return this;
  }
};

for (let friend of player) {
  console.log(friend);
}
```

</details>

<details>
<summary>How to call an iterator explicitly?</summary>

```JavaScript
const text = 'Hello';
// the same as for...of
const iterator = text[Symbol.iterator]();

while (true) {
  const result = iterator.next();

  if (result.done) {
    break;
  }

  console.log(result.value);
}
```

</details>

<details>
<summary>What are Generators and how to use them?</summary>

- using generators to build an iterator object
- generator is special function which generates an iterator
- returns an object with `next()` method
```JavaScript
const player = {
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
  // value should be an iterator
  // returns an object with next() method
  [Symbol.iterator]: function* friendGenerator() {
    // we can have both, generator and separate next() method
    let currentFriend = 0;

    while(currentFriend < this.friends.length) {
      // almost like return
      // pauses the execution on first call
      // and continues on second and so on
      // that's why we get different values
      yield this.friends[currentFriend];
      currentFriend++;
    }
  }
};

// now we can use loops
// for loop and some other (like spread)
// look for the [Symbol.iterator] function
// so all iterables have it by default
for (let friend of player) {
  console.log(friend);
}

console.log([...player]);

// if instead of [Symbol.iterator] different name is used
// can use it like that
// in this case value is the same (we generate new generator)
console.log(player.getFriend().next());
console.log(player.getFriend().next());
console.log(player.getFriend().next());

// but if we store it, the value will be different
const friendsIterator = player.getFriend();

console.log(friendsIterator.next());
console.log(friendsIterator.next());
console.log(friendsIterator.next());
```

</details>

<details>
<summary>What is Reflect API and how to use it?</summary>

- API to control objects
- standardized and grouped methods
- control code usage/impact
- has the same methods and properties as `Object`, but `Reflect` is new and has more methods
  - better error handling (`Object` sometimes returns undefined or just fails silently)
  - all the methods are present (`Object` doesn't have delete property method, have to use `delete obj.prop;`)
- gives a handful of methods to change object on a meta level
```JavaScript
const player = {
  name: 'Harry Potter'
};

Reflect.setPrototypeOf(player, {
  toString() {
    return this.name;
  }
});
```

</details>

<details>
<summary>What is Proxy API and how to use it?</summary>

- create traps for object operations
- step in and execute code
- control code usage/impact
```JavaScript
const player = {
  name: 'Harry Potter'
};

const playerHandler = {
  // executes when somebody tries to read a value
  // arguments are passed automatically by Proxy API
  get(obj, propertyName) {
    console.log(propertyName);
    return obj[propertyName] || 'NOT FOUND';
  },

  // executes when we try to set a value
  set(obj, propertyName, newValue) {
    if (propertyName === 'age') {
      return;
    }

    obj[propertyName] = newValue;
  }
};

// new Proxy(object, handlers)
const proxyPlayer = new Proxy(player, playerHandler);

console.log(proxyPlayer.name);
// => name
// => Harry Potter
console.log(proxyPlayer.age); // => NOT FOUND
proxyPlayer.age = 10;
// because of the set trap
console.log(proxyPlayer.age); // => NOT FOUND
```

</details>

<details>
<summary>Learn more</summary>

- [ ] [Symbol on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [ ] [Iterators and Generators on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)
- [ ] [Reflect API on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)
- [ ] [Proxy API on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

</details>

## Performance and optimizations
<details>
<summary>How does the code parse, compiles, executes?</summary>

<img src="../images/code-parsing.png" alt="Code parsing">

<img src="../images/heap-stack.png" alt="Heap, stack (how JS engine works)">

- JS is single-threaded
- event loop is not a JS-engine feature (only heap and stack - simple sync code), it's a browser feature

</details>

<details>
<summary>What are Primitive and Reference values?</summary>

- primitive - strings, numbers, booleans, `null`, `undefined`, symbol
  - stored in a memory (normally on stack)
  - variable stores the value itself
  - copying a variable copies the value
- reference - all other objects (more expensive to create)
  - stored in a memory (heap)
  - variable stores a pointer (address) to location in memory
  - copying a variable copies the pointer (reference)

</details>

<details>
<summary>How do the Garbage collection and Memory management work?</summary>

- the stack is cleared automatically (mostly ok)
- the heap may overflow more frequently
  - if exceeded the allocated memory for the browser (chrome crashes the site, but the app still runs)
  - no need to manually manage in most cases
- V8 garbage collector
  - periodically checks the heap for unused objects (objects without references) and removes them
  -  if we put a reference type into an array (or other structure), then while the array is alive, the object will be alive as well
```JavaScript
let player = {name: 'John'};
const map = new Map();

map.set(player, 1);

// even if we set the value of player to null
player = null;
// the object will be accessible
map.keys();
// but works different with WeakMap 
// (the object is removed when it is set to null)
```
- memory leaks (due to unused objects you still hold the reference to)
```JavaScript
function printMsg() { ... }

function addListener() {
  // JS replaces the function, the listener is only one
  button.addEventListener('click', printMsg);

  // JS adds the new listener every time
  button.addEventListener('click', function() { ... });
}
```

</details>

<details>
<summary>Learn more</summary>

- [Reference vs Primitive values](https://academind.com/learn/javascript/reference-vs-primitive-values/)
- [Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
- [JavaScript V8 Engine Explained](https://hackernoon.com/javascript-v8-engine-explained-3f940148d4ef)
- [Getting garbage collection for free](https://v8.dev/blog/free-garbage-collection)

</details>

## Security
<details>
<summary>What are the Potential Security Holes?</summary>

- security details in the code (like connection strings, keys, user data)
- keep in mind that JS code could be read by everyone
- security relevant details can be read
- ex: database access credentials exposed in code (not the issue with google API Key, can restrict that)

</details>

<details>
<summary>What are the XSS Attacks?</summary>

- attack pattern when malicious JS code gets injected and executed
- injected code can do anything your code could do as well
- vary dangerous, gives full control for hackers
- ex: unchecked user-generated content
```HTML
<!-- new versions of browsers don't execute -->
<script>alert('Hello!');</script>
<!-- always runs -->
<img src="" onerror="alert('Hello!');">
```
- use `textContent` instead of `innerHTML` if possible
- use packages like `sanitize-html`, also validate on server side
- use the third party libraries you trust

</details>

<details>
<summary>What is the Cross-Site Request Forgery (CSRF)?</summary>

- attack pattern that depends on injected content (ex: images)
- requests to malicious servers are made with user's cookies
- actions can be executed without the user knowing
- ex: malicious image URL, XSS
- mostly backend security issue (CSRF token to deal with the issue)
<img with="500" src="./images/csrf.png">

</details>

<details>
<summary>What is the Cross-Origin Resource Sharing (CORS)?</summary>

- not an attack pattern but a security concept
- requests are only allowed from the same origin (domain)
- controlled via server-side response headers and browser
- ex: JS modules (that's why we need to run a server - are only allowed if modules are from the same server)

</details>

## Regular expressions
<details>
<summary>Some common cases</summary>

- `myRegEx.test(myString);` to check if any part of the string matches
- `myString.match(myRegEx);` to check if there is this part in a string and extract it (returns `['matching part']`)
- case matters `/Kevin/` !== `/kevin/`
- add `i` flag to ignore the case `/kevin/i`
- add `g` flag to search or extract a pattern more than once `/little/g`, match returns `['match', 'match']` or more items
- to alternate search use `|` `/yes|no/`
- if you wanted to match "hug", "huh", "hut", and "hum", you can use the regex `/hu./` to match all four words (wildcard `.` matches any one character)
- `/[abc]/` character classes to define a group of characters you wish to match, ex "bag", "big", and "bug" but not "bog" `/b[aiu]g/`
- `/[a-e]/` works the same as character classes but given a group of characters to match
- `/[0-9]/` for numbers
- `/[a-e0-9]/` for numbers and letters
- `/[^aeiou]/gi` to create a negated character set, you place a caret character after the opening bracket and before the characters you do not want to match
- `+` the character or pattern has to be present consecutively (the character has to repeat one after the other) `/a+/g` will match 
  - `['a']` - `"abc"`
  - `['aa']` - `"aabc"`
  - `['a', 'a']` - `"abab"`
- `*` for 0 or more occurrence `/go*/`
- `/t[a-z]*i/` is greedy and matches the largest substring, ex `titanic` => `['titani']`
- `/t[a-z]*?i/` lazy matching `titanic` => `['ti']`
- `/^a/` matches the beginning of a string
- `/a$/` matches the ending of a string
- `/\w/` === `/[A-Za-z0-9_]/`
- `/\W/` the opposite to `/\w/`
- `/\d/` for numbers and `/\D/` is an opposite
- `/\s/` not only matches whitespace, but also carriage return, tab, form feed, and new line characters === character class `/[ \r\t\f\n\v]/` `/\S/` is an opposite
- `/a{3,5}h/` to match only the letter a appearing between 3 and 5 times in the string "ah"
- `/ha{3,}h/` to specify only the lower count
- `/ha{3}h/` exact number of matches
- `/u?/` checks for zero or one of the preceding element, you can think of this symbol as saying the previous element is optional
- `/q(?=u)/` => `['q']` positive lookahead will look to make sure the element in the search pattern is there, but won't actually match it
- `/q(?!u)/` => `['q']` negative lookahead will look to make sure the element is not there, won't match it
- `/(a|b)/` are used to group patterns
- () are used to find repeat substrings
- `/(\w+)\s\1/` matches any word that occurs twice separated by a space, `.match()` method on a string will return an array with the string it matches, along with its capture group

</details>

<details>
<summary>Learn more</summary>

- [8 полезных регэкспов с наглядным разбором](https://habr.com/ru/post/66931/)
- [Regex testing service](https://regex101.com/)
- [A collection of different regexps](http://html5pattern.com/)
- Mastering Regular Expressions (O'Reilly, by Jeffrey Friedl)

</details>

## Deploying

## Testing

## Debugging
<details>
<summary>What are the common console methods?</summary>

```JavaScript
console.log();
console.debug();
console.error();
console.info();
console.warn();
```

</details>

<details>
<summary>How to console log as an object instead of the html tree?</summary>

- if by default logs the html tree, use to log as an object
```JavaScript
console.dir(document);
```

</details>

<details>
<summary>How to console log as a table?</summary>

- for nice table overview
```JavaScript
console.table([1, 2, 3]);
```

</details>

<details>
<summary>How to clear the console?</summary>

```JavaScript
console.clear();
```

</details>

<details>
<summary>Learn more</summary>

- [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- [Get Started with Debugging JavaScript in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript/)
- [A Guide to Console Commands](https://css-tricks.com/a-guide-to-console-commands/)

</details>

## Browser support
<details>
<summary>Feature detection and fallbacks</summary>

```JavaScript
// if not supported === undefined
if (navigator.clipboard) {
  navigator.clipboard.writeText('Some text to copy.')
    .then(result => console.log(result))
    .catch(error => console.log(error));
} else {
  console.log('Feature is not available, try to copy manually.');
}
```

</details>

<details>
<summary>Transpiling the code</summary>

- something like babel could be integrated into webpack config `modules`
- set browsers list in `package.json`

</details>

<details>
<summary>Polyfills</summary>

- can add manually
- and also with babel it's available to add an auto detection

</details>

<details>
<summary>If JavaScript is off in the browser</summary>

- at least use `<noscript>Please turn on the JavaScript support.</noscript>` 

</details>

<details>
<summary>Learn more</summary>

- [ ] [What is Babel?](https://babeljs.io/docs/en/)
- [ ] [Babel loader](https://github.com/babel/babel-loader)
- [ ] [@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env)
- [ ] [core-js](https://github.com/zloirock/core-js)

</details>

## Tools and workflow
<details>
<summary>Learn more</summary>

- [Introduction to JavaScript Source Maps](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)

</details>

## Libraries
<details>
<summary>Working with dates</summary>

- [Flatpickr](https://flatpickr.js.org/getting-started/)
- [Moment.js](https://momentjs.com/)

</details>

<details>
<summary>Animations</summary>

- [Mojs](https://mojs.github.io/)

</details>

<details>
<summary>Charts</summary>

- [Chart.js](https://www.chartjs.org/)

</details>

<details>
<summary>Security</summary>

- [He.js](https://github.com/mathiasbynens/he)

</details>

<details>
<summary>Maps</summary>

- [OpenLayers](https://openlayers.org/en/latest/doc/quickstart.html)

</details>

## Frameworks

- [ ] [Angular vs React vs Vue](https://academind.com/learn/angular/angular-vs-react-vs-vue-my-thoughts/)

## Resources
<details>
<summary>Read</summary>

- [JavaScript Garden](http://shamansir.github.io/JavaScript-Garden/)

</details>

<details>
<summary>Practice</summary>

- [JavaScript Questions](https://github.com/lydiahallie/javascript-questions)
- [Codewars](https://www.codewars.com/dashboard)
- [FreeCodeCamp](https://www.freecodecamp.org/)
- [HackerRank](https://www.hackerrank.com/dashboard)
- [CodinGame](https://www.codingame.com/)

</details>

<details>
<summary>Create</summary>

- [Responsive and Dynamic Progress Bar with HTML, CSS, and JavaScript](https://www.freecodecamp.org/news/how-to-build-a-responsive-and-dynamic-progress-bar/)

</details>

<details>
<summary>Courses</summary>



</details>

<details>
<summary>Books</summary>

- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS) by Kyle Simpson
- [Head First JavaScript Programming (O'Reilly, by Elisabeth Robson, Eric Freeman)
- [JavaScript: The Definitive Guide (O'Reilly, by David Flanagan)
- [JavaScript: The Good Parts (O'Reilly, by Douglas Crockford)
- [JavaScript Patterns (O'Reilly, by Stoyan Stefanov)

</details>