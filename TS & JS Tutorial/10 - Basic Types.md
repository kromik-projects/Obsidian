# Basic Types

## Primitive Types

TypeScript has all JavaScript primitive types plus some additions.

### string

```typescript
let name: string = "Alice";
let greeting: string = `Hello, ${name}!`;  // Template literal
let empty: string = "";
```

### number

```typescript
let integer: number = 42;
let decimal: number = 3.14;
let negative: number = -10;
let hex: number = 0xff;
let binary: number = 0b1010;
let octal: number = 0o744;
```

### boolean

```typescript
let isActive: boolean = true;
let isComplete: boolean = false;
```

### null and undefined

```typescript
let nothing: null = null;
let notDefined: undefined = undefined;

// With strict null checks, these are distinct types
let maybeString: string | null = null;
```

### symbol

```typescript
let sym1: symbol = Symbol("key");
let sym2: symbol = Symbol("key");
console.log(sym1 === sym2);  // false - symbols are unique
```

### bigint

```typescript
let big: bigint = 9007199254740991n;
let anotherBig: bigint = BigInt(9007199254740991);
```

## Special Types

### any

Opt out of type checking (avoid when possible):

```typescript
let anything: any = 42;
anything = "now a string";
anything = true;
anything.foo.bar;  // No error - dangerous!
```

> [!warning] Avoid `any`
> Using `any` defeats the purpose of TypeScript. Use `unknown` for truly unknown types.

### unknown

Safer alternative to `any`:

```typescript
let value: unknown = 42;
value = "hello";

// Must narrow type before using
if (typeof value === "string") {
    console.log(value.toUpperCase());  // OK after check
}

// value.toUpperCase();  // ❌ Error: unknown
```

### void

For functions that don't return a value:

```typescript
function logMessage(message: string): void {
    console.log(message);
}
```

### never

For functions that never return:

```typescript
// Throws an error
function throwError(message: string): never {
    throw new Error(message);
}

// Infinite loop
function infinite(): never {
    while (true) {}
}
```

## Arrays

```typescript
// Array of specific type
let numbers: number[] = [1, 2, 3];
let names: string[] = ["Alice", "Bob"];

// Generic syntax
let values: Array<number> = [1, 2, 3];

// Mixed types (avoid if possible)
let mixed: (string | number)[] = [1, "two", 3];

// Readonly array
let readonlyNums: readonly number[] = [1, 2, 3];
// readonlyNums.push(4);  // ❌ Error
```

## Tuples

Fixed-length arrays with specific types at each position:

```typescript
// Tuple definition
let person: [string, number] = ["Alice", 25];

// Access elements
let name = person[0];  // string
let age = person[1];   // number

// Named tuples (TypeScript 4.0+)
type Point = [x: number, y: number];
let coords: Point = [10, 20];

// Tuple with optional element
type Result = [number, string?];
let success: Result = [200];
let error: Result = [404, "Not Found"];

// Rest elements
type StringNumberBooleans = [string, number, ...boolean[]];
let data: StringNumberBooleans = ["hello", 42, true, false, true];
```

## Object Types

### Inline Object Type

```typescript
let user: { name: string; age: number } = {
    name: "Alice",
    age: 25
};
```

### Optional Properties

```typescript
let config: { timeout: number; retries?: number } = {
    timeout: 5000
};
```

### Readonly Properties

```typescript
let user: { readonly id: number; name: string } = {
    id: 1,
    name: "Alice"
};

user.name = "Bob";  // OK
// user.id = 2;     // ❌ Error: readonly
```

### Index Signatures

```typescript
// Object with string keys and number values
let scores: { [key: string]: number } = {};
scores.math = 95;
scores.english = 88;

// Object with any string key
let data: { [key: string]: unknown } = {
    name: "Alice",
    age: 25
};
```

## Union Types

A value that can be one of several types:

