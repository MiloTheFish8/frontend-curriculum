# Review progress and questions I have to review
## 26, ..., 22 Mar 2021 (29 Mar)
### JavaScript
<details>
<summary>When do you need to use meta-programming?</summary>

- advanced concepts used mostly when you create libraries

</details>

<details>
<summary>What are Symbols and how to use them?</summary>

- primitive values
- used as keys in objects
- built-in symbols and creatable symbols
- uniqueness is guaranteed
```JavaScript
const userId = Symbol(); // => Symbol()
const playerId = Symbol('id'); // => Symbol(id)

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

## 01, ..., 25 Mar 2021 (01 Apr)
### JavaScript
<details>
<summary>What are Iterators and how to use them?</summary>

- create your own iterable values
- iterables use it internally
- iterator is an object which has `next()` method
```JavaScript
const player = {
  currentFriend: 0,
  name: 'Harry',
  friends: ['Ron', 'Hermione', 'Luna'],
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

## 02, ..., 26 Mar 2021 (02 Apr)
### JavaScript
<details>
<summary>What is API?</summary>

- API (Application Public Interface)
  - a set of available properties and methods to solve a particular task
  - frequent implementation - objects

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

## 03, ..., 27 Mar 2021 (03 Apr)
### JavaScript
<details>
<summary>How to create an Array?</summary>

```JavaScript
// ES5
// 1
var numbers = new Array(3, 5); // => [3, 5]
var emptyArray = new Array(3); // => [] with length === 3
// 2
var numbers2 = Array(3, 5);
var emptyArray2 = Array(3);
// 3
var letters = ['a', 'r']; // => ['a', 'r']
// 4 clones array and adds values from another array
const newNumbers = numbers.concat([8, 5, 2]);

// ES6+
// 5 makes an array of any iterable (collection, separate values)
const elements = Array.from(document.querySelectorAll('li'));
const letters = Array.from('string');
// 6 of separate values
const values = Array.of(1, 2, 3);
// 7
const items = [...elements, ...values];
```

</details>

<details>
<summary>How to make an Array of a string?</summary>

```JavaScript
const text = 'One two three';
const words = text.split(' '); // => ['One', 'two', 'three']
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
<summary>How to delete or add an element from (to) an Array at any position?</summary>

- change the initial array
```JavaScript
const numbers = [1, 2, 5];
// start index, delete count, value to add (or more 10, 15)
const removedElements = numbers.splice(1, 0, 10); // => [1, 10, 2, 5]
// removes from the end
const removedElements2 = numbers.splice(-1, 1); // => [1, 2]
// will delete all items starting with the provided index
const removedElements3 = numbers.splice(0);
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

## 06, ..., 23 Mar 2021 (30, 06 Apr)
### Angular
<details>
<summary>How to intercept input property changes with a setter?</summary>

```TypeScript
// app/components/child/child.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent {
  private _fieldLabel = '';
  @Input() 
  get fieldLabel(): string { return this._fieldLabel; };
  set fieldLabel(fieldLabel: string) {
    this._fieldLabel = (fieldLabel && fieldLabel.trim()) || 'Unknown Label';
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<!-- E-mail -->
<app-child fieldLabel="E-mail"></app-child>
<!-- Unknown Label -->
<app-child fieldLabel="  "></app-child>
```

</details>

<details>
<summary>How to intercept input property changes with OnChanges and why?</summary>

- you may prefer this approach to the property setter when watching multiple, interacting input properties
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p></p>'
})
export class ChildComponent implements OnChanges {
  @Input() level: number;
  @Input() power: number;
  changeLog: string[] = [];

  ngOnChanges(changes: SimpleChanges) {
    const log: string[] = [];

    for (const propName in changes) {
      const changedProp = changes[propName];
      const to = JSON.stringify(changedProp.currentValue);

      if (changedProp.isFirstChange()) {
        log.push(`Initial value of ${propName} set to ${to}`)
      } else {
        const from = JSON.stringify(changedProp.previousValue);

        log.push(`${propName} changed from ${from} to ${to}`);
      }
    }

    this.changeLog.push(log.join(', '));
  }
}

