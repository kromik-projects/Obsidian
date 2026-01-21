# Generics

## What are Generics?

Generics allow you to write flexible, reusable code that works with multiple types while maintaining type safety. Think of them as "type variables."

```typescript
// Without generics - loses type information
function identity(value: any): any {
    return value;
}

// With generics - preserves type
function identity<T>(value: T): T {
    return value;
}

const str = identity<string>("hello");  // Type: string
const num = identity<number>(42);       // Type: number
const inferred = identity("hello");     // Type inferred: string
```

## Generic Functions

### Single Type Parameter

```typescript
function wrapInArray<T>(value: T): T[] {
    return [value];
}

wrapInArray(42);        // number[]
wrapInArray("hello");   // string[]
wrapInArray({ x: 1 });  // { x: number }[]
```

### Multiple Type Parameters

```typescript
function pair<T, U>(first: T, second: U): [T, U] {
    return [first, second];
}

pair<string, number>("age", 25);  // [string, number]
pair(true, "yes");                // [boolean, string]

function map<T, U>(arr: T[], fn: (item: T) => U): U[] {
    return arr.map(fn);
}

map([1, 2, 3], n => n.toString());  // string[]
```

## Generic Constraints

### Using `extends`

```typescript
// Constrain to types with length property
interface HasLength {
    length: number;
}

function logLength<T extends HasLength>(value: T): number {
    return value.length;
}

logLength("hello");     // OK - string has length
logLength([1, 2, 3]);   // OK - array has length
// logLength(42);       // ❌ Error - number has no length
```

### Object Key Constraints

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

const person = { name: "Alice", age: 25 };
getProperty(person, "name");  // string
getProperty(person, "age");   // number
// getProperty(person, "email");  // ❌ Error
```

### Multiple Constraints

```typescript
interface Printable {
    print(): void;
}

interface Loggable {
    log(): void;
}

function process<T extends Printable & Loggable>(item: T): void {
    item.print();
    item.log();
}
```

## Generic Interfaces

```typescript
// Generic interface
interface Container<T> {
    value: T;
    getValue(): T;
}

const numberContainer: Container<number> = {
    value: 42,
    getValue() {
        return this.value;
    }
};

// Generic interface with methods
interface Repository<T> {
    getById(id: number): T | undefined;
    getAll(): T[];
    add(item: T): void;
    update(id: number, item: T): void;
    delete(id: number): boolean;
}
```

## Generic Classes

```typescript
class Queue<T> {
    private items: T[] = [];

    enqueue(item: T): void {
        this.items.push(item);
    }

    dequeue(): T | undefined {
        return this.items.shift();
    }

    peek(): T | undefined {
        return this.items[0];
    }

    isEmpty(): boolean {
        return this.items.length === 0;
    }
}

const numberQueue = new Queue<number>();
numberQueue.enqueue(1);
numberQueue.enqueue(2);
numberQueue.dequeue();  // 1

const stringQueue = new Queue<string>();
stringQueue.enqueue("hello");
```

## Generic Type Aliases

```typescript
// Generic type alias
type Result<T> = {
    success: boolean;
    data: T | null;
    error: string | null;
};

type UserResult = Result<User>;
type OrderResult = Result<Order>;

// Generic function type
type Transformer<T, U> = (input: T) => U;

const stringify: Transformer<number, string> = (n) => n.toString();
```

## Default Type Parameters

```typescript
interface Response<T = any> {
    data: T;
    status: number;
}

// Use default
const res1: Response = { data: "anything", status: 200 };

// Override default
const res2: Response<User> = { data: { name: "Alice" }, status: 200 };

// With functions
function createArray<T = string>(length: number, value: T): T[] {
    return Array(length).fill(value);
}

createArray(3, "x");  // string[] (using default hint)
createArray<number>(3, 0);  // number[]
```

## Conditional Types

```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false

// Extract types
type ExtractArrayType<T> = T extends (infer U)[] ? U : never;

type C = ExtractArrayType<string[]>;  // string
type D = ExtractArrayType<number[]>;  // number

// Exclude and Extract
type Exclude<T, U> = T extends U ? never : T;
type Extract<T, U> = T extends U ? T : never;

type E = Exclude<"a" | "b" | "c", "a">;  // "b" | "c"
type F = Extract<"a" | "b" | "c", "a" | "b">;  // "a" | "b"
```

## Mapped Types

```typescript
// Make all properties optional
type Partial<T> = {
    [P in keyof T]?: T[P];
};

// Make all properties required
type Required<T> = {
    [P in keyof T]-?: T[P];
};

// Make all properties readonly
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

// Custom mapped type
type Nullable<T> = {
    [P in keyof T]: T[P] | null;
};

interface User {
    name: string;
    age: number;
}

type NullableUser = Nullable<User>;
// { name: string | null; age: number | null; }
```

## Utility Types (Built-in)

### Working with Object Types

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age: number;
}

// Partial - all optional
type PartialUser = Partial<User>;

// Required - all required
type RequiredUser = Required<PartialUser>;

// Readonly - all readonly
type ReadonlyUser = Readonly<User>;

// Pick - select properties
type UserPreview = Pick<User, "id" | "name">;

// Omit - exclude properties
type UserWithoutEmail = Omit<User, "email">;

// Record - create object type
type UserRoles = Record<string, User>;
```

