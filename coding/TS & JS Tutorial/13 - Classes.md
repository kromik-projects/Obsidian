# Classes

## Basic Classes

Classes are blueprints for creating objects with properties and methods.

```typescript
class Person {
    // Properties
    name: string;
    age: number;

    // Constructor
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    // Method
    greet(): string {
        return `Hello, I'm ${this.name}`;
    }
}

// Creating instances
const alice = new Person("Alice", 25);
console.log(alice.greet());  // "Hello, I'm Alice"
```

## Access Modifiers

### public (default)

```typescript
class User {
    public name: string;  // Accessible everywhere

    constructor(name: string) {
        this.name = name;
    }
}

const user = new User("Alice");
console.log(user.name);  // OK
```

### private

```typescript
class BankAccount {
    private balance: number;  // Only accessible within class

    constructor(initialBalance: number) {
        this.balance = initialBalance;
    }

    deposit(amount: number): void {
        this.balance += amount;
    }

    getBalance(): number {
        return this.balance;
    }
}

const account = new BankAccount(1000);
account.deposit(500);
// account.balance;  // ❌ Error: private
console.log(account.getBalance());  // 1500
```

### protected

```typescript
class Animal {
    protected name: string;  // Accessible in class and subclasses

    constructor(name: string) {
        this.name = name;
    }
}

class Dog extends Animal {
    bark(): string {
        return `${this.name} says woof!`;  // OK - protected
    }
}

const dog = new Dog("Buddy");
// dog.name;  // ❌ Error: protected
dog.bark();   // "Buddy says woof!"
```

## Parameter Properties

Shorthand for declaring and initializing properties:

```typescript
// Long form
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

// Shorthand with parameter properties
class Person {
    constructor(
        public name: string,
        public age: number,
        private id: number = Math.random()
    ) {}
}

const person = new Person("Alice", 25);
console.log(person.name);  // "Alice"
```

## Readonly Properties

```typescript
class Config {
    readonly apiUrl: string;
    readonly timeout: number;

    constructor(apiUrl: string, timeout: number) {
        this.apiUrl = apiUrl;
        this.timeout = timeout;
    }
}

const config = new Config("https://api.example.com", 5000);
// config.apiUrl = "new url";  // ❌ Error: readonly
```

## Getters and Setters

```typescript
class Person {
    private _age: number;

    constructor(
        public name: string,
        age: number
    ) {
        this._age = age;
    }

    // Getter
    get age(): number {
        return this._age;
    }

    // Setter with validation
    set age(value: number) {
        if (value < 0) {
            throw new Error("Age cannot be negative");
        }
        this._age = value;
    }

    // Computed property
    get isAdult(): boolean {
        return this._age >= 18;
    }
}

const person = new Person("Alice", 25);
console.log(person.age);      // 25 (uses getter)
person.age = 26;              // Uses setter
console.log(person.isAdult);  // true
```

## Static Members

```typescript
class MathUtils {
    static PI = 3.14159;

    static square(n: number): number {
        return n * n;
    }

    static cube(n: number): number {
        return n * n * n;
    }
}

// Access without instantiation
console.log(MathUtils.PI);         // 3.14159
console.log(MathUtils.square(5));  // 25
```

### Static Blocks

```typescript
class Config {
    static environment: string;
    static apiUrl: string;

    // Static initialization block
    static {
        this.environment = process.env.NODE_ENV || "development";
        this.apiUrl = this.environment === "production"
            ? "https://api.example.com"
            : "http://localhost:3000";
    }
}
```

## Inheritance

```typescript
class Animal {
    constructor(public name: string) {}

    move(distance: number): void {
        console.log(`${this.name} moved ${distance} meters`);
    }
}

class Dog extends Animal {
    constructor(name: string, public breed: string) {
        super(name);  // Call parent constructor
    }

    bark(): void {
        console.log(`${this.name} barks!`);
    }

    // Override parent method
    move(distance: number): void {
        console.log("Running...");
        super.move(distance);  // Call parent method
    }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.bark();    // "Buddy barks!"
dog.move(10);  // "Running..." then "Buddy moved 10 meters"
```

## Abstract Classes

Classes that can't be instantiated directly:

```typescript
abstract class Shape {
    constructor(public color: string) {}

    // Abstract method - must be implemented
    abstract getArea(): number;

    // Concrete method - inherited as-is
    describe(): string {
        return `A ${this.color} shape`;
    }
}

class Circle extends Shape {
    constructor(color: string, public radius: number) {
        super(color);
    }

    getArea(): number {
        return Math.PI * this.radius ** 2;
    }
}

class Rectangle extends Shape {
    constructor(
        color: string,
        public width: number,
        public height: number
    ) {
        super(color);
    }