// app/components/parent/parent.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './'
})
export class ParentComponent {
  level: number = 1;
  power: number = 0;

  increasePower() {
    this.power++;
  }

  increaseLevel() {
    this.level++;
    this.power = 0;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<button type="button" (click)="increasePower()">Power Up</button>
<button type="button" (click)="increaseLevel()">Level Up</button>
<app-child [level]="level" [power]="power"></app-child>
```

</details>

<details>
<summary>How to pass data from child to parent (listen to child event)?</summary>

- the child exposes an `EventEmitter` property with which it emits events when something happens
- the parent binds to that event property and reacts to those events
```TypeScript
// app/components/child/child.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h2>{{ name }}</h2>
    <button 
      (click)="checkIn(true)" 
      [disabled]="haveChosen" 
      type="button"
    >Check In</button>
    <button 
      (click)="checkIn(false)" 
      [disabled]="haveChosen" 
      type="button"
    >I'm Out</button>
  `
})
export class ChildComponent implements OnChanges {
  @Input() name: string;
  @Output() checkedIn = new EventEmitter<boolean>();
  haveChosen = false;

  checkIn(isIn: boolean) {
    this.checkedIn.emit(isIn);
    this.haveChosen = true;
  }
}
```
```HTML
<!-- app/components/parent/parent.component.html -->
<app-child name="Harry" (checkedIn)="onCheckedIn($event)"></app-child>
```

</details>

<details>
<summary>How to use a local reference (inside one component) and what is the limitation?</summary>

- can be used only in the template, not in the component (.ts file)
- returns an HTML element
```HTML
<!-- simple.component.html -->
<input type="text" #locRef>
<button (click)="onButtonClick(locRef)" type="button">Get the input HTML</button>
<p>{{ locRef.value }}</p>
```

</details>

<details>
<summary>How to interact parent > child via local variable (reference) and what is the limitation?</summary>

- parent component cannot use data binding to read child properties or invoke child methods
- can do both by creating a template reference variable for the child element and then reference that variable within the parent template
- accessible only from the template, not from the parent component itself
```TypeScript
// child.component.ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p>{{ message }}</p>'
})
export class ChildComponent {
  message: string = '';

  start() {
    this.message = 'Start in 10 seconds.';
    // some countdown code
  }

  stop() {
    this.message = 'Stopped!';
    // stop the timer code
  }
}
```
```HTML
<!-- parent.component.html -->
<app-child #childComponent></app-child>
<p>{{ childComponent.message }}</p>
<button (click)="childComponent.start()" type="button">Start</button>
<button (click)="childComponent.stop()" type="button">Stop</button>
```

</details>

## 09, ..., 26 Mar 2021 (02, 09 Apr)
### JavaScript
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

## 10, ..., 27 Mar 2021 (03, 10 Apr)
### JavaScript
<details>
<summary>Why a Map, not just an Object?</summary>

- any keys possible
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

// or with iterable
const pairs = new Map([['John', 'May'], ['Ichigo', 'Rukiya']]);
```

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
```

</details>

## 12, ..., 22 Mar 2021 (29, 05, 12 Apr)
### JavaScript
<details>
<summary>What data structures could be used as a key in an Object?</summary>

- strings
- numbers (positive int or floats)
- symbols

</details>

<details>
<summary>Is an Object iterable and how to iterate?</summary>

- not iterable (can use `for ... in` old loop, has some issues, not `for ... of`)

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

## 18, ..., 28 Mar 2021 (04, 11, 18 Apr)
### JavaScript
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
<summary>What is the arguments keyword in a function?</summary>

- don't have to pass as a parameter (accessible as a keyword inside any function)
- iterable structure
- arrow functions do not have arguments keyword

</details>

## 28 Mar 2021 (29, 30, 01, 03, 07, 14, 21, 28 Apr)