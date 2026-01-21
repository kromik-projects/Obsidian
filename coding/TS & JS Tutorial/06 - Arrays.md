# Arrays

## What are Arrays?

Arrays are ordered collections of values. They can hold any type of data and are one of the most commonly used data structures in JavaScript.

## Creating Arrays

```javascript
// Array literal (preferred)
let fruits = ["apple", "banana", "orange"];

// Array constructor
let numbers = new Array(1, 2, 3);

// Empty array
let empty = [];

// Mixed types (valid but not recommended)
let mixed = [1, "hello", true, null];

// Array.from() - create from iterable
let chars = Array.from("hello");  // ["h", "e", "l", "l", "o"]

// Array.of() - create from arguments
let nums = Array.of(1, 2, 3);  // [1, 2, 3]
```

## Accessing Elements

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

// By index (0-based)
console.log(fruits[0]);  // "apple"
console.log(fruits[2]);  // "orange"

// Last element
console.log(fruits[fruits.length - 1]);  // "mango"

// Using at() - supports negative indices
console.log(fruits.at(-1));  // "mango"
console.log(fruits.at(-2));  // "orange"

// Modifying elements
fruits[1] = "blueberry";
console.log(fruits);  // ["apple", "blueberry", "orange", "mango"]
```

## Array Properties and Methods

### Length

```javascript
let fruits = ["apple", "banana", "orange"];
console.log(fruits.length);  // 3

// Can be modified (truncates or extends)
fruits.length = 2;
console.log(fruits);  // ["apple", "banana"]
```

### Adding Elements

```javascript
let fruits = ["apple"];

// Add to end
fruits.push("banana");        // ["apple", "banana"]
fruits.push("orange", "mango"); // Add multiple

// Add to beginning
fruits.unshift("grape");      // ["grape", "apple", "banana", ...]

// Add at specific index
fruits.splice(2, 0, "kiwi");  // Insert at index 2
```

### Removing Elements

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

// Remove from end
let last = fruits.pop();      // "mango"

// Remove from beginning
let first = fruits.shift();   // "apple"

// Remove at specific index
fruits.splice(1, 1);          // Remove 1 element at index 1

// Remove multiple elements
fruits.splice(0, 2);          // Remove 2 elements starting at 0
```

### Finding Elements

```javascript
let fruits = ["apple", "banana", "orange", "banana"];

// Find index
console.log(fruits.indexOf("banana"));     // 1 (first occurrence)
console.log(fruits.lastIndexOf("banana")); // 3 (last occurrence)
console.log(fruits.indexOf("grape"));      // -1 (not found)

// Check if exists
console.log(fruits.includes("orange"));    // true

// Find with condition
let numbers = [1, 5, 10, 15, 20];
let found = numbers.find(n => n > 8);      // 10 (first match)
let index = numbers.findIndex(n => n > 8); // 2 (index of first match)
```

## Iterating Arrays

### for Loop

```javascript
let fruits = ["apple", "banana", "orange"];

for (let i = 0; i < fruits.length; i++) {
    console.log(`${i}: ${fruits[i]}`);
}
```

### for...of Loop

```javascript
for (let fruit of fruits) {
    console.log(fruit);
}
```

### forEach Method

```javascript
fruits.forEach((fruit, index) => {
    console.log(`${index}: ${fruit}`);
});
```

## Transforming Arrays

### map() - Transform Each Element

```javascript
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(n => n * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]

// Original unchanged
console.log(numbers);  // [1, 2, 3, 4, 5]

// Practical example
let users = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 }
];
let names = users.map(user => user.name);
console.log(names);  // ["Alice", "Bob"]
```

### filter() - Keep Matching Elements

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let evens = numbers.filter(n => n % 2 === 0);
console.log(evens);  // [2, 4, 6, 8, 10]

let greaterThan5 = numbers.filter(n => n > 5);
console.log(greaterThan5);  // [6, 7, 8, 9, 10]

// Practical example
let products = [
    { name: "Laptop", price: 999 },
    { name: "Phone", price: 699 },
    { name: "Tablet", price: 499 }
];
let expensive = products.filter(p => p.price > 500);
```

### reduce() - Combine to Single Value

```javascript
let numbers = [1, 2, 3, 4, 5];

// Sum
let sum = numbers.reduce((acc, n) => acc + n, 0);
console.log(sum);  // 15

// Max value
let max = numbers.reduce((max, n) => n > max ? n : max, numbers[0]);
console.log(max);  // 5

