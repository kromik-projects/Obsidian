# Functions

## What are Functions?

Functions are reusable blocks of code that perform a specific task. They help organize code, avoid repetition, and make programs easier to understand.

## Declaring Functions

### Function Declaration

```javascript
function greet(name) {
    return `Hello, ${name}!`;
}

console.log(greet("Alice"));  // "Hello, Alice!"
```

### Function Expression

```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};

console.log(greet("Bob"));  // "Hello, Bob!"
```

### Arrow Functions (ES6+)

```javascript
// Full syntax
const greet = (name) => {
    return `Hello, ${name}!`;
};

// Shorthand (single expression)
const greet = name => `Hello, ${name}!`;

// Multiple parameters
const add = (a, b) => a + b;

// No parameters
const sayHi = () => "Hi!";
```

> [!tip] When to Use Arrow Functions
> Arrow functions are great for short, simple functions and callbacks. Use regular functions for methods and when you need `this` binding.

## Parameters and Arguments

### Basic Parameters

```javascript
function introduce(name, age) {
    console.log(`I'm ${name}, ${age} years old.`);
}

introduce("Alice", 25);  // I'm Alice, 25 years old.
```

### Default Parameters

```javascript
function greet(name = "Guest", greeting = "Hello") {
    return `${greeting}, ${name}!`;
}

console.log(greet());              // "Hello, Guest!"
console.log(greet("Alice"));       // "Hello, Alice!"
console.log(greet("Bob", "Hi"));   // "Hi, Bob!"
```

### Rest Parameters

Collect remaining arguments into an array:

```javascript
function sum(...numbers) {
    let total = 0;
    for (let num of numbers) {
        total += num;
    }
    return total;
}

console.log(sum(1, 2, 3));      // 6
console.log(sum(1, 2, 3, 4, 5)); // 15

// With regular parameters
function greet(greeting, ...names) {
    return names.map(name => `${greeting}, ${name}!`);
}
```

### Destructuring Parameters

```javascript
// Object destructuring
function createUser({ name, age, email }) {
    return { name, age, email, createdAt: new Date() };
}

createUser({ name: "Alice", age: 25, email: "alice@example.com" });

// Array destructuring
function getFirst([first, second]) {
    return first;
}
```

## Return Values

```javascript
// Single return
function square(n) {
    return n * n;
}

// Multiple returns (conditional)
function absoluteValue(n) {
    if (n < 0) {
        return -n;
    }
    return n;
}

// Returning objects
function createPerson(name, age) {
    return {
        name: name,
        age: age,
        greet() {
            return `Hi, I'm ${this.name}`;
        }
    };
}

// No return (returns undefined)
function logMessage(msg) {
    console.log(msg);
    // implicit return undefined
}
```

## Scope

### Local Scope

Variables declared inside a function are local:

```javascript
function example() {
    let localVar = "I'm local";
    console.log(localVar);  // Works
}

example();
// console.log(localVar);  // ERROR: not defined
```

### Global Scope

Variables declared outside functions are global:

```javascript
let globalVar = "I'm global";

function example() {
    console.log(globalVar);  // Works
}
```

### Block Scope

`let` and `const` are block-scoped:

```javascript
function example() {
    if (true) {
        let blockVar = "I'm in a block";
        var functionVar = "I'm function-scoped";
    }
    // console.log(blockVar);    // ERROR
    console.log(functionVar);    // Works (var is function-scoped)
}
```

## Closures

Functions remember their outer scope:

```javascript
function createCounter() {
    let count = 0;

    return function() {
        count++;
        return count;
    };
}

const counter = createCounter();
console.log(counter());  // 1
console.log(counter());  // 2
console.log(counter());  // 3

// Each counter is independent
const counter2 = createCounter();
console.log(counter2()); // 1
```

### Practical Closure Example

```javascript
function createMultiplier(multiplier) {
    return function(number) {
        return number * multiplier;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

## Higher-Order Functions

Functions that take or return other functions:

```javascript
// Taking a function as argument
function repeat(n, action) {
    for (let i = 0; i < n; i++) {
        action(i);
    }
}

repeat(3, console.log);  // 0, 1, 2

repeat(3, i => {
    console.log(`Iteration ${i}`);
});

// Array methods are higher-order functions
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);
const sum = numbers.reduce((acc, n) => acc + n, 0);
```

## Immediately Invoked Function Expressions (IIFE)

```javascript
// Runs immediately
(function() {
    console.log("I run immediately!");
})();

// With parameters
(function(name) {
    console.log(`Hello, ${name}!`);
})("Alice");

// Arrow function IIFE
(() => {
    console.log("Arrow IIFE!");
})();
```

## Recursion

Functions calling themselves:

```javascript
// Factorial: 5! = 5 * 4 * 3 * 2 * 1 = 120
function factorial(n) {
    if (n <= 1) {
        return 1;  // Base case
    }
    return n * factorial(n - 1);  // Recursive case
}

console.log(factorial(5));  // 120

// Countdown
function countdown(n) {
    if (n <= 0) {
        console.log("Blastoff!");
        return;
    }
    console.log(n);
    countdown(n - 1);
}
```

## Practical Examples

### Calculator Functions

```javascript
const calculator = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => b !== 0 ? a / b : "Cannot divide by zero"
};

console.log(calculator.add(5, 3));      // 8
console.log(calculator.divide(10, 2));  // 5
```

### Validation Function

```javascript
function validateEmail(email) {
    const pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return pattern.test(email);
}

console.log(validateEmail("test@example.com"));  // true
console.log(validateEmail("invalid"));           // false
```

### Debounce Function

```javascript
function debounce(func, delay) {
    let timeoutId;

    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}

// Usage: only runs after 300ms of no calls
const debouncedSearch = debounce(query => {
    console.log(`Searching: ${query}`);
}, 300);
```

## Practice Exercises

```javascript
// 1. Write a function that returns the larger of two numbers
function max(a, b) {
    return a > b ? a : b;
}

// 2. Write a function that checks if a string is a palindrome
function isPalindrome(str) {
    const cleaned = str.toLowerCase().replace(/[^a-z]/g, "");
    return cleaned === cleaned.split("").reverse().join("");
}

// 3. Write a function that counts vowels in a string
function countVowels(str) {
    const vowels = "aeiouAEIOU";
    let count = 0;
    for (let char of str) {
        if (vowels.includes(char)) {
            count++;
        }
    }
    return count;
}

// 4. Write a higher-order function that applies a function twice
function applyTwice(func, value) {
    return func(func(value));
}

const addOne = x => x + 1;
console.log(applyTwice(addOne, 5));  // 7
```

## Key Takeaways

- Functions are declared with `function`, expressions, or arrow syntax
- Parameters can have default values and use rest syntax (`...`)
- Variables have function or block scope
- Closures let functions remember their outer scope
- Higher-order functions take or return other functions
- Arrow functions are concise but have different `this` behavior

---

**Previous:** [[04 - Control Flow]]

**Next:** [[06 - Arrays]]

**Back to:** [[00 - Welcome]]
