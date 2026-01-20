# Variables and Data Types

## What are Variables?

Variables are containers that store data values. Think of them as labeled boxes where you can put information.

## Declaring Variables

JavaScript has three ways to declare variables:

### `let` - Modern, Recommended
```javascript
let age = 25;
let name = "Alice";
age = 26; // Can be reassigned
```

### `const` - For Constants
```javascript
const PI = 3.14159;
const SITE_NAME = "My Website";
// PI = 3; // ERROR! Cannot reassign
```

### `var` - Legacy (Avoid)
```javascript
var oldWay = "not recommended";
// Still works, but has scoping issues
```

> [!tip] Best Practice
> Use `const` by default. Use `let` only when you need to reassign the value. Avoid `var`.

## Naming Rules

Variable names must:
- Start with a letter, `_`, or `$`
- Contain only letters, numbers, `_`, or `$`
- Not be a reserved keyword (`let`, `function`, etc.)

```javascript
// Valid names
let userName = "John";
let _private = true;
let $price = 9.99;
let camelCase = "recommended style";

// Invalid names
// let 2fast = "error";     // Can't start with number
// let my-name = "error";   // No hyphens allowed
// let let = "error";       // Reserved keyword
```

## Data Types

JavaScript has several built-in data types:

### 1. String (Text)
```javascript
let greeting = "Hello, World!";
let name = 'Alice';  // Single or double quotes
let template = `Hello, ${name}!`;  // Template literal (backticks)

console.log(template); // "Hello, Alice!"
```

### 2. Number
```javascript
let integer = 42;
let decimal = 3.14;
let negative = -10;
let scientific = 2.5e6;  // 2,500,000

// Special numbers
let infinity = Infinity;
let notANumber = NaN;
```

### 3. Boolean
```javascript
let isActive = true;
let isLoggedIn = false;

// Result of comparisons
let isAdult = age >= 18;  // true or false
```

### 4. Undefined
```javascript
let notAssigned;
console.log(notAssigned);  // undefined
```

### 5. Null
```javascript
let empty = null;  // Intentionally empty
```

### 6. Symbol (Advanced)
```javascript
let id = Symbol("id");  // Unique identifier
```

### 7. BigInt (Large Numbers)
```javascript
let bigNumber = 9007199254740991n;  // Note the 'n'
```

## Checking Types

Use `typeof` to check a variable's type:

```javascript
console.log(typeof "Hello");    // "string"
console.log(typeof 42);         // "number"
console.log(typeof true);       // "boolean"
console.log(typeof undefined);  // "undefined"
console.log(typeof null);       // "object" (quirk!)
console.log(typeof {});         // "object"
console.log(typeof []);         // "object"
```

## Type Conversion

### String Conversion
```javascript
let num = 42;
let str = String(num);      // "42"
let str2 = num.toString();  // "42"
let str3 = num + "";        // "42"
```

### Number Conversion
```javascript
let str = "42";
let num = Number(str);    // 42
let num2 = parseInt(str); // 42 (integer)
let num3 = parseFloat("3.14"); // 3.14
let num4 = +"42";         // 42 (unary plus)
```

### Boolean Conversion
```javascript
// Falsy values (become false)
Boolean(0);         // false
Boolean("");        // false
Boolean(null);      // false
Boolean(undefined); // false
Boolean(NaN);       // false

// Truthy values (become true)
Boolean(1);         // true
Boolean("hello");   // true
Boolean([]);        // true (even empty array!)
Boolean({});        // true (even empty object!)
```

## Practice Exercises

```javascript
// 1. Create variables for a person
const firstName = "John";
const lastName = "Doe";
let age = 30;

// 2. Create a greeting using template literal
let greeting = `Hello, ${firstName} ${lastName}! You are ${age} years old.`;
console.log(greeting);

// 3. Check types
console.log(typeof firstName);  // ?
console.log(typeof age);        // ?
console.log(typeof true);       // ?

// 4. Type conversion practice
let strNumber = "100";
let actualNumber = Number(strNumber);
console.log(actualNumber + 50);  // 150 (not "10050")
```

## Key Takeaways

- Use `const` for values that won't change, `let` for values that will
- JavaScript has 7 primitive types: string, number, boolean, undefined, null, symbol, bigint
- Use `typeof` to check a value's type
- Be aware of type coercion - JavaScript will convert types automatically

---

**Previous:** [[01 - Introduction to JavaScript]]

**Next:** [[03 - Operators and Expressions]]

**Back to:** [[00 - Welcome]]