// Count occurrences
let letters = ["a", "b", "a", "c", "a", "b"];
let counts = letters.reduce((acc, letter) => {
    acc[letter] = (acc[letter] || 0) + 1;
    return acc;
}, {});
console.log(counts);  // { a: 3, b: 2, c: 1 }
```

### Chaining Methods

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

let result = numbers
    .filter(n => n % 2 === 0)     // [2, 4, 6, 8, 10]
    .map(n => n * 2)               // [4, 8, 12, 16, 20]
    .reduce((sum, n) => sum + n);  // 60

console.log(result);  // 60
```

## Other Useful Methods

### Sorting

```javascript
let fruits = ["orange", "apple", "banana"];
fruits.sort();
console.log(fruits);  // ["apple", "banana", "orange"]

// Numbers need a compare function!
let numbers = [10, 5, 8, 1, 7];
numbers.sort((a, b) => a - b);  // Ascending
console.log(numbers);  // [1, 5, 7, 8, 10]

numbers.sort((a, b) => b - a);  // Descending
console.log(numbers);  // [10, 8, 7, 5, 1]
```

### Reversing

```javascript
let arr = [1, 2, 3];
arr.reverse();
console.log(arr);  // [3, 2, 1]
```

### Slicing (Non-destructive)

```javascript
let fruits = ["apple", "banana", "orange", "mango"];

let some = fruits.slice(1, 3);  // ["banana", "orange"]
let fromEnd = fruits.slice(-2); // ["orange", "mango"]
let copy = fruits.slice();      // Full copy
```

### Joining

```javascript
let fruits = ["apple", "banana", "orange"];

console.log(fruits.join());       // "apple,banana,orange"
console.log(fruits.join(" - ")); // "apple - banana - orange"
console.log(fruits.join(""));    // "applebananaorange"
```

### Concatenating

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];

let combined = arr1.concat(arr2);
console.log(combined);  // [1, 2, 3, 4]

// Spread operator (preferred)
let combined2 = [...arr1, ...arr2];
console.log(combined2);  // [1, 2, 3, 4]
```

### Flattening

```javascript
let nested = [[1, 2], [3, 4], [5, 6]];
let flat = nested.flat();
console.log(flat);  // [1, 2, 3, 4, 5, 6]

let deepNested = [1, [2, [3, [4]]]];
let deepFlat = deepNested.flat(Infinity);
console.log(deepFlat);  // [1, 2, 3, 4]
```

## Checking Arrays

```javascript
// some() - at least one matches
let numbers = [1, 2, 3, 4, 5];
console.log(numbers.some(n => n > 3));   // true
console.log(numbers.some(n => n > 10));  // false

// every() - all match
console.log(numbers.every(n => n > 0));  // true
console.log(numbers.every(n => n > 3));  // false

// Check if array
console.log(Array.isArray([1, 2]));      // true
console.log(Array.isArray("hello"));     // false
```

## Destructuring Arrays

```javascript
let colors = ["red", "green", "blue"];

// Basic destructuring
let [first, second, third] = colors;
console.log(first);  // "red"

// Skip elements
let [, , last] = colors;
console.log(last);  // "blue"

// Rest pattern
let [head, ...rest] = colors;
console.log(head);  // "red"
console.log(rest);  // ["green", "blue"]

// Default values
let [a, b, c, d = "yellow"] = colors;
console.log(d);  // "yellow"

// Swapping variables
let x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y);  // 2, 1
```

## Practice Exercises

```javascript
// 1. Find the sum of an array
function sum(arr) {
    return arr.reduce((total, n) => total + n, 0);
}

// 2. Find the average
function average(arr) {
    return arr.reduce((sum, n) => sum + n, 0) / arr.length;
}

// 3. Remove duplicates
function unique(arr) {
    return [...new Set(arr)];
}

// 4. Get the first n elements
function take(arr, n) {
    return arr.slice(0, n);
}

// 5. Chunk array into groups
function chunk(arr, size) {
    const chunks = [];
    for (let i = 0; i < arr.length; i += size) {
        chunks.push(arr.slice(i, i + size));
    }
    return chunks;
}

console.log(chunk([1, 2, 3, 4, 5], 2));  // [[1, 2], [3, 4], [5]]
```

## Key Takeaways

- Arrays are ordered, zero-indexed collections
- Use `push/pop` for end operations, `shift/unshift` for beginning
- `map`, `filter`, and `reduce` are the most important array methods
- Always use a compare function when sorting numbers
- Spread operator `...` is useful for copying and combining arrays
- Destructuring makes working with arrays more elegant

---

**Previous:** [[05 - Functions]]

**Next:** [[07 - Objects]]

**Back to:** [[00 - Welcome]]
