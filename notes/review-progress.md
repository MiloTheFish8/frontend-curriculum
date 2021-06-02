# Review progress
## 02 Jun 2021 (03, 05, 08, 15 Jun)
<details>
<summary>What is operand?</summary>

- what operators are applied to: 5 * 2 there are two operands: the left operand is 5 and the right operand is 2 (sometimes called arguments instead of operands)

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
<summary>What are the 'falsy' values?</summary>

- `0`
- `''`
- `NaN`
- `null`
- `undefined`

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

## 03 Jun 2021 (04, 06, 09, 16 Jun)
```JavaScript
&& ||
const name = '' || 'Mary'; // first true
const name = '' && 'Mary'; // first falsy
```