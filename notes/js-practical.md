# Practical Questions
- [Fundamentals](#fundamentals)
- [Data types and structures](#data-types-and-structures)
- [Functions](#functions)

## Fundamentals
### 1. What will be logged to the console?
```JavaScript
let counter = 1;
console.log(2 * ++counter);
```

<details>
<summary>Answer</summary>

- `4` - first `++`, returns the value, then `*`

</details>

### 2. What will be logged to the console?
```JavaScript
let counter = 1;
console.log(2 * counter++);
```

<details>
<summary>Answer</summary>

- `2` first returns the value then `*` and `++`
```JavaScript
// if you need multiply and then increase, more readable
console.log(2 * counter);
counter++;
```

</details>

### 3. What will be logged to the console?
```JavaScript
let a = (1 + 2, 3 + 4);
console.log(a);
```

<details>
<summary>Answer</summary>

- `7` the first expression `1 + 2` is evaluated and its result is thrown away, then `3 + 4` is evaluated and returned as the result

</details>

### 4. What will be logged to the console?
```JavaScript
let b = 1 + 2, 3 + 4;
console.log(b);
```

<details>
<summary>Answer</summary>

- `3` comma operator has very low precedence, lower than `=`. Evaluates `+` first, summing the numbers into `b = 3, 7` then the assignment operator assigns `b = 3` and the rest is ignored

</details>

### 5. What will be logged to the console?
```JavaScript
console.log('3' > 1);
console.log('04' == 4);
console.log(true == 1);
console.log(false == 0);

const a = 0;
const b = '0';
console.log(Boolean(a));
console.log(Boolean(b));
console.log(a == b);
```

<details>
<summary>Answer</summary>

- JS converts the values to numbers when using a compare operators
```JavaScript
console.log('3' > 1); // true
console.log('04' == 4); // true
console.log(true == 1); // true
console.log(false == 0); // true

// the strange thing because of conversion to a number
const a = 0;
const b = '0';

console.log(Boolean(a)); // false
console.log(Boolean(b)); // true
console.log(a == b); // true
```

</details>

### 6. What will be logged to the console?
```JavaScript
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);

console.log(a);
console.log(c);

let a, b, c;
a = b = c = 2 + 2;
console.log(a);
console.log(b);
console.log(c);

console.log(2 ** 2);
console.log(4 ** (1 / 2));
console.log(8 ** (1 / 3));
```

<details>
<summary>Answer</summary>

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

console.log(2 ** 2); // => 4 (2 pow 2)
console.log(4 ** (1 / 2)); // => square root
console.log(8 ** (1 / 3)); // => cubic root
```

</details>

### 7. How to compare with null or undefined?
```JavaScript
console.log(null === undefined);
console.log(null == undefined);

console.log(null > 0);
console.log(null == 0);
console.log(null >= 0);

console.log(undefined > 0);
console.log(undefined < 0);
console.log(undefined == 0);
```

<details>
<summary>Answer</summary>

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

### 8. How to use OR and AND?
```JavaScript
const userName1 = null && 'Mary';
const isLoggedIn = true;
const userName0 = isLoggedIn && 'Mary';
const userName2 = 'Lily' && 'Max' && 'Mary';
const userName1 = '' || 'Mary' || 'Maya';
const userName2 = 'Max' || 'Mary' || '';
const userName3 = null || 0 || '';
true || console.log('Will not be logged!');
false || console.log('Logged!');
```

<details>
<summary>Answer</summary>

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

### 9. What will be logged to the console?
```JavaScript
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);

console.log(a);
console.log(c);

let a, b, c;

a = b = c = 2 + 2;
console.log(a);
console.log(b);
console.log(c);

console.log(2 ** 2);
console.log(4 ** (1 / 2));
console.log(8 ** (1 / 3));
```

<details>
<summary>Answer</summary>

```JavaScript
// assignment returns a value
// x = value writes the value into x and then returns it
let a = 1;
let b = 2;
let c = 3 - (a = b + 1);

console.log(a); // => 3
console.log(c); // => 0

// chaining assignment
// evaluate from right to left
// 1. the rightmost expression 2 + 2 is evaluated 
// 2. and then assigned to the variables on the left: c, b and a
let a, b, c;

a = b = c = 2 + 2;
console.log(a); // => 4
console.log(b); // => 4
console.log(c); // => 4

console.log(2 ** 2); // => 4 (2 pow 2)
console.log(4 ** (1 / 2)); // => square root
console.log(8 ** (1 / 3)); // => cubic root
```

</details>

### 10. What will be logged to the console?
```JavaScript
let text1 = 'one' && 'two' ?? 'three';
let text2 = ('one' && 'two') ?? 'three';

console.log(text1);
console.log(text2);
```

<details>
<summary>Answer</summary>

```JavaScript
// Syntax error
let text = 'one' && 'two' ?? 'three';
// Works just fine (=> 'two')
let text = ('one' && 'two') ?? 'three';
```

</details>

### 11. What will be logged to the console?
```JavaScript
function greet() {
  console.log(message);

  var message = 'Hello!';
}
```

<details>
<summary>Answer</summary>

- `undefined` - the assignment doesn't hoist

</details>

### 12. What will be logged to the console?
```JavaScript
function greet() {
  message = 'Hello!';

  if (false) {
    var message;
  }

  console.log(message);
}
```

<details>
<summary>Answer</summary>

```JavaScript
function greet() {
  // even if the if block never executes,
  // the var hoists here anyways var message;
  // assigns to 'Hello!'
  message = 'Hello!';

  if (false) {
    var message;
  }
  // => "Hello!"
  console.log(message);
}
```

</details>

## Data types and structures

### 1. How to set a date?

## Functions

### 1. What will be logged to the console?
```JavaScript
function createCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let count = createCounter();

console.log(count());
console.log(count());
console.log(count());
```

<details>
<summary>Answer</summary>

- `0`, `1`, `2`

</details>

### 2. What will be logged to the console?
```JavaScript
function() {
  var message = 'Hello!';
  console.log(message);
}();
```

<details>
<summary>Answer</summary>

- `SyntaxError: Function statements require a function name` there will be an error because `function` in the FD must have a name

</details>

### 3. What will be logged to the console?
```JavaScript
function greet() {
  var message = 'Hello!';
  console.log(message);
}();
```

<details>
<summary>Answer</summary>

- `SyntaxError: Unexpected token ')'` JS doesn't allow the FD to be called immediately

</details>

### 4. What will be logged to the console?
```JavaScript
function greet() {}
console.log(greet.name);
```

<details>
<summary>Answer</summary>

- `greet`

</details>

### 5. What will be logged to the console?
```JavaScript
const greet = function() {};
console.log(greet.name);
```

<details>
<summary>Answer</summary>

- `greet` because of contextual name

</details>

### 6. What will be logged to the console?
```JavaScript
function do(greet = function() {}) {
  console.log(greet.name);
}
```

<details>
<summary>Answer</summary>

- `greet` because of contextual name

</details>

### 7. What will be logged to the console?
```JavaScript
const player = {
  logLevel() {},
  logName: function() {}
};
console.log(player.logLevel.name);
console.log(player.logName.name);
```

<details>
<summary>Answer</summary>

- `logLevel`, `logName` because of the contextual name

</details>

### 8. What will be logged to the console?
```JavaScript
const arr = [function() {}];
console.log(arr[0].name);
```

<details>
<summary>Answer</summary>

- `''` the engine has no way to set up the right name, so there is none

</details>

### 9. What will be logged to the console?
```JavaScript

```

<details>
<summary>Answer</summary>


</details>

### 10. What will be logged to the console?
```JavaScript

```

<details>
<summary>Answer</summary>


</details>

### 11. What will be logged to the console?
```JavaScript

```

<details>
<summary>Answer</summary>


</details>