    getArea(): number {
        return this.width * this.height;
    }
}

// const shape = new Shape("red");  // ❌ Error: abstract
const circle = new Circle("red", 5);
console.log(circle.getArea());    // ~78.54
console.log(circle.describe());   // "A red shape"
```

## Implementing Interfaces

```typescript
interface Printable {
    print(): void;
}

interface Serializable {
    serialize(): string;
}

class Document implements Printable, Serializable {
    constructor(public content: string) {}

    print(): void {
        console.log(this.content);
    }

    serialize(): string {
        return JSON.stringify({ content: this.content });
    }
}
```

## Generic Classes

```typescript
class Container<T> {
    private items: T[] = [];

    add(item: T): void {
        this.items.push(item);
    }

    get(index: number): T {
        return this.items[index];
    }

    getAll(): T[] {
        return [...this.items];
    }
}

const numberContainer = new Container<number>();
numberContainer.add(1);
numberContainer.add(2);

const stringContainer = new Container<string>();
stringContainer.add("hello");
stringContainer.add("world");
```

### Generic Constraints

```typescript
interface Identifiable {
    id: number;
}

class Repository<T extends Identifiable> {
    private items: Map<number, T> = new Map();

    add(item: T): void {
        this.items.set(item.id, item);
    }

    get(id: number): T | undefined {
        return this.items.get(id);
    }

    delete(id: number): boolean {
        return this.items.delete(id);
    }
}

interface User {
    id: number;
    name: string;
}

const userRepo = new Repository<User>();
userRepo.add({ id: 1, name: "Alice" });
```

## Practical Examples

### Event Emitter

```typescript
type EventCallback = (...args: any[]) => void;

class EventEmitter {
    private events: Map<string, EventCallback[]> = new Map();

    on(event: string, callback: EventCallback): void {
        const callbacks = this.events.get(event) || [];
        callbacks.push(callback);
        this.events.set(event, callbacks);
    }

    emit(event: string, ...args: any[]): void {
        const callbacks = this.events.get(event) || [];
        callbacks.forEach(cb => cb(...args));
    }

    off(event: string, callback: EventCallback): void {
        const callbacks = this.events.get(event) || [];
        this.events.set(
            event,
            callbacks.filter(cb => cb !== callback)
        );
    }
}
```

### Singleton Pattern

```typescript
class Database {
    private static instance: Database;
    private connected = false;

    private constructor() {}  // Private constructor

    static getInstance(): Database {
        if (!Database.instance) {
            Database.instance = new Database();
        }
        return Database.instance;
    }

    connect(): void {
        this.connected = true;
        console.log("Connected to database");
    }
}

const db1 = Database.getInstance();
const db2 = Database.getInstance();
console.log(db1 === db2);  // true - same instance
```

### Builder Pattern

```typescript
class UserBuilder {
    private user: Partial<User> = {};

    setName(name: string): this {
        this.user.name = name;
        return this;
    }

    setEmail(email: string): this {
        this.user.email = email;
        return this;
    }

    setAge(age: number): this {
        this.user.age = age;
        return this;
    }

    build(): User {
        if (!this.user.name || !this.user.email) {
            throw new Error("Name and email are required");
        }
        return this.user as User;
    }
}

interface User {
    name: string;
    email: string;
    age?: number;
}

const user = new UserBuilder()
    .setName("Alice")
    .setEmail("alice@example.com")
    .setAge(25)
    .build();
```

## Practice Exercises

```typescript
// 1. Create a Stack class
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

    isEmpty(): boolean {
        return this.items.length === 0;
    }

    get size(): number {
        return this.items.length;
    }
}

// 2. Create a Logger class with levels
abstract class Logger {
    abstract log(message: string): void;

    info(message: string): void {
        this.log(`[INFO] ${message}`);
    }

    error(message: string): void {
        this.log(`[ERROR] ${message}`);
    }
}

class ConsoleLogger extends Logger {
    log(message: string): void {
        console.log(message);
    }
}

// 3. Create a class that implements multiple interfaces
interface Flyable {
    fly(): void;
}

interface Swimmable {
    swim(): void;
}

class Duck implements Flyable, Swimmable {
    fly(): void {
        console.log("Flying!");
    }

    swim(): void {
        console.log("Swimming!");
    }
}
```

## Key Takeaways

- Classes encapsulate data and behavior together
- Access modifiers: `public`, `private`, `protected`
- Parameter properties reduce constructor boilerplate
- Getters and setters provide controlled access to properties
- Static members belong to the class, not instances
- Abstract classes define contracts for subclasses
- Generics make classes reusable with different types
- Use `implements` for interfaces, `extends` for inheritance

---

**Previous:** [[12 - Functions in TypeScript]]

**Next:** [[14 - Generics]]

**Back to:** [[00 - Welcome]]
