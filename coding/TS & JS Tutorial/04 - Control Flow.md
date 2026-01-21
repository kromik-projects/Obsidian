# Control Flow

## What is Control Flow?

Control flow determines the order in which code executes. By default, code runs top to bottom, but control flow statements let you make decisions and repeat actions.

## Conditional Statements

### if Statement

```javascript
let temperature = 75;

if (temperature > 80) {
    console.log("It's hot outside!");
}
```

### if...else Statement

```javascript
let age = 16;

if (age >= 18) {
    console.log("You can vote!");
} else {
    console.log("You're too young to vote.");
}
```

### if...else if...else Statement

```javascript
let score = 85;

if (score >= 90) {
    console.log("Grade: A");
} else if (score >= 80) {
    console.log("Grade: B");
} else if (score >= 70) {
    console.log("Grade: C");
} else if (score >= 60) {
    console.log("Grade: D");
} else {
    console.log("Grade: F");
}
```

### Nested if Statements

```javascript
let isLoggedIn = true;
let isAdmin = true;

if (isLoggedIn) {
    if (isAdmin) {
        console.log("Welcome, Admin!");
    } else {
        console.log("Welcome, User!");
    }
} else {
    console.log("Please log in.");
}
```

## Switch Statement

Use switch when comparing one value against many options:

```javascript
let day = 3;
let dayName;

switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    case 6:
        dayName = "Saturday";
        break;
    case 7:
        dayName = "Sunday";
        break;
    default:
        dayName = "Invalid day";
}

console.log(dayName);  // "Wednesday"
```

> [!warning] Don't Forget `break`
> Without `break`, execution "falls through" to the next case!

### Fall-Through (Intentional)

```javascript
let month = 2;
let season;

switch (month) {
    case 12:
    case 1:
    case 2:
        season = "Winter";
        break;
    case 3:
    case 4:
    case 5:
        season = "Spring";
        break;
    case 6:
    case 7:
    case 8:
        season = "Summer";
        break;
    case 9:
    case 10:
    case 11:
        season = "Fall";
        break;
    default:
        season = "Unknown";
}
```

## Loops

### for Loop

Use when you know how many times to iterate:

```javascript
// Basic for loop
for (let i = 0; i < 5; i++) {
    console.log(`Iteration ${i}`);
}
// Output: 0, 1, 2, 3, 4

// Counting backwards
for (let i = 5; i > 0; i--) {
    console.log(i);
}
// Output: 5, 4, 3, 2, 1

// Step by 2
for (let i = 0; i <= 10; i += 2) {
    console.log(i);
}
// Output: 0, 2, 4, 6, 8, 10
```

### while Loop

Use when you don't know how many iterations:

```javascript
let count = 0;

while (count < 5) {
    console.log(`Count: ${count}`);
    count++;
}

// Common pattern: user input
let password = "";
while (password !== "secret") {
    password = prompt("Enter password:");
}
```

### do...while Loop

Always executes at least once:

```javascript
let num;
do {
    num = Math.floor(Math.random() * 10);
    console.log(`Got: ${num}`);
} while (num !== 7);

console.log("Found 7!");
```

### for...of Loop

Iterate over iterable values (arrays, strings):

```javascript
// Array
let fruits = ["apple", "banana", "orange"];
for (let fruit of fruits) {
    console.log(fruit);
}

// String
let word = "Hello";
for (let char of word) {
    console.log(char);
}
```

### for...in Loop

Iterate over object keys:

```javascript
let person = {
    name: "Alice",
    age: 25,
    city: "NYC"
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}
// Output:
// name: Alice
// age: 25
// city: NYC
```

## Loop Control

### break Statement

Exit the loop immediately:

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break;  // Stop at 5
    }
    console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

### continue Statement

Skip to the next iteration:

```javascript
for (let i = 0; i < 5; i++) {
    if (i === 2) {
        continue;  // Skip 2
    }
    console.log(i);
}
// Output: 0, 1, 3, 4
```

### Labeled Statements

Control nested loops:

```javascript
outerLoop: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            break outerLoop;  // Break out of outer loop
        }
        console.log(`i=${i}, j=${j}`);
    }
}
```

## Practical Examples

### Finding an Item

```javascript
let numbers = [1, 4, 7, 2, 9, 3];
let target = 7;
let found = false;

for (let num of numbers) {
    if (num === target) {
        found = true;
        console.log("Found it!");
        break;
    }
}

if (!found) {
    console.log("Not found");
}
```

### Summing Numbers

```javascript
let sum = 0;
for (let i = 1; i <= 100; i++) {
    sum += i;
}
console.log(`Sum: ${sum}`);  // 5050
```

### FizzBuzz (Classic Exercise)

```javascript
for (let i = 1; i <= 15; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
        console.log("FizzBuzz");
    } else if (i % 3 === 0) {
        console.log("Fizz");
    } else if (i % 5 === 0) {
        console.log("Buzz");
    } else {
        console.log(i);
    }
}
```

### Validating Input

```javascript
function validateAge(age) {
    if (typeof age !== "number") {
        return "Age must be a number";
    }
    if (age < 0) {
        return "Age cannot be negative";
    }
    if (age > 150) {
        return "Age seems unrealistic";
    }
    return "Valid age";
}
```

## Practice Exercises

```javascript
// 1. Print even numbers from 1 to 20
for (let i = 2; i <= 20; i += 2) {
    console.log(i);
}

// 2. Find the first number divisible by 7 between 50 and 100
for (let i = 50; i <= 100; i++) {
    if (i % 7 === 0) {
        console.log(`Found: ${i}`);
        break;
    }
}

// 3. Count down from 10 and say "Blastoff!"
let countdown = 10;
while (countdown > 0) {
    console.log(countdown);
    countdown--;
}
console.log("Blastoff!");

// 4. Grade calculator using switch
let percentage = 85;
let grade;
switch (true) {
    case percentage >= 90:
        grade = "A";
        break;
    case percentage >= 80:
        grade = "B";
        break;
    case percentage >= 70:
        grade = "C";
        break;
    default:
        grade = "F";
}
console.log(`Grade: ${grade}`);
```

## Key Takeaways

- Use `if/else` for simple conditions, `switch` for multiple comparisons
- `for` loops are best when you know the iteration count
- `while` loops are best when iteration count is unknown
- `for...of` iterates over values, `for...in` iterates over keys
- Use `break` to exit loops and `continue` to skip iterations

---

**Previous:** [[03 - Operators and Expressions]]

**Next:** [[05 - Functions]]

**Back to:** [[00 - Welcome]]
