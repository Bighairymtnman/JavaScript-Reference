# JavaScript Elements Quick Reference

## Table of Contents
- [Variables & Data Types](#variables--data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Functions](#functions)
- [Arrays & Objects](#arrays--objects)
- [DOM Manipulation](#dom-manipulation)
- [Events](#events)
- [Promises & Async](#promises--async)


## Variables & Data Types

### Variable Declaration
```javascript
// Modern variable declarations
let changeable = "Can be reassigned";
const constant = "Cannot be reassigned";
var oldStyle = "Not recommended, function-scoped";

// Multiple declarations
let a, b, c;
let x = 1, y = 2, z = 3;
```

### Basic Data Types
```javascript
// String
let name = "John";
let template = `Hello ${name}`; // Template literal

// Number
let integer = 42;
let float = 3.14;
let infinity = Infinity;
let notANumber = NaN;

// Boolean
let isTrue = true;
let isFalse = false;

// Null and Undefined
let empty = null;
let notDefined = undefined;

// Symbol (unique identifier)
let symbol = Symbol('description');

// BigInt (large numbers)
let bigNumber = 9007199254740991n;
```

### Type Checking
```javascript
// typeof operator
typeof "hello"     // "string"
typeof 42          // "number"
typeof true        // "boolean"
typeof undefined   // "undefined"
typeof null        // "object" (JavaScript quirk)
typeof {}          // "object"
typeof []          // "object"
typeof Symbol()    // "symbol"
```



## Operators

### Arithmetic Operators
```javascript
// Basic Math
let sum = 5 + 3;      // Addition
let diff = 10 - 4;    // Subtraction
let product = 3 * 6;  // Multiplication
let quotient = 15 / 3;// Division
let remainder = 17 % 5;// Modulus
let power = 2 ** 3;   // Exponentiation

// Increment/Decrement
let count = 0;
count++;              // Increment
count--;              // Decrement
```

### Assignment Operators
```javascript
let x = 5;            // Basic assignment
x += 3;               // x = x + 3
x -= 2;               // x = x - 2
x *= 4;               // x = x * 4
x /= 2;               // x = x / 2
x %= 3;               // x = x % 3
x **= 2;              // x = x ** 2
```

### Comparison Operators
```javascript
// Regular comparison
5 > 3                 // Greater than
5 < 3                 // Less than
5 >= 3                // Greater than or equal
5 <= 3                // Less than or equal

// Equality
5 == "5"              // Equal (with type coercion)
5 === "5"             // Strictly equal (no type coercion)
5 != "5"              // Not equal
5 !== "5"             // Strictly not equal
```

### Logical Operators
```javascript
// AND, OR, NOT
true && false         // Logical AND
true || false         // Logical OR
!true                 // Logical NOT

// Short-circuit evaluation
let a = null;
let b = a || "default"; // Returns "default"

// Nullish coalescing
let c = null ?? "default"; // Returns "default"
```




## Control Structures

### If Statements
```javascript
// Basic if
if (condition) {
    // code
}

// If-else
if (condition) {
    // code
} else {
    // code
}

// If-else if-else
if (condition1) {
    // code
} else if (condition2) {
    // code
} else {
    // code
}

// Ternary operator
let result = condition ? "yes" : "no";
```

### Switch Statements
```javascript
switch (value) {
    case 1:
        // code
        break;
    case 2:
        // code
        break;
    default:
        // code
}
```

### Loops
```javascript
// For loop
for (let i = 0; i < 5; i++) {
    // code
}

// While loop
while (condition) {
    // code
}

// Do-while loop
do {
    // code
} while (condition);

// For...of (arrays, strings)
for (const item of array) {
    // code
}

// For...in (object properties)
for (const key in object) {
    // code
}
```

### Error Handling
```javascript
try {
    // code that might throw an error
} catch (error) {
    // handle error
} finally {
    // always executes
}
```






## Functions

### Function Declarations
```javascript
// Basic function
function greet(name) {
    return `Hello, ${name}!`;
}

// Function expression
const greet = function(name) {
    return `Hello, ${name}!`;
};

// Arrow function
const greet = (name) => `Hello, ${name}!`;

// Default parameters
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}
```

### Function Parameters
```javascript
// Rest parameters
function sum(...numbers) {
    return numbers.reduce((a, b) => a + b, 0);
}

// Destructuring parameters
function printUser({name, age}) {
    console.log(`${name} is ${age} years old`);
}

// Parameter validation
function divide(a, b) {
    if (b === 0) throw new Error("Cannot divide by zero");
    return a / b;
}
```

### Advanced Function Concepts
```javascript
// Immediately Invoked Function Expression (IIFE)
(function() {
    // code
})();

// Closure
function counter() {
    let count = 0;
    return function() {
        return ++count;
    };
}

// Higher-order function
function multiply(factor) {
    return function(number) {
        return number * factor;
    };
}
```






## Arrays & Objects

### Array Methods
```javascript
// Creating arrays
let array = [1, 2, 3];
let newArray = Array.from("hello");
let filled = new Array(3).fill(0);

// Basic operations
array.push(4);           // Add to end
array.pop();            // Remove from end
array.unshift(0);       // Add to start
array.shift();          // Remove from start

// Modern array methods
array.map(x => x * 2);          // Transform elements
array.filter(x => x > 2);       // Filter elements
array.reduce((a, b) => a + b);  // Reduce to single value
array.find(x => x === 2);       // Find element
array.some(x => x > 2);         // Check if some pass
array.every(x => x > 0);        // Check if all pass
```

### Object Operations
```javascript
// Object creation
const user = {
    name: "John",
    age: 30,
    sayHi() {
        return `Hi, I'm ${this.name}`;
    }
};

// Object methods
Object.keys(user);              // Get keys
Object.values(user);            // Get values
Object.entries(user);           // Get key-value pairs
Object.freeze(user);            // Make immutable
Object.assign({}, user);        // Shallow copy

// Destructuring
const { name, age } = user;
const { name: userName } = user;
```

### Modern Object Features
```javascript
// Spread operator
const clone = { ...user };
const merged = { ...obj1, ...obj2 };

// Computed properties
const prop = "name";
const obj = {
    [prop]: "John"
};

// Object shorthand
const name = "John";
const userObj = { name };  // Same as { name: name }
```







## DOM Manipulation

### Selecting Elements
```javascript
// Basic selectors
const element = document.getElementById('myId');
const elements = document.getElementsByClassName('myClass');
const tags = document.getElementsByTagName('div');

// Query selectors
const one = document.querySelector('.myClass');
const all = document.querySelectorAll('.myClass');

// Navigation
const parent = element.parentElement;
const children = element.children;
const next = element.nextElementSibling;
const prev = element.previousElementSibling;
```

### Modifying Elements
```javascript
// Content manipulation
element.textContent = 'New text';
element.innerHTML = '<span>HTML content</span>';
element.innerText = 'Visible text';

// Attributes
element.setAttribute('class', 'newClass');
element.getAttribute('class');
element.removeAttribute('class');
element.hasAttribute('class');

// Classes
element.classList.add('newClass');
element.classList.remove('oldClass');
element.classList.toggle('active');
element.classList.contains('active');
```

### Creating & Removing Elements
```javascript
// Creating elements
const div = document.createElement('div');
const text = document.createTextNode('Hello');

// Adding elements
parent.appendChild(div);
parent.insertBefore(div, referenceNode);
parent.append(div, text, 'Hello');
parent.prepend(div);

// Removing elements
element.remove();
parent.removeChild(element);
```






## Events

### Event Handling
```javascript
// Adding event listeners
element.addEventListener('click', function(event) {
    console.log('Clicked!');
});

// Removing event listeners
const handler = (event) => console.log('Clicked!');
element.addEventListener('click', handler);
element.removeEventListener('click', handler);

// Event object properties
element.addEventListener('click', (event) => {
    event.preventDefault();     // Prevent default behavior
    event.stopPropagation();   // Stop event bubbling
    event.target;              // Element that triggered event
    event.currentTarget;       // Element handling event
});
```

### Common Events
```javascript
// Mouse events
element.onclick = () => {};
element.onmousedown = () => {};
element.onmouseup = () => {};
element.onmouseover = () => {};
element.onmouseout = () => {};

// Keyboard events
element.onkeydown = () => {};
element.onkeyup = () => {};
element.onkeypress = () => {};

// Form events
form.onsubmit = () => {};
input.onchange = () => {};
input.oninput = () => {};
```

### Event Delegation
```javascript
// Efficient event handling
document.getElementById('parent').addEventListener('click', (e) => {
    if (e.target.matches('.button')) {
        console.log('Button clicked!');
    }
});

// Custom events
const event = new CustomEvent('custom', {
    detail: { message: 'Hello' }
});
element.dispatchEvent(event);
```







## Promises & Async

### Promises
```javascript
// Creating promises
const promise = new Promise((resolve, reject) => {
    // Async operation
    if (success) {
        resolve('Success!');
    } else {
        reject('Error!');
    }
});

// Using promises
promise
    .then(result => console.log(result))
    .catch(error => console.error(error))
    .finally(() => console.log('Done'));

// Promise methods
Promise.all([promise1, promise2]);     // All promises
Promise.race([promise1, promise2]);    // First to complete
Promise.allSettled([promise1, promise2]); // All settled
Promise.resolve('Success');            // Resolved promise
Promise.reject('Error');               // Rejected promise
```

### Async/Await
```javascript
// Async function
async function getData() {
    try {
        const response = await fetch('api/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error(error);
    }
}

// Parallel execution
async function getMultipleData() {
    const [data1, data2] = await Promise.all([
        fetch('api/data1'),
        fetch('api/data2')
    ]);
    return [await data1.json(), await data2.json()];
}
```

### Fetch API
```javascript
// Basic fetch
fetch('api/data')
    .then(response => response.json())
    .then(data => console.log(data));

// Fetch with options
fetch('api/data', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ key: 'value' })
});
```



