# Operators and Expressions

## What are Operators?

Operators are symbols that perform operations on values. An **expression** is any code that produces a value.

## Arithmetic Operators

```javascript
let a = 10;
let b = 3;

console.log(a + b);   // 13  (Addition)
console.log(a - b);   // 7   (Subtraction)
console.log(a * b);   // 30  (Multiplication)
console.log(a / b);   // 3.333... (Division)
console.log(a % b);   // 1   (Modulus/Remainder)
console.log(a ** b);  // 1000 (Exponentiation: 10^3)
```

### Increment and Decrement

```javascript
let count = 5;

count++;  // count is now 6 (post-increment)
count--;  // count is now 5 (post-decrement)
++count;  // count is now 6 (pre-increment)
--count;  // count is now 5 (pre-decrement)

// Difference between pre and post
let x = 5;
console.log(x++);  // Prints 5, then x becomes 6
console.log(++x);  // x becomes 7, then prints 7
```

## Assignment Operators

```javascript
let x = 10;     // Basic assignment

x += 5;   // x = x + 5  → 15
x -= 3;   // x = x - 3  → 12
x *= 2;   // x = x * 2  → 24
x /= 4;   // x = x / 4  → 6
x %= 4;   // x = x % 4  → 2
x **= 3;  // x = x ** 3 → 8
```

## Comparison Operators

```javascript
let a = 5;
let b = "5";

// Equality (loose - allows type coercion)
console.log(a == b);   // true (5 == "5")
console.log(a != b);   // false

// Strict Equality (no type coercion) - RECOMMENDED
console.log(a === b);  // false (number !== string)
console.log(a !== b);  // true

// Relational
console.log(a > 3);    // true
console.log(a < 3);    // false
console.log(a >= 5);   // true
console.log(a <= 5);   // true
```

> [!warning] Always Use Strict Equality
> Use `===` and `!==` instead of `==` and `!=` to avoid unexpected type coercion bugs.

## Logical Operators

```javascript
let isLoggedIn = true;
let isAdmin = false;

// AND (&&) - both must be true
console.log(isLoggedIn && isAdmin);  // false

// OR (||) - at least one must be true
console.log(isLoggedIn || isAdmin);  // true

// NOT (!) - inverts the value
console.log(!isLoggedIn);  // false
console.log(!isAdmin);     // true
```

### Short-Circuit Evaluation

```javascript
// AND returns first falsy value or last value
console.log(null && "hello");  // null
console.log("hi" && "hello");  // "hello"

// OR returns first truthy value or last value
console.log(null || "default");   // "default"
console.log("value" || "default"); // "value"

// Common pattern: default values
let username = inputName || "Guest";
```

### Nullish Coalescing (??)

```javascript
// Only checks for null or undefined (not other falsy values)
let value = 0;
console.log(value || 10);   // 10 (0 is falsy)
console.log(value ?? 10);   // 0  (?? only checks null/undefined)

let name = null;
console.log(name ?? "Guest");  // "Guest"
```

## String Operators

```javascript
// Concatenation
let firstName = "John";
let lastName = "Doe";
let fullName = firstName + " " + lastName;  // "John Doe"

// Template literals (preferred)
let greeting = `Hello, ${firstName} ${lastName}!`;

// String comparison (alphabetical)
console.log("apple" < "banana");  // true
console.log("Zoo" < "apple");     // true (uppercase < lowercase)
```

## Ternary Operator

A shorthand for if-else:

```javascript
// condition ? valueIfTrue : valueIfFalse

let age = 20;
let status = age >= 18 ? "adult" : "minor";
console.log(status);  // "adult"

// Equivalent to:
let status2;
if (age >= 18) {
    status2 = "adult";
} else {
    status2 = "minor";
}
```

### Chained Ternary

```javascript
let score = 85;
let grade = score >= 90 ? "A"
          : score >= 80 ? "B"
          : score >= 70 ? "C"
          : score >= 60 ? "D"
          : "F";
console.log(grade);  // "B"
```

## Operator Precedence

Operations follow a specific order (like PEMDAS in math):

```javascript
// Higher precedence first
console.log(2 + 3 * 4);    // 14 (not 20)
console.log((2 + 3) * 4);  // 20 (parentheses first)

// Common precedence (high to low):
// 1. () - Parentheses
// 2. ** - Exponentiation
// 3. *, /, % - Multiplication, Division, Modulus
// 4. +, - - Addition, Subtraction
// 5. <, >, <=, >= - Comparisons
// 6. ===, !== - Equality
// 7. && - AND
// 8. || - OR
// 9. = - Assignment
```

## Practical Examples

```javascript
// Calculate total with tax
let price = 100;
let taxRate = 0.08;
let total = price + (price * taxRate);  // 108

// Check if number is even
let num = 42;
let isEven = num % 2 === 0;  // true

// Validate age range
let age = 25;
let isValidAge = age >= 18 && age <= 65;  // true

// Get display name with fallback
let user = { name: "" };
let displayName = user.name || "Anonymous";  // "Anonymous"

// Safe property access with default
let config = null;
let timeout = config?.timeout ?? 3000;  // 3000
```

## Practice Exercises

```javascript
// 1. Calculate the area of a rectangle
let width = 10;
let height = 5;
let area = width * height;
console.log(`Area: ${area}`);

// 2. Check if a number is between 1 and 100
let number = 50;
let inRange = number >= 1 && number <= 100;
console.log(`In range: ${inRange}`);

// 3. Determine pass/fail status
let examScore = 72;
let passingScore = 70;
let result = examScore >= passingScore ? "Pass" : "Fail";
console.log(`Result: ${result}`);

// 4. Calculate discount price
let originalPrice = 80;
let discountPercent = 20;
let salePrice = originalPrice - (originalPrice * discountPercent / 100);
console.log(`Sale price: $${salePrice}`);
```

## Key Takeaways

- Use `===` and `!==` for comparisons (strict equality)
- `&&` returns first falsy or last value; `||` returns first truthy or last value
- `??` only checks for null/undefined, unlike `||` which checks all falsy values
- The ternary operator `? :` is useful for simple conditionals
- Use parentheses to control operation order

---

**Previous:** [[02 - Variables and Data Types]]

**Next:** [[04 - Control Flow]]

**Back to:** [[00 - Welcome]]
