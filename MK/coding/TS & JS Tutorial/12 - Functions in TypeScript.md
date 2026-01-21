# Functions in TypeScript

## Function Type Annotations

### Basic Function Types

```typescript
// Named function
function add(a: number, b: number): number {
    return a + b;
}

// Function expression
const multiply = function(a: number, b: number): number {
    return a * b;
};

// Arrow function
const divide = (a: number, b: number): number => a / b;
```

### Void Return Type

```typescript
function logMessage(message: string): void {
    console.log(message);
    // No return statement needed
}

// Arrow function with void
const greet = (name: string): void => {
    console.log(`Hello, ${name}!`);
};
```

### Type Inference for Returns

```typescript
// TypeScript infers the return type as number
function double(n: number) {
    return n * 2;
}

// Explicit is better for complex functions
function processData(data: string): { success: boolean; result: string } {
    return { success: true, result: data.toUpperCase() };
}
```

## Optional and Default Parameters

### Optional Parameters

```typescript
function greet(name: string, greeting?: string): string {
    if (greeting) {
        return `${greeting}, ${name}!`;
    }
    return `Hello, ${name}!`;
}

greet("Alice");           // "Hello, Alice!"
greet("Alice", "Hi");     // "Hi, Alice!"
```

### Default Parameters

```typescript
function greet(name: string, greeting: string = "Hello"): string {
    return `${greeting}, ${name}!`;
}

greet("Alice");           // "Hello, Alice!"
greet("Alice", "Hi");     // "Hi, Alice!"

// With complex defaults
function createUser(
    name: string,
    role: string = "user",
    createdAt: Date = new Date()
) {
    return { name, role, createdAt };
}
```

## Rest Parameters

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((total, n) => total + n, 0);
}

sum(1, 2, 3);        // 6
sum(1, 2, 3, 4, 5);  // 15

// With other parameters
function log(level: string, ...messages: string[]): void {
    console.log(`[${level}]`, ...messages);
}

log("INFO", "Server started", "Port 3000");
```

## Function Type Expressions

### Type Alias for Functions

```typescript
// Define function type
type MathOperation = (a: number, b: number) => number;

// Use the type
const add: MathOperation = (a, b) => a + b;
const subtract: MathOperation = (a, b) => a - b;
const multiply: MathOperation = (a, b) => a * b;
```

### Call Signatures

```typescript
// Object with call signature
type Logger = {
    (message: string): void;
    level: string;
};

const logger: Logger = (message) => {
    console.log(`[${logger.level}] ${message}`);
};
logger.level = "INFO";
logger("Hello!");  // [INFO] Hello!
```

### Construct Signatures

```typescript
interface PersonConstructor {
    new (name: string, age: number): Person;
}

class Person {
    constructor(public name: string, public age: number) {}
}

function createPerson(
    ctor: PersonConstructor,
    name: string,
    age: number
): Person {
    return new ctor(name, age);
}
```

## Generic Functions

Functions that work with multiple types:

```typescript
// Generic function
function identity<T>(value: T): T {
    return value;
}

identity<string>("hello");  // "hello"
identity<number>(42);       // 42
identity("hello");          // Type inferred as string

// Multiple type parameters
function pair<T, U>(first: T, second: U): [T, U] {
    return [first, second];
}

pair<string, number>("age", 25);  // ["age", 25]
pair("name", "Alice");            // Inferred: [string, string]
```

### Generic Constraints

```typescript
// Constrain to types with length
interface HasLength {
    length: number;
}

function logLength<T extends HasLength>(value: T): number {
    console.log(value.length);
    return value.length;
}

logLength("hello");     // 5
logLength([1, 2, 3]);   // 3
logLength({ length: 10 }); // 10
// logLength(123);      // ❌ Error: number has no length

// Constrain to object keys
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

const person = { name: "Alice", age: 25 };
getProperty(person, "name");  // "Alice"
// getProperty(person, "email");  // ❌ Error
```

## Overloaded Functions

Multiple signatures for different parameter types:

```typescript
// Overload signatures
function format(value: string): string;
function format(value: number): string;
function format(value: Date): string;

// Implementation signature
function format(value: string | number | Date): string {
    if (typeof value === "string") {
        return value.trim();
    } else if (typeof value === "number") {
        return value.toFixed(2);
    } else {
        return value.toISOString();
    }
}

format("  hello  ");  // "hello"
format(42.5);         // "42.50"
format(new Date());   // "2024-01-15T..."
```

### Practical Overloading

```typescript
// Array find with different returns
function find<T>(arr: T[], predicate: (item: T) => boolean): T | undefined;
function find<T>(arr: T[], predicate: (item: T) => boolean, defaultValue: T): T;

function find<T>(
    arr: T[],
    predicate: (item: T) => boolean,
    defaultValue?: T
): T | undefined {
    const found = arr.find(predicate);
    return found !== undefined ? found : defaultValue;
}