### Working with Union Types

```typescript
type Status = "pending" | "approved" | "rejected" | null;

// Exclude - remove from union
type NonNullStatus = Exclude<Status, null>;
// "pending" | "approved" | "rejected"

// Extract - keep from union
type ApprovalStatus = Extract<Status, "approved" | "rejected">;
// "approved" | "rejected"

// NonNullable - remove null and undefined
type ValidStatus = NonNullable<Status>;
// "pending" | "approved" | "rejected"
```

### Working with Functions

```typescript
function createUser(name: string, age: number): User {
    return { id: 1, name, age, email: "" };
}

// ReturnType - get return type
type UserFromCreate = ReturnType<typeof createUser>;
// User

// Parameters - get parameter types
type CreateUserParams = Parameters<typeof createUser>;
// [string, number]

// ConstructorParameters
class MyClass {
    constructor(public x: number, public y: string) {}
}
type MyClassParams = ConstructorParameters<typeof MyClass>;
// [number, string]
```

## Practical Examples

### Generic API Response

```typescript
interface ApiResponse<T> {
    data: T;
    status: number;
    timestamp: Date;
    pagination?: {
        page: number;
        totalPages: number;
        totalItems: number;
    };
}

interface User {
    id: number;
    name: string;
}

async function fetchApi<T>(url: string): Promise<ApiResponse<T>> {
    const response = await fetch(url);
    const data = await response.json();
    return {
        data,
        status: response.status,
        timestamp: new Date()
    };
}

// Usage
const userResponse = await fetchApi<User>("/api/user/1");
console.log(userResponse.data.name);  // Typed as string
```

### Generic State Management

```typescript
interface State<T> {
    value: T;
    previousValue: T | null;
    history: T[];
}

function createState<T>(initialValue: T): {
    get: () => T;
    set: (newValue: T) => void;
    getHistory: () => T[];
} {
    const state: State<T> = {
        value: initialValue,
        previousValue: null,
        history: [initialValue]
    };

    return {
        get: () => state.value,
        set: (newValue: T) => {
            state.previousValue = state.value;
            state.value = newValue;
            state.history.push(newValue);
        },
        getHistory: () => [...state.history]
    };
}

const counter = createState(0);
counter.set(1);
counter.set(2);
console.log(counter.getHistory());  // [0, 1, 2]
```

### Generic Validation

```typescript
type ValidationResult = {
    valid: boolean;
    errors: string[];
};

type Validator<T> = (value: T) => string | null;

function validate<T>(
    value: T,
    ...validators: Validator<T>[]
): ValidationResult {
    const errors = validators
        .map(v => v(value))
        .filter((e): e is string => e !== null);

    return {
        valid: errors.length === 0,
        errors
    };
}

// String validators
const minLength = (min: number): Validator<string> =>
    (value) => value.length < min ? `Min ${min} chars` : null;

const maxLength = (max: number): Validator<string> =>
    (value) => value.length > max ? `Max ${max} chars` : null;

const result = validate("Hi", minLength(3), maxLength(10));
// { valid: false, errors: ["Min 3 chars"] }
```

## Practice Exercises

```typescript
// 1. Create a generic Stack
class Stack<T> {
    private items: T[] = [];

    push(item: T): void {
        this.items.push(item);
    }

    pop(): T | undefined {
        return this.items.pop();
    }

    peek(): T | undefined {
        return this.items[this.items.length - 1];
    }
}

// 2. Create a generic Result type
type Result<T, E = Error> =
    | { success: true; value: T }
    | { success: false; error: E };

function divide(a: number, b: number): Result<number, string> {
    if (b === 0) {
        return { success: false, error: "Cannot divide by zero" };
    }
    return { success: true, value: a / b };
}

// 3. Create a generic memoize function
function memoize<T extends (...args: any[]) => any>(
    fn: T
): T {
    const cache = new Map<string, ReturnType<T>>();

    return ((...args: Parameters<T>): ReturnType<T> => {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key)!;
        }
        const result = fn(...args);
        cache.set(key, result);
        return result;
    }) as T;
}

// 4. Create DeepPartial utility type
type DeepPartial<T> = {
    [P in keyof T]?: T[P] extends object
        ? DeepPartial<T[P]>
        : T[P];
};
```

## Key Takeaways

- Generics use `<T>` syntax to create type variables
- Constraints (`extends`) limit which types can be used
- Multiple type parameters handle complex relationships
- Default types provide fallbacks with `<T = DefaultType>`
- Mapped types transform object types systematically
- Conditional types create type-level if/else logic
- Built-in utility types solve common type transformations
- Generics preserve type information through operations

---

**Previous:** [[13 - Classes]]

**Next:** [[15 - Development Environment Setup]]

**Back to:** [[00 - Welcome]]
