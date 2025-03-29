# Advanced JavaScript Guide

## Table of Contents
- [Object-Oriented JavaScript](#object-oriented-javascript)
- [Advanced Functions & Closures](#advanced-functions--closures)
- [Asynchronous Programming](#asynchronous-programming)
- [Modern JavaScript Features](#modern-javascript-features)
- [Design Patterns](#design-patterns)
- [Performance Optimization](#performance-optimization)
- [Testing & Debugging](#testing--debugging)
- [Security Best Practices](#security-best-practices)






## Object-Oriented JavaScript

### Classes and Objects
```javascript
// Modern Class Syntax
class User {
    // Private fields (# makes it private)
    #password;
    
    // Constructor method
    constructor(username, password) {
        this.username = username;    // Public property
        this.#password = password;   // Private property
    }
    
    // Instance method
    login() {
        return `${this.username} is logging in...`;
    }
    
    // Static method (called on class itself)
    static validateUsername(username) {
        return username.length >= 3;
    }
    
    // Getter
    get userInfo() {
        return `Username: ${this.username}`;
    }
    
    // Setter
    set userPassword(newPassword) {
        if (newPassword.length >= 8) {
            this.#password = newPassword;
        }
    }
}

// Using the class
const user = new User('john_doe', 'secret123');
console.log(user.login());          // "john_doe is logging in..."
console.log(User.validateUsername('john_doe'));  // true
```

### Inheritance and Polymorphism
```javascript
// Base class
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        return `${this.name} makes a sound`;
    }
}

// Derived class
class Dog extends Animal {
    constructor(name, breed) {
        super(name);                // Call parent constructor
        this.breed = breed;
    }
    
    speak() {
        return `${this.name} barks!`;  // Override parent method
    }
    
    fetch() {
        return `${this.name} fetches the ball`;
    }
}

// Using inheritance
const dog = new Dog('Rex', 'German Shepherd');
console.log(dog.speak());           // "Rex barks!"
console.log(dog.fetch());           // "Rex fetches the ball"
```







## Advanced Functions & Closures

### Higher-Order Functions
```javascript
// Functions that take or return other functions
const multiply = (multiplier) => {
    // Returns a new function
    return (number) => number * multiplier;
};

const double = multiply(2);
const triple = multiply(3);

console.log(double(5));    // 10
console.log(triple(5));    // 15

// Function composition
const compose = (f, g) => (x) => f(g(x));
const addOne = (x) => x + 1;
const square = (x) => x * x;

const addThenSquare = compose(square, addOne);
console.log(addThenSquare(3));    // 16 ((3 + 1)²)
```

### Advanced Closures
```javascript
// Creating private state
function createCounter() {
    let count = 0;    // Private variable
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getCount: () => count,
        reset: () => { count = 0; }
    };
}

const counter = createCounter();
counter.increment();    // 1
counter.increment();    // 2
counter.decrement();    // 1
console.log(counter.getCount());    // 1

// Partial application
function partial(fn, ...args) {
    return function(...moreArgs) {
        return fn(...args, ...moreArgs);
    };
}

const add = (a, b, c) => a + b + c;
const add5and10 = partial(add, 5, 10);
console.log(add5and10(15));    // 30
```

### Function Currying
```javascript
// Converting a function with multiple arguments
// into a sequence of functions with single arguments
const curry = (fn) => {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn(...args);
        }
        return (...moreArgs) => curried(...args, ...moreArgs);
    };
};

// Example usage
const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);

console.log(curriedSum(1)(2)(3));     // 6
console.log(curriedSum(1, 2)(3));     // 6
console.log(curriedSum(1)(2, 3));     // 6
```



## Asynchronous Programming

### Promises Deep Dive
```javascript
// Creating and using promises
const fetchData = (id) => {
    return new Promise((resolve, reject) => {
        // Simulating API call
        setTimeout(() => {
            const data = { id: id, name: 'Item ' + id };
            
            if (id > 0) {
                resolve(data);    // Success case
            } else {
                reject('Invalid ID');    // Error case
            }
        }, 1000);
    });
};

// Promise chaining
fetchData(1)
    .then(data => {
        console.log('First then:', data);
        return fetchData(2);    // Return another promise
    })
    .then(data => {
        console.log('Second then:', data);
    })
    .catch(error => {
        console.error('Error:', error);
    })
    .finally(() => {
        console.log('Operation complete');
    });
```

### Async/Await Patterns
```javascript
// Basic async/await
async function getData() {
    try {
        const result1 = await fetchData(1);
        console.log('First result:', result1);
        
        const result2 = await fetchData(2);
        console.log('Second result:', result2);
        
        return [result1, result2];
        
    } catch (error) {
        console.error('Error:', error);
    }
}

// Parallel execution
async function getMultipleData() {
    try {
        // Run promises in parallel
        const results = await Promise.all([
            fetchData(1),
            fetchData(2),
            fetchData(3)
        ]);
        
        console.log('All results:', results);
        
    } catch (error) {
        console.error('Error in parallel execution:', error);
    }
}
```

### Advanced Async Patterns
```javascript
// Custom async iterator
async function* generateSequence(start, end) {
    for (let i = start; i <= end; i++) {
        // Yield promise results
        yield await fetchData(i);
    }
}

// Using async iterator
async function processSequence() {
    for await (const data of generateSequence(1, 3)) {
        console.log('Processed:', data);
    }
}

// Race condition handling
async function getFirstResult() {
    try {
        const result = await Promise.race([
            fetchData(1),
            fetchData(2),
            fetchData(3)
        ]);
        
        console.log('First to complete:', result);
        
    } catch (error) {
        console.error('Race error:', error);
    }
}
```







## Modern JavaScript Features

### ES6+ Syntax Features
```javascript
// Destructuring
const user = { name: 'John', age: 30, city: 'New York' };
const { name, age, city } = user;    // Object destructuring

const numbers = [1, 2, 3, 4, 5];
const [first, second, ...rest] = numbers;    // Array destructuring

// Spread operator
const newUser = { ...user, role: 'admin' };    // Clone and extend object
const moreNumbers = [...numbers, 6, 7];        // Clone and extend array

// Optional chaining
const response = {
    data: {
        user: {
            address: null
        }
    }
};
const zipCode = response?.data?.user?.address?.zip;    // Safe nested access
```

### Modern Data Structures
```javascript
// Map - key-value pairs with any type of key
const userMap = new Map();
userMap.set('john', { age: 30 });
userMap.set(42, 'meaning');    // Numbers as keys
userMap.set(user, 'object');   // Objects as keys

// Set - unique values
const uniqueNumbers = new Set([1, 2, 2, 3, 3, 4]);
uniqueNumbers.add(5);
uniqueNumbers.has(2);    // true
uniqueNumbers.size;      // 5

// WeakMap and WeakSet
const weakMap = new WeakMap();    // Garbage-collection-friendly
const key = { id: 1 };
weakMap.set(key, 'data');
```

### Modern Functions and Methods
```javascript
// Array methods
const items = [1, 2, 3, 4, 5];

// Pipeline of operations
const result = items
    .filter(n => n > 2)             // [3, 4, 5]
    .map(n => n * 2)                // [6, 8, 10]
    .reduce((sum, n) => sum + n);   // 24

// Object methods
const source = { a: 1, b: 2 };
const clone = Object.fromEntries(    // Create object from entries
    Object.entries(source)           // Get key-value pairs
        .map(([key, val]) => [key, val * 2])
);

// String methods
const text = '  Hello World  ';
text.trimStart();    // "Hello World  "
text.trimEnd();      // "  Hello World"
text.replaceAll('l', 'L');    // "  HeLLo WorLd  "
```





## Design Patterns

### Creational Patterns
```javascript
// Singleton Pattern
class Database {
    static #instance;
    
    constructor() {
        if (Database.#instance) {
            return Database.#instance;
        }
        Database.#instance = this;
    }
    
    query(sql) {
        console.log(`Executing: ${sql}`);
    }
}

// Factory Pattern
class UserFactory {
    createUser(type) {
        switch(type) {
            case 'admin':
                return new AdminUser();
            case 'guest':
                return new GuestUser();
            default:
                return new RegularUser();
        }
    }
}
```

### Structural Patterns
```javascript
// Adapter Pattern
class OldAPI {
    oldMethod() {
        return { oldData: 'data' };
    }
}

class NewAPIAdapter {
    constructor(oldAPI) {
        this.oldAPI = oldAPI;
    }
    
    newMethod() {
        const oldData = this.oldAPI.oldMethod();
        return { newData: oldData.oldData };
    }
}

// Decorator Pattern
class Coffee {
    cost() {
        return 5;
    }
}

class MilkDecorator {
    constructor(coffee) {
        this.coffee = coffee;
    }
    
    cost() {
        return this.coffee.cost() + 2;
    }
}
```

### Behavioral Patterns
```javascript
// Observer Pattern
class EventEmitter {
    constructor() {
        this.events = {};
    }
    
    on(event, callback) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(callback);
    }
    
    emit(event, data) {
        if (this.events[event]) {
            this.events[event].forEach(callback => callback(data));
        }
    }
}

// Strategy Pattern
class PaymentProcessor {
    constructor(strategy) {
        this.strategy = strategy;
    }
    
    processPayment(amount) {
        return this.strategy.pay(amount);
    }
}

class CreditCardStrategy {
    pay(amount) {
        return `Paid ${amount} with credit card`;
    }
}
```





## Performance Optimization

### Memory Management
```javascript
// Efficient data structures
const largeArray = new Array(1000000);    // Pre-allocate space
const typedArray = new Float64Array(1000); // Typed arrays for numbers

// Memory leaks prevention
class ResourceManager {
    constructor() {
        this.resources = new WeakMap();    // Automatic cleanup
    }
    
    addResource(key, value) {
        this.resources.set(key, value);
    }
    
    // Proper cleanup
    dispose() {
        this.resources = null;
    }
}
```

### Code Optimization
```javascript
// Caching results (memoization)
const memoize = (fn) => {
    const cache = new Map();
    
    return (...args) => {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);    // Return cached result
        }
        
        const result = fn(...args);
        cache.set(key, result);       // Store for later
        return result;
    };
};

// Efficient loops
const arr = [1, 2, 3, 4, 5];
// Faster than forEach for large arrays
for (let i = 0; i < arr.length; i++) {
    // Process item
}
```

### DOM Performance
```javascript
// Batch DOM updates
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    fragment.appendChild(div);
}
document.body.appendChild(fragment);    // Single DOM update

// Virtual scrolling for large lists
class VirtualScroller {
    constructor(container, items) {
        this.container = container;
        this.items = items;
        this.viewportHeight = container.clientHeight;
        this.rowHeight = 30;
        
        this.visibleItems = Math.ceil(this.viewportHeight / this.rowHeight);
        this.renderVisible();
    }
    
    renderVisible() {
        // Only render items in viewport
        const start = Math.floor(this.container.scrollTop / this.rowHeight);
        const items = this.items.slice(start, start + this.visibleItems);
        // Render items...
    }
}
```




## Testing & Debugging

### Unit Testing
```javascript
// Using Jest testing framework
describe('Calculator', () => {
    // Setup before tests
    const calculator = new Calculator();
    
    test('adds two numbers correctly', () => {
        expect(calculator.add(2, 3)).toBe(5);
    });
    
    test('subtracts two numbers correctly', () => {
        expect(calculator.subtract(5, 3)).toBe(2);
    });
    
    // Test async functions
    test('fetches user data', async () => {
        const data = await calculator.fetchData();
        expect(data).toHaveProperty('id');
    });
});

// Mock functions and dependencies
const mockAPI = {
    getData: jest.fn().mockResolvedValue({ success: true })
};
```

### Advanced Debugging
```javascript
// Custom debug utility
const debug = {
    log: (message, data) => {
        console.log(
            `[${new Date().toISOString()}]`,
            message,
            JSON.stringify(data, null, 2)
        );
    },
    
    trace: (error) => {
        console.error('Error:', error);
        console.trace('Stack trace:');
    }
};

// Performance monitoring
class PerformanceMonitor {
    static measure(label, callback) {
        console.time(label);
        const result = callback();
        console.timeEnd(label);
        return result;
    }
    
    static async measureAsync(label, callback) {
        const start = performance.now();
        const result = await callback();
        const duration = performance.now() - start;
        console.log(`${label}: ${duration}ms`);
        return result;
    }
}
```

### Error Handling
```javascript
// Custom error classes
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = 'ValidationError';
    }
}

// Global error handler
window.onerror = (message, source, line, column, error) => {
    debug.log('Global error:', {
        message,
        source,
        line,
        column,
        stack: error.stack
    });
    
    // Report to error tracking service
    ErrorTracker.report(error);
    
    return true; // Prevent default handling
};
```



## Security Best Practices

### Input Validation
```javascript
// Sanitize user input
class InputValidator {
    static sanitizeString(input) {
        return input
            .trim()
            .replace(/[<>]/g, '')    // Remove potential HTML
            .slice(0, 255);          // Limit length
    }
    
    static validateEmail(email) {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(email);
    }
    
    static sanitizeObject(obj) {
        return Object.entries(obj).reduce((clean, [key, value]) => {
            clean[key] = typeof value === 'string' 
                ? this.sanitizeString(value) 
                : value;
            return clean;
        }, {});
    }
}
```

### XSS Prevention
```javascript
// Content Security Policy
class SecurityHeaders {
    static setupCSP() {
        const csp = {
            'default-src': ["'self'"],
            'script-src': ["'self'", "'nonce-random123'"],
            'style-src': ["'self'", "'unsafe-inline'"],
            'img-src': ["'self'", 'https:'],
        };
        
        return Object.entries(csp)
            .map(([key, values]) => `${key} ${values.join(' ')}`)
            .join('; ');
    }
}

// Safe HTML rendering
class SafeRenderer {
    static escapeHTML(str) {
        const div = document.createElement('div');
        div.textContent = str;
        return div.innerHTML;
    }
    
    static renderUserContent(content) {
        return `<div>${this.escapeHTML(content)}</div>`;
    }
}
```

### Authentication & Authorization
```javascript
// JWT handling
class TokenManager {
    static generateToken(payload) {
        return jwt.sign(payload, process.env.SECRET_KEY, {
            expiresIn: '1h'
        });
    }
    
    static verifyToken(token) {
        try {
            return jwt.verify(token, process.env.SECRET_KEY);
        } catch (error) {
            throw new ValidationError('Invalid token');
        }
    }
}

// Role-based access control
class AccessControl {
    static checkPermission(user, resource, action) {
        const userRole = user.role;
        const permissions = this.getPermissions(userRole);
        
        return permissions.some(permission => 
            permission.resource === resource &&
            permission.actions.includes(action)
        );
    }
}
```



