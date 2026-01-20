# Introduction to JavaScript

## What is JavaScript?

JavaScript is a versatile programming language that powers the interactive web. It's one of the most popular programming languages in the world and is essential for:

- **Web Development** - Making websites interactive
- **Server-side Development** - Building backends with Node.js
- **Mobile Apps** - Creating apps with React Native
- **Desktop Apps** - Building with Electron

## A Brief History

JavaScript was created in 1995 by Brendan Eich at Netscape in just 10 days. Despite its name, it's not related to Java - the name was a marketing decision!

Key milestones:
- **1995** - JavaScript created
- **2009** - Node.js released (JavaScript on servers)
- **2015** - ES6/ES2015 (major modernization)
- **Today** - Runs everywhere: browsers, servers, mobile, IoT

## Your First JavaScript Code

Let's write your first JavaScript! Open your browser's console (press `F12` or right-click > Inspect > Console) and type:

```javascript
console.log("Hello, World!");
```

Press Enter. You should see `Hello, World!` printed!

### What Just Happened?

- `console.log()` is a **function** that prints text
- `"Hello, World!"` is a **string** (text data)
- The semicolon `;` ends the statement (optional but recommended)

## Running JavaScript

There are several ways to run JavaScript:

### 1. Browser Console
Press `F12` in any browser and use the Console tab.

### 2. HTML File
Create an HTML file and add a script:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First JS</title>
</head>
<body>
    <script>
        console.log("Hello from HTML!");
    </script>
</body>
</html>
```

### 3. External JavaScript File
Create a `.js` file and link it:

```html
<script src="script.js"></script>
```

### 4. Node.js
Install Node.js, then run from terminal:

```bash
node script.js
```

## Basic Syntax Rules

1. **Case Sensitive** - `myVariable` and `myvariable` are different
2. **Semicolons** - Optional but recommended at end of statements
3. **Comments** - Use `//` for single line, `/* */` for multi-line
4. **Whitespace** - Generally ignored (use for readability)

```javascript
// This is a single-line comment

/* This is a
   multi-line comment */

console.log("Code here"); // Comment at end of line
```

## Practice Exercise

Try these in your browser console:

```javascript
// 1. Print your name
console.log("Your Name");

// 2. Do some math
console.log(5 + 3);
console.log(10 * 2);

// 3. Combine text
console.log("Hello, " + "World!");
```

## Key Takeaways

- JavaScript is a versatile language for web, server, and app development
- You can run JavaScript in browsers, with Node.js, or in HTML files
- `console.log()` is your friend for testing and debugging
- JavaScript is case-sensitive

---

**Next:** [[02 - Variables and Data Types]]

**Back to:** [[00 - Welcome]]
