# JavaScript Basics Guide

## Table of Contents
- [Introduction to JavaScript](#introduction-to-javascript)
- [Setting Up Development Environment](#setting-up-development-environment)
- [JavaScript in HTML](#javascript-in-html)
- [Working with Data](#working-with-data)
- [Program Flow](#program-flow)
- [Functions Deep Dive](#functions-deep-dive)
- [DOM Basics](#dom-basics)
- [Basic Event Handling](#basic-event-handling)







## Introduction to JavaScript

### What is JavaScript?
JavaScript is a versatile programming language that enables interactive and dynamic web content. It runs in browsers, on servers, and in various other environments.

### Key Features
- Dynamic typing
- First-class functions
- Object-oriented capabilities
- Event-driven programming
- Rich ecosystem of libraries and frameworks

### JavaScript Uses
```javascript
// Web Development
document.getElementById('myButton').onclick = function() {
    alert('Button clicked!');
}

// Server-side (Node.js)
const http = require('http');
const server = http.createServer((req, res) => {
    res.end('Hello World!');
});

// Mathematics
const calculateArea = (radius) => Math.PI * radius ** 2;

// Data Manipulation
const users = ['John', 'Jane', 'Bob'];
const filtered = users.filter(name => name.startsWith('J'));
```




## Setting Up Development Environment

### Code Editor Setup
```javascript
// Popular Code Editors:
// 1. Visual Studio Code (VS Code) - Free, lightweight, extensive plugins
// 2. Sublime Text - Fast, customizable
// 3. WebStorm - Full IDE, powerful features

// Essential VS Code Extensions:
// - JavaScript (ES6) code snippets
// - ESLint - Code quality checker
// - Prettier - Code formatter
// - Live Server - Local development server
```

### Browser Developer Tools
```javascript
// Chrome DevTools Shortcuts:
// F12 or Ctrl+Shift+I - Open DevTools
// Ctrl+Shift+J - Open Console
// Ctrl+Shift+C - Inspect Elements

// Debugging in Console
console.log('Basic output');     // Simple logging
console.info('Information');     // Info level
console.warn('Warning');         // Warning level
console.error('Error');          // Error level
console.table(['a', 'b', 'c']);  // Table format
```

### Project Structure
```plaintext
my-project/
├── index.html          // Main HTML file
├── css/               
│   └── styles.css     // Stylesheet
├── js/
│   ├── main.js        // Main JavaScript file
│   └── utils.js       // Utility functions
└── images/            // Image assets
```







## JavaScript in HTML

### Adding JavaScript to HTML
```html
<!-- 1. Internal JavaScript (in HTML file) -->
<script>
    // Your JavaScript code here
    const greeting = "Hello World!";
    console.log(greeting);
</script>

<!-- 2. External JavaScript (separate .js file) -->
<!-- Best practice: Place before closing </body> tag -->
<script src="js/main.js"></script>

<!-- 3. Async loading (downloads in background) -->
<script src="js/analytics.js" async></script>

<!-- 4. Defer loading (runs after HTML loads) -->
<script src="js/main.js" defer></script>
```

### Script Loading Strategies
```javascript
// DOMContentLoaded - HTML is loaded and parsed
document.addEventListener('DOMContentLoaded', () => {
    // Your code here - DOM is ready!
    const title = document.querySelector('h1');
    title.style.color = 'blue';
});

// Window load - Everything is loaded
window.onload = () => {
    // Your code here - Images and resources are ready!
    const images = document.querySelectorAll('img');
    console.log('Total images:', images.length);
};
```

### Modern JavaScript Features
```html
<!-- Using modules -->
<script type="module">
    // Import features from other files
    import { helper } from './utils.js';
    
    // Use modern JavaScript features
    const numbers = [1, 2, 3];
    const doubled = numbers.map(x => x * 2);
</script>
```





## Working with Data

### String Operations
```javascript
// String creation and manipulation
const firstName = "John";
const lastName = 'Doe';      // Single or double quotes work

// Template literals - modern string formatting
const greeting = `Hello, ${firstName}!`;    // Using variables in strings

// Common string methods
const text = "JavaScript is awesome";
text.length;                 // Get string length: 21
text.toUpperCase();         // Convert to uppercase: "JAVASCRIPT IS AWESOME"
text.toLowerCase();         // Convert to lowercase: "javascript is awesome"
text.split(' ');           // Split into array: ["JavaScript", "is", "awesome"]
text.includes('Java');     // Check if contains: true
text.replace('awesome', 'amazing');  // Replace text
```

### Number Operations
```javascript
// Number types and calculations
const integer = 42;         // Whole number
const float = 3.14;        // Decimal number
const scientific = 2.998e8; // Scientific notation

// Math operations
Math.round(3.6);           // Round to nearest integer: 4
Math.floor(3.6);           // Round down: 3
Math.ceil(3.2);            // Round up: 4
Math.random();             // Random number between 0 and 1
Math.max(1, 2, 3);         // Find highest number: 3
Math.min(1, 2, 3);         // Find lowest number: 1

// Number formatting
const price = 42.5678;
price.toFixed(2);          // Format decimals: "42.57"
```

### Data Type Conversion
```javascript
// Converting between types
String(123);               // Number to string: "123"
Number("123");            // String to number: 123
Boolean(1);               // To boolean: true

// Type checking
typeof "hello";           // Returns: "string"
typeof 42;                // Returns: "number"
typeof true;              // Returns: "boolean"
Array.isArray([1,2,3]);   // Check for array: true

// Common type conversion gotchas
Number("hello");          // NaN (Not a Number)
Number(null);             // 0
Number(undefined);        // NaN
Boolean("");              // false
Boolean(0);              // false
Boolean("0");            // true
```





## Program Flow

### Making Decisions
```javascript
// If statements - the building blocks of logic
const age = 18;

// Simple if statement
if (age >= 18) {
    console.log("You can vote!");    // Will run if age is 18 or more
}

// If-else for two possibilities
const time = 14;
if (time < 12) {
    console.log("Good morning!");    // Before noon
} else {
    console.log("Good afternoon!");  // Noon or later
}

// Multiple conditions with else-if
const score = 85;
if (score >= 90) {
    console.log("A grade");          // 90 or above
} else if (score >= 80) {
    console.log("B grade");          // 80-89
} else if (score >= 70) {
    console.log("C grade");          // 70-79
} else {
    console.log("Need improvement"); // Below 70
}
```

### Loops and Iteration
```javascript
// For loop - when you know how many times to loop
for (let i = 0; i < 5; i++) {
    console.log(`Count: ${i}`);      // Counts 0 through 4
}

// While loop - when you don't know how many iterations
let coins = 0;
while (coins < 10) {
    coins++;                         // Adds coins until we have 10
    console.log(`You have ${coins} coins`);
}

// For...of loop - iterate over arrays
const fruits = ['apple', 'banana', 'orange'];
for (const fruit of fruits) {
    console.log(`I like ${fruit}`);  // Prints each fruit
}

// Break and Continue
for (let i = 0; i < 5; i++) {
    if (i === 3) break;             // Stops at 3
    console.log(i);                 // Prints 0, 1, 2
}

for (let i = 0; i < 5; i++) {
    if (i === 3) continue;          // Skips 3
    console.log(i);                 // Prints 0, 1, 2, 4
}
```






## Functions Deep Dive

### Function Basics
```javascript
// Regular function declaration
function sayHello(name) {
    return `Hello, ${name}!`;    // Returns a greeting
}

// Function expression
const greet = function(name) {
    return `Hi, ${name}!`;       // Another way to create functions
};

// Arrow function - modern, concise syntax
const welcome = (name) => `Welcome, ${name}!`;

// Functions with default parameters
function greetUser(name = "Guest") {
    return `Hello, ${name}!`;    // Uses "Guest" if no name provided
}
```

### Function Scope and Closure
```javascript
// Global vs Local scope
let globalVar = "I'm global";     // Available everywhere

function scopeExample() {
    let localVar = "I'm local";   // Only available inside function
    console.log(globalVar);       // Can access global
    console.log(localVar);        // Can access local
}

// Closure - function remembering its scope
function counter() {
    let count = 0;               // Private variable
    
    return {
        increment: () => ++count,
        getCount: () => count
    };
}

const myCounter = counter();
myCounter.increment();           // Returns 1
myCounter.increment();           // Returns 2
myCounter.getCount();           // Returns 2
```

### Advanced Function Patterns
```javascript
// Callback functions
function doAfterDelay(callback) {
    setTimeout(() => {
        console.log("Delayed operation complete");
        callback();              // Runs the provided function
    }, 1000);
}

// Method chaining
const calculator = {
    value: 0,
    add(n) {
        this.value += n;
        return this;            // Returns object for chaining
    },
    subtract(n) {
        this.value -= n;
        return this;
    },
    getResult() {
        return this.value;
    }
};

calculator.add(5).subtract(2).add(10);  // Chains methods together
```






## DOM Basics

### Understanding the DOM Tree
```javascript
// The DOM represents HTML as a tree structure
document                          // The root element
    └── html                     // Root HTML element
        ├── head                 // Head section
        │   ├── title
        │   └── meta
        └── body                 // Body section
            ├── header
            ├── main
            └── footer

// Basic document access
document.documentElement;         // The <html> element
document.head;                   // The <head> element
document.body;                   // The <body> element
```

### Finding Elements
```javascript
// Single element selectors
const header = document.getElementById('main-header');     // By ID
const firstButton = document.querySelector('.btn');        // First matching CSS selector

// Multiple element selectors
const paragraphs = document.getElementsByTagName('p');     // All <p> elements
const buttons = document.getElementsByClassName('btn');     // All elements with class 'btn'
const links = document.querySelectorAll('a');              // All elements matching selector

// Navigation properties
const parent = element.parentElement;          // Parent element
const children = element.children;             // Child elements
const next = element.nextElementSibling;       // Next sibling
const prev = element.previousElementSibling;   // Previous sibling
```

### Modifying Elements
```javascript
// Changing content
element.textContent = 'New text';              // Update text content
element.innerHTML = '<span>New HTML</span>';   // Update HTML content

// Working with attributes
element.setAttribute('class', 'new-class');    // Set attribute
element.getAttribute('class');                 // Get attribute value
element.removeAttribute('class');              // Remove attribute
element.hasAttribute('class');                 // Check if attribute exists

// Styling elements
element.style.color = 'blue';                  // Change text color
element.style.backgroundColor = '#fff';        // Change background
element.style.fontSize = '16px';               // Change font size

// CSS classes
element.classList.add('active');               // Add class
element.classList.remove('disabled');          // Remove class
element.classList.toggle('visible');           // Toggle class
element.classList.contains('hidden');          // Check for class
```






## Basic Event Handling

### Understanding Events
```javascript
// Common types of events
// click     - When element is clicked
// submit    - When form is submitted
// keydown   - When keyboard key is pressed
// mouseover - When mouse moves over element
// load      - When page/image loads
// change    - When form input changes

// Basic event handling
const button = document.querySelector('#myButton');

button.onclick = function() {
    console.log('Button clicked!');    // Simple click handler
};

// Modern event listener approach
button.addEventListener('click', function() {
    console.log('Button clicked!');    // Better practice
});
```

### Event Object Properties
```javascript
// Working with the event object
button.addEventListener('click', function(event) {
    // Common event properties
    event.target;              // Element that triggered event
    event.currentTarget;       // Element handling the event
    event.type;               // Type of event (e.g., 'click')
    event.timestamp;          // When event occurred
    
    // Prevent default behavior
    event.preventDefault();    // Stop form submission, link navigation
    
    // Stop event bubbling
    event.stopPropagation();  // Prevent event from bubbling up
});
```

### Practical Event Examples
```javascript
// Form submission
const form = document.querySelector('form');

form.addEventListener('submit', function(event) {
    event.preventDefault();    // Prevent form from submitting
    
    // Get form data
    const formData = new FormData(form);
    const username = formData.get('username');
    
    console.log(`Form submitted by ${username}`);
});

// Keyboard events
document.addEventListener('keydown', function(event) {
    if (event.key === 'Escape') {
        console.log('Escape key pressed!');
    }
});

// Mouse events
const box = document.querySelector('.box');

box.addEventListener('mouseover', function() {
    this.style.backgroundColor = 'blue';    // Change color on hover
});

box.addEventListener('mouseout', function() {
    this.style.backgroundColor = 'red';     // Change back when mouse leaves
});
```