const nums = [1, 2, 3];
find(nums, n => n > 5);        // number | undefined
find(nums, n => n > 5, 0);     // number (with default)
```

## Callbacks and Higher-Order Functions

### Callback Types

```typescript
// Simple callback
function fetchData(callback: (data: string) => void): void {
    setTimeout(() => {
        callback("Data loaded!");
    }, 1000);
}

// Callback with error handling
type Callback<T> = (error: Error | null, result: T | null) => void;

function readFile(path: string, callback: Callback<string>): void {
    // Simulated async operation
    if (path) {
        callback(null, "File contents");
    } else {
        callback(new Error("Path required"), null);
    }
}
```

### Higher-Order Functions

```typescript
// Function that returns a function
function createMultiplier(multiplier: number): (n: number) => number {
    return (n) => n * multiplier;
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

double(5);  // 10
triple(5);  // 15

// Function that takes a function
function transform<T, U>(
    items: T[],
    transformer: (item: T) => U
): U[] {
    return items.map(transformer);
}

transform([1, 2, 3], n => n * 2);          // [2, 4, 6]
transform(["a", "b"], s => s.toUpperCase()); // ["A", "B"]
```

## Async Functions

```typescript
// Async function with Promise return
async function fetchUser(id: number): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
}

// Type the resolved value
interface User {
    id: number;
    name: string;
}

async function getUsers(): Promise<User[]> {
    const response = await fetch("/api/users");
    return response.json();
}

// Using the async function
async function main() {
    const user: User = await fetchUser(1);
    const users: User[] = await getUsers();
}
```

## this Parameter

```typescript
interface Button {
    label: string;
    onClick: (this: Button, e: Event) => void;
}

const button: Button = {
    label: "Submit",
    onClick: function(e) {
        console.log(this.label);  // TypeScript knows 'this' is Button
    }
};

// Explicit this type in functions
function handleClick(this: HTMLButtonElement, e: Event): void {
    console.log(this.textContent);
}
```

## Practical Examples

### Event Handler Factory

```typescript
type EventHandler<T extends Event> = (event: T) => void;

function createClickHandler(
    callback: (x: number, y: number) => void
): EventHandler<MouseEvent> {
    return (event) => {
        callback(event.clientX, event.clientY);
    };
}

const handler = createClickHandler((x, y) => {
    console.log(`Clicked at ${x}, ${y}`);
});
```

### API Wrapper

```typescript
interface ApiResponse<T> {
    data: T;
    status: number;
}

async function apiCall<T>(
    url: string,
    options?: RequestInit
): Promise<ApiResponse<T>> {
    const response = await fetch(url, options);
    const data = await response.json();
    return {
        data: data as T,
        status: response.status
    };
}

// Usage
interface User {
    id: number;
    name: string;
}

const result = await apiCall<User>("/api/user/1");
console.log(result.data.name);
```

### Validation Functions

```typescript
type Validator<T> = (value: T) => string | null;

function validate<T>(
    value: T,
    ...validators: Validator<T>[]
): string[] {
    return validators
        .map(v => v(value))
        .filter((error): error is string => error !== null);
}

const minLength = (min: number): Validator<string> =>
    (value) => value.length < min ? `Min ${min} characters` : null;

const maxLength = (max: number): Validator<string> =>
    (value) => value.length > max ? `Max ${max} characters` : null;

const errors = validate("Hi", minLength(3), maxLength(10));
// ["Min 3 characters"]
```

## Practice Exercises

```typescript
// 1. Create a typed filter function
function filter<T>(
    array: T[],
    predicate: (item: T) => boolean
): T[] {
    return array.filter(predicate);
}

// 2. Create a debounce function with types
function debounce<T extends (...args: any[]) => any>(
    func: T,
    delay: number
): (...args: Parameters<T>) => void {
    let timeoutId: NodeJS.Timeout;
    return (...args) => {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => func(...args), delay);
    };
}

// 3. Create a compose function
function compose<T>(
    ...fns: Array<(arg: T) => T>
): (arg: T) => T {
    return (arg) => fns.reduceRight((acc, fn) => fn(acc), arg);
}

// 4. Create a memoize function
function memoize<T extends (...args: any[]) => any>(
    fn: T
): T {
    const cache = new Map<string, ReturnType<T>>();
    return ((...args: Parameters<T>) => {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);
        }
        const result = fn(...args);
        cache.set(key, result);
        return result;
    }) as T;
}
```

## Key Takeaways

- Always type function parameters; return types can often be inferred
- Use optional (`?`) and default parameters for flexibility
- Generic functions work with multiple types safely
- Overloads provide different signatures for the same function
- Type callbacks and higher-order functions for better safety
- Async functions return `Promise<T>`
- Use `this` parameter to type method context

---

**Previous:** [[11 - Interfaces and Type Aliases]]

**Next:** [[13 - Classes]]

**Back to:** [[00 - Welcome]]
