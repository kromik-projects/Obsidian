# Interfaces and Type Aliases

## Interfaces

Interfaces define the shape of objects. They're one of TypeScript's most powerful features.

### Basic Interface

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

const user: User = {
    id: 1,
    name: "Alice",
    email: "alice@example.com"
};
```

### Optional Properties

```typescript
interface Config {
    apiUrl: string;
    timeout?: number;  // Optional
    retries?: number;  // Optional
}

const config: Config = {
    apiUrl: "https://api.example.com"
};
```

### Readonly Properties

```typescript
interface Point {
    readonly x: number;
    readonly y: number;
}

const origin: Point = { x: 0, y: 0 };
// origin.x = 5;  // ❌ Error: readonly
```

### Method Definitions

```typescript
interface Calculator {
    // Method signature
    add(a: number, b: number): number;

    // Alternative syntax
    subtract: (a: number, b: number) => number;
}

const calc: Calculator = {
    add(a, b) {
        return a + b;
    },
    subtract: (a, b) => a - b
};
```

### Index Signatures

```typescript
interface StringMap {
    [key: string]: string;
}

const translations: StringMap = {
    hello: "Hola",
    goodbye: "Adiós"
};

interface NumberArray {
    [index: number]: string;
}

const arr: NumberArray = ["a", "b", "c"];
```

### Extending Interfaces

```typescript
interface Person {
    name: string;
    age: number;
}

interface Employee extends Person {
    employeeId: number;
    department: string;
}

const employee: Employee = {
    name: "Alice",
    age: 30,
    employeeId: 12345,
    department: "Engineering"
};

// Extend multiple interfaces
interface Manager extends Person, Employee {
    reports: Employee[];
}
```

### Interface Merging

```typescript
// Interfaces with same name merge automatically
interface Window {
    title: string;
}

interface Window {
    close(): void;
}

// Result: Window has both 'title' and 'close'
```

## Type Aliases

Type aliases create custom names for any type.

### Basic Type Alias

```typescript
type ID = string | number;
type Name = string;
type Callback = (data: string) => void;
```

### Object Type Alias

```typescript
type User = {
    id: number;
    name: string;
    email: string;
};

const user: User = {
    id: 1,
    name: "Alice",
    email: "alice@example.com"
};
```

### Union Types

```typescript
type Status = "pending" | "approved" | "rejected";
type Result = string | number | null;

let orderStatus: Status = "pending";
```

### Intersection Types

Combine multiple types:

```typescript
type Person = {
    name: string;
    age: number;
};

type Employee = {
    employeeId: number;
    department: string;
};

// Combine both types
type StaffMember = Person & Employee;

const staff: StaffMember = {
    name: "Alice",
    age: 30,
    employeeId: 12345,
    department: "Engineering"
};
```

### Tuple Types

```typescript
type Coordinate = [number, number];
type RGB = [number, number, number];
type NameAge = [string, number];

const point: Coordinate = [10, 20];
const color: RGB = [255, 128, 0];
```

### Function Types

```typescript
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;

type EventHandler = (event: MouseEvent) => void;
type Predicate<T> = (item: T) => boolean;
```

## Interface vs Type Alias

### When to Use Interface

```typescript
// Objects and classes
interface User {
    name: string;
    age: number;
}

// When you need declaration merging
interface Window {
    customProperty: string;
}

// When extending other interfaces
interface Admin extends User {
    permissions: string[];
}
```

### When to Use Type Alias

```typescript
// Union types
type Status = "active" | "inactive";

// Tuples
type Point = [number, number];

// Function types
type Handler = (e: Event) => void;

// Complex combinations
type Response = Success | Error;

// Computed/mapped types
type Readonly<T> = { readonly [P in keyof T]: T[P] };
```

### Key Differences

| Feature | Interface | Type Alias |
|---------|-----------|------------|
| Objects | ✅ | ✅ |
| Extend/Intersect | `extends` | `&` |
| Unions | ❌ | ✅ |
| Tuples | ❌ | ✅ |
| Declaration Merging | ✅ | ❌ |
| Computed Properties | ❌ | ✅ |

## Utility Types

TypeScript provides built-in utility types:

### Partial<T>

Makes all properties optional:

```typescript
interface User {
    name: string;
    email: string;
    age: number;
}

