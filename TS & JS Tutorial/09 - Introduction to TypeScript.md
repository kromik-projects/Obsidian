# Introduction to TypeScript

## What is TypeScript?

TypeScript is a **superset of JavaScript** that adds optional static typing. Every valid JavaScript code is also valid TypeScript code, but TypeScript adds powerful features that help catch errors before runtime.

```
JavaScript + Types = TypeScript
```

## Why TypeScript?

### 1. Catch Errors Early

```typescript
// JavaScript - Error at runtime
function greet(name) {
    return "Hello, " + name.toUpperCase();
}
greet(42);  // Runtime error!

// TypeScript - Error at compile time
function greet(name: string) {
    return "Hello, " + name.toUpperCase();
}
greet(42);  // ❌ Compile error: number is not string
```

### 2. Better IDE Support

- Autocomplete suggestions
- Inline documentation
- Refactoring tools
- Go to definition

### 3. Self-Documenting Code

Types serve as documentation that's always up-to-date.

### 4. Safer Refactoring

The compiler catches breaking changes across your codebase.

## Setting Up TypeScript

### Installation

```bash
# Install globally
npm install -g typescript

# Or as dev dependency in project
npm install --save-dev typescript
```

### Check Version

```bash
tsc --version
```

### Create Config File

```bash
tsc --init
```

This creates `tsconfig.json`:

```json
{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "strict": true,
        "outDir": "./dist",
        "rootDir": "./src"
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules"]
}
```

## Your First TypeScript File

Create `hello.ts`:

```typescript
// Variable with type annotation
let message: string = "Hello, TypeScript!";

// Function with typed parameters and return type
function greet(name: string): string {
    return `Hello, ${name}!`;
}

console.log(greet("World"));
```

### Compile and Run

```bash
# Compile TypeScript to JavaScript
tsc hello.ts

# This creates hello.js, then run it
node hello.js
```

### Watch Mode

```bash
# Auto-compile on changes
tsc --watch
```

## Basic Type Annotations

### Variables

```typescript
// Explicit types
let name: string = "Alice";
let age: number = 25;
let isActive: boolean = true;

// Type inference (TypeScript figures it out)
let city = "NYC";  // TypeScript infers string
let count = 42;    // TypeScript infers number
```

### Functions

```typescript
// Parameter and return types
function add(a: number, b: number): number {
    return a + b;
}

// Void return (no return value)
function logMessage(msg: string): void {
    console.log(msg);
}

// Arrow functions
const multiply = (a: number, b: number): number => a * b;
```

### Arrays

```typescript
// Array of strings
let names: string[] = ["Alice", "Bob", "Charlie"];

// Array of numbers
let scores: number[] = [95, 87, 92];

// Alternative syntax
let values: Array<number> = [1, 2, 3];
```

### Objects

```typescript
// Object type annotation
let person: { name: string; age: number } = {
    name: "Alice",
    age: 25
};

// Optional properties
let user: { name: string; email?: string } = {
    name: "Bob"
};
```

## Type Inference

TypeScript is smart - it can often figure out types automatically:

```typescript
// TypeScript infers types
let name = "Alice";          // string
let age = 25;                // number
let numbers = [1, 2, 3];     // number[]

// Function return type inferred
function double(n: number) {
    return n * 2;  // Return type inferred as number
}
```

> [!tip] When to Add Type Annotations
> - Always annotate function parameters
> - Annotate when inference isn't clear
> - Let TypeScript infer when the type is obvious

## TypeScript vs JavaScript

| Feature | JavaScript | TypeScript |
|---------|-----------|------------|
| Type checking | Runtime | Compile time |
| Type annotations | No | Yes |
| Interfaces | No | Yes |
| Enums | No | Yes |
| Generics | No | Yes |
| Browser support | Direct | Needs compilation |

## Common Configuration Options

```json
{
    "compilerOptions": {
        // Target JavaScript version
        "target": "ES2020",

        // Module system
        "module": "commonjs",

        // Enable all strict checks
        "strict": true,

        // Output directory
        "outDir": "./dist",

        // Source directory
        "rootDir": "./src",

        // Generate source maps for debugging
        "sourceMap": true,

        // Allow importing JSON files
        "resolveJsonModule": true,

        // Check for unreachable code
        "noUnusedLocals": true,
        "noUnusedParameters": true
    }
}
```

## Using TypeScript with Tools

### With Node.js (ts-node)

```bash
npm install -g ts-node
ts-node hello.ts  # Run directly without compiling
```

### With React

```bash
npx create-react-app my-app --template typescript
```

### With Vite

```bash
npm create vite@latest my-app -- --template vanilla-ts
```

## Practice Exercise

Create a file `practice.ts`:

```typescript
// 1. Create typed variables
let username: string = "developer";
let level: number = 5;
let isPremium: boolean = true;

// 2. Create a typed function
function createGreeting(name: string, premium: boolean): string {
    if (premium) {
        return `Welcome back, ${name}! 🌟`;
    }
    return `Hello, ${name}!`;
}

// 3. Use the function
console.log(createGreeting(username, isPremium));

// 4. Try intentional errors (to see TypeScript catch them)
// createGreeting(42, "yes");  // ❌ Uncomment to see errors
```

Compile and run:

```bash
tsc practice.ts && node practice.js
```

## Key Takeaways

- TypeScript adds static typing to JavaScript
- Types catch errors at compile time, not runtime
- Type annotations are added after colons: `let x: number`
- TypeScript can infer many types automatically
- TypeScript compiles to plain JavaScript
- Use `tsconfig.json` to configure the compiler

---

**Previous:** [[08 - DOM Manipulation]]

**Next:** [[10 - Basic Types]]

**Back to:** [[00 - Welcome]]