```typescript
let id: string | number;
id = "abc123";  // OK
id = 42;        // OK
// id = true;   // ❌ Error

// With null/undefined
let name: string | null = null;
name = "Alice";

// Function parameter
function printId(id: string | number): void {
    console.log(`ID: ${id}`);
}
```

### Type Narrowing

```typescript
function process(value: string | number) {
    if (typeof value === "string") {
        // TypeScript knows it's a string here
        console.log(value.toUpperCase());
    } else {
        // TypeScript knows it's a number here
        console.log(value.toFixed(2));
    }
}
```

## Literal Types

Exact values as types:

```typescript
// String literal
let direction: "north" | "south" | "east" | "west";
direction = "north";  // OK
// direction = "up";  // ❌ Error

// Number literal
let dice: 1 | 2 | 3 | 4 | 5 | 6;
dice = 4;  // OK

// Boolean literal
let success: true;
success = true;  // OK
// success = false;  // ❌ Error

// Combined with types
type Status = "pending" | "approved" | "rejected";
let orderStatus: Status = "pending";
```

## Type Aliases

Give a name to a type:

```typescript
// Simple alias
type ID = string | number;

// Object type alias
type User = {
    id: ID;
    name: string;
    email: string;
};

// Function type alias
type Callback = (data: string) => void;

// Union type alias
type Status = "active" | "inactive" | "pending";

// Using the aliases
let userId: ID = "abc123";
let user: User = { id: 1, name: "Alice", email: "alice@example.com" };
let handler: Callback = (data) => console.log(data);
```

## Enums

Named constants:

```typescript
// Numeric enum (default)
enum Direction {
    North,  // 0
    South,  // 1
    East,   // 2
    West    // 3
}

let dir: Direction = Direction.North;
console.log(dir);  // 0

// String enum
enum Status {
    Pending = "PENDING",
    Approved = "APPROVED",
    Rejected = "REJECTED"
}

let status: Status = Status.Pending;
console.log(status);  // "PENDING"

// Const enum (inlined at compile time)
const enum Color {
    Red = "#FF0000",
    Green = "#00FF00",
    Blue = "#0000FF"
}
```

> [!tip] String Enums vs Union Types
> Consider using union types instead of enums for simpler use cases:
> ```typescript
> type Status = "pending" | "approved" | "rejected";
> ```

## Type Assertions

Tell TypeScript you know the type:

```typescript
// as syntax (preferred)
let value: unknown = "hello";
let length = (value as string).length;

// Angle bracket syntax (doesn't work in JSX)
let length2 = (<string>value).length;

// Non-null assertion (use carefully!)
let element = document.getElementById("app")!;

// const assertions
let colors = ["red", "green", "blue"] as const;
// type is readonly ["red", "green", "blue"]
```

## Practice Exercises

```typescript
// 1. Define a type for a product
type Product = {
    id: number;
    name: string;
    price: number;
    inStock: boolean;
    category?: string;
};

// 2. Create a variable with union type
let result: string | null = null;
result = "Success!";

// 3. Define an enum for days
enum Day {
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}

// 4. Use literal types for status
type OrderStatus = "pending" | "processing" | "shipped" | "delivered";
let myOrder: OrderStatus = "pending";

// 5. Create a tuple for coordinates
let point: [number, number, number?] = [10, 20];
point = [10, 20, 30];  // Optional z
```

## Key Takeaways

- TypeScript has all JavaScript primitives plus `any`, `unknown`, `void`, `never`
- Prefer `unknown` over `any` for type safety
- Arrays: `number[]` or `Array<number>`
- Tuples: fixed-length arrays with specific types
- Union types: `string | number` for multiple possible types
- Type aliases: `type Name = ...` to name complex types
- Literal types: exact values like `"north"` or `1`
- Use type narrowing to work with union types safely

---

**Previous:** [[09 - Introduction to TypeScript]]

**Next:** [[11 - Interfaces and Type Aliases]]

**Back to:** [[00 - Welcome]]