type PartialUser = Partial<User>;
// { name?: string; email?: string; age?: number; }

function updateUser(id: number, updates: Partial<User>) {
    // Can update any subset of properties
}

updateUser(1, { name: "Bob" });  // OK
updateUser(1, { age: 26 });      // OK
```

### Required<T>

Makes all properties required:

```typescript
interface Config {
    timeout?: number;
    retries?: number;
}

type RequiredConfig = Required<Config>;
// { timeout: number; retries: number; }
```

### Readonly<T>

Makes all properties readonly:

```typescript
interface User {
    name: string;
    age: number;
}

type ReadonlyUser = Readonly<User>;

const user: ReadonlyUser = { name: "Alice", age: 25 };
// user.name = "Bob";  // ❌ Error
```

### Pick<T, K>

Select specific properties:

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age: number;
}

type UserPreview = Pick<User, "id" | "name">;
// { id: number; name: string; }
```

### Omit<T, K>

Remove specific properties:

```typescript
type UserWithoutEmail = Omit<User, "email">;
// { id: number; name: string; age: number; }
```

### Record<K, T>

Create object type with specific keys:

```typescript
type Status = "pending" | "approved" | "rejected";

type StatusCounts = Record<Status, number>;
// { pending: number; approved: number; rejected: number; }

const counts: StatusCounts = {
    pending: 5,
    approved: 10,
    rejected: 2
};
```

## Practical Examples

### API Response Types

```typescript
interface ApiResponse<T> {
    data: T;
    status: number;
    message: string;
}

interface User {
    id: number;
    name: string;
}

type UserResponse = ApiResponse<User>;
type UsersResponse = ApiResponse<User[]>;

async function fetchUser(id: number): Promise<UserResponse> {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
}
```

### Form State

```typescript
interface FormField<T> {
    value: T;
    error: string | null;
    touched: boolean;
}

interface LoginForm {
    email: FormField<string>;
    password: FormField<string>;
    rememberMe: FormField<boolean>;
}

const initialForm: LoginForm = {
    email: { value: "", error: null, touched: false },
    password: { value: "", error: null, touched: false },
    rememberMe: { value: false, error: null, touched: false }
};
```

### Event System

```typescript
interface EventMap {
    login: { userId: number; timestamp: Date };
    logout: { userId: number };
    purchase: { productId: number; amount: number };
}

type EventName = keyof EventMap;

function emit<K extends EventName>(
    event: K,
    data: EventMap[K]
): void {
    console.log(`Event: ${event}`, data);
}

emit("login", { userId: 1, timestamp: new Date() });
emit("purchase", { productId: 42, amount: 99 });
```

### React Component Props

```typescript
interface ButtonProps {
    label: string;
    onClick: () => void;
    variant?: "primary" | "secondary" | "danger";
    disabled?: boolean;
    children?: React.ReactNode;
}

// Extending HTML element props
interface InputProps extends React.InputHTMLAttributes<HTMLInputElement> {
    label: string;
    error?: string;
}
```

## Practice Exercises

```typescript
// 1. Create an interface for a blog post
interface BlogPost {
    id: number;
    title: string;
    content: string;
    author: string;
    publishedAt: Date;
    tags: string[];
    isPublished: boolean;
}

// 2. Create a type for post status
type PostStatus = "draft" | "review" | "published" | "archived";

// 3. Use Partial for update function
function updatePost(id: number, updates: Partial<BlogPost>): BlogPost {
    // Implementation
    return {} as BlogPost;
}

// 4. Create a response wrapper type
type Response<T> = {
    success: boolean;
    data: T | null;
    error: string | null;
};

// 5. Combine types with intersection
type PostWithStatus = BlogPost & { status: PostStatus };
```

## Key Takeaways

- Interfaces define object shapes and can be extended
- Type aliases can represent any type including unions and tuples
- Interfaces support declaration merging; type aliases don't
- Use interfaces for objects and classes, types for everything else
- Utility types (`Partial`, `Pick`, `Omit`, etc.) transform existing types
- Both can be used interchangeably for objects in most cases

---

**Previous:** [[10 - Basic Types]]

**Next:** [[12 - Functions in TypeScript]]

**Back to:** [[00 - Welcome]]
