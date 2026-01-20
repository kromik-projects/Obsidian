# Objects

## What are Objects?

Objects are collections of key-value pairs. They're used to store related data and functionality together. Almost everything in JavaScript is an object!

## Creating Objects

### Object Literal

```javascript
const person = {
    firstName: "Alice",
    lastName: "Smith",
    age: 25,
    isEmployed: true
};
```

### With Methods

```javascript
const person = {
    firstName: "Alice",
    lastName: "Smith",

    // Method
    getFullName() {
        return `${this.firstName} ${this.lastName}`;
    },

    // Arrow function (careful with 'this'!)
    greet: () => "Hello!"
};

console.log(person.getFullName());  // "Alice Smith"
```

### Object Constructor

```javascript
const person = new Object();
person.name = "Alice";
person.age = 25;
```

### Object.create()

```javascript
const personPrototype = {
    greet() {
        return `Hello, I'm ${this.name}`;
    }
};

const alice = Object.create(personPrototype);
alice.name = "Alice";
console.log(alice.greet());  // "Hello, I'm Alice"
```

## Accessing Properties

### Dot Notation

```javascript
const person = { name: "Alice", age: 25 };

console.log(person.name);  // "Alice"
console.log(person.age);   // 25
```

### Bracket Notation

```javascript
console.log(person["name"]);  // "Alice"

// Required for:
// - Dynamic property names
// - Property names with spaces or special characters
// - Reserved words

let key = "name";
console.log(person[key]);  // "Alice"

const obj = { "my-property": 42 };
console.log(obj["my-property"]);  // 42
```

### Optional Chaining

```javascript
const user = {
    name: "Alice",
    address: {
        city: "NYC"
    }
};

// Safe access - won't error if intermediate is undefined
console.log(user.address?.city);     // "NYC"
console.log(user.contact?.email);    // undefined (not error)
console.log(user.getInfo?.());       // undefined (safe method call)
```

## Modifying Objects

### Adding Properties

```javascript
const person = { name: "Alice" };
person.age = 25;
person["email"] = "alice@example.com";
```

### Modifying Properties

```javascript
person.name = "Bob";
person.age = 30;
```

### Deleting Properties

```javascript
delete person.age;
console.log(person.age);  // undefined
```

## Checking Properties

```javascript
const person = { name: "Alice", age: 25 };

// in operator
console.log("name" in person);     // true
console.log("email" in person);    // false

// hasOwnProperty
console.log(person.hasOwnProperty("name"));  // true

// Check for undefined (less reliable)
console.log(person.email !== undefined);  // false
```

## Object Methods

### Object.keys()

```javascript
const person = { name: "Alice", age: 25, city: "NYC" };
const keys = Object.keys(person);
console.log(keys);  // ["name", "age", "city"]
```

### Object.values()

```javascript
const values = Object.values(person);
console.log(values);  // ["Alice", 25, "NYC"]
```

### Object.entries()

```javascript
const entries = Object.entries(person);
console.log(entries);
// [["name", "Alice"], ["age", 25], ["city", "NYC"]]

// Great for iteration
for (let [key, value] of Object.entries(person)) {
    console.log(`${key}: ${value}`);
}
```

### Object.assign()

```javascript
const target = { a: 1, b: 2 };
const source = { b: 3, c: 4 };

const result = Object.assign(target, source);
console.log(result);  // { a: 1, b: 3, c: 4 }
console.log(target);  // { a: 1, b: 3, c: 4 } - modified!

// Clone an object
const clone = Object.assign({}, person);
```

### Object.freeze()

```javascript
const frozen = Object.freeze({ name: "Alice" });
frozen.name = "Bob";      // Silently fails (or error in strict mode)
frozen.age = 25;          // Silently fails
console.log(frozen.name); // "Alice"
```

### Object.seal()

```javascript
const sealed = Object.seal({ name: "Alice" });
sealed.name = "Bob";  // Works - can modify existing
sealed.age = 25;      // Fails - can't add new
delete sealed.name;   // Fails - can't delete
```

## Spread Operator with Objects

```javascript
const person = { name: "Alice", age: 25 };

// Clone
const clone = { ...person };

// Merge
const details = { city: "NYC", country: "USA" };
const full = { ...person, ...details };
console.log(full);  // { name: "Alice", age: 25, city: "NYC", country: "USA" }

// Override properties
const updated = { ...person, age: 26 };
console.log(updated);  // { name: "Alice", age: 26 }
```

## Destructuring Objects

```javascript
const person = {
    name: "Alice",
    age: 25,
    city: "NYC"
};

// Basic destructuring
const { name, age } = person;
console.log(name);  // "Alice"

// Rename variables
const { name: personName, age: personAge } = person;
console.log(personName);  // "Alice"

// Default values
const { country = "USA" } = person;
console.log(country);  // "USA"

// Nested destructuring
const user = {
    id: 1,
    profile: {
        name: "Alice",
        email: "alice@example.com"
    }
};

const { profile: { name: userName, email } } = user;
console.log(userName);  // "Alice"

// Rest pattern
const { name: n, ...rest } = person;
console.log(rest);  // { age: 25, city: "NYC" }
```

## Shorthand Properties

```javascript
const name = "Alice";
const age = 25;

// Longhand
const person1 = {
    name: name,
    age: age
};

// Shorthand (ES6+)
const person2 = { name, age };
console.log(person2);  // { name: "Alice", age: 25 }
```

## Computed Property Names

```javascript
const key = "color";
const value = "blue";

const obj = {
    [key]: value,
    [`${key}Code`]: "#0000FF"
};

console.log(obj);  // { color: "blue", colorCode: "#0000FF" }
```

## this Keyword

```javascript
const person = {
    name: "Alice",

    // Regular function - 'this' refers to the object
    greet() {
        return `Hello, I'm ${this.name}`;
    },

    // Arrow function - 'this' is inherited from outer scope
    greetArrow: () => {
        return `Hello, I'm ${this.name}`;  // 'this' is NOT person!
    }
};

console.log(person.greet());       // "Hello, I'm Alice"
console.log(person.greetArrow());  // "Hello, I'm undefined"
```

## Object Comparison

```javascript
// Objects are compared by reference, not value
const obj1 = { name: "Alice" };
const obj2 = { name: "Alice" };
const obj3 = obj1;

console.log(obj1 === obj2);  // false (different objects)
console.log(obj1 === obj3);  // true (same reference)

// Deep comparison
function deepEqual(a, b) {
    return JSON.stringify(a) === JSON.stringify(b);
}
console.log(deepEqual(obj1, obj2));  // true
```

## Practical Examples

### Configuration Object

```javascript
const config = {
    apiUrl: "https://api.example.com",
    timeout: 5000,
    retries: 3,
    headers: {
        "Content-Type": "application/json"
    }
};
```

### Factory Function

```javascript
function createPerson(name, age) {
    return {
        name,
        age,
        greet() {
            return `Hi, I'm ${this.name}`;
        },
        birthday() {
            this.age++;
        }
    };
}

const alice = createPerson("Alice", 25);
alice.birthday();
console.log(alice.age);  // 26
```

### Data Transformation

```javascript
const users = [
    { id: 1, name: "Alice", role: "admin" },
    { id: 2, name: "Bob", role: "user" },
    { id: 3, name: "Charlie", role: "user" }
];

// Create lookup object
const userById = users.reduce((acc, user) => {
    acc[user.id] = user;
    return acc;
}, {});

console.log(userById[2]);  // { id: 2, name: "Bob", role: "user" }

// Group by role
const byRole = users.reduce((acc, user) => {
    acc[user.role] = acc[user.role] || [];
    acc[user.role].push(user);
    return acc;
}, {});
```

## Practice Exercises

```javascript
// 1. Merge objects with custom logic
function merge(obj1, obj2) {
    return { ...obj1, ...obj2 };
}

// 2. Pick specific properties
function pick(obj, keys) {
    return keys.reduce((acc, key) => {
        if (key in obj) acc[key] = obj[key];
        return acc;
    }, {});
}

// 3. Omit specific properties
function omit(obj, keys) {
    const result = { ...obj };
    keys.forEach(key => delete result[key]);
    return result;
}

// 4. Deep clone (simple version)
function deepClone(obj) {
    return JSON.parse(JSON.stringify(obj));
}

// 5. Check if object is empty
function isEmpty(obj) {
    return Object.keys(obj).length === 0;
}
```

## Key Takeaways

- Objects store key-value pairs and methods
- Use dot notation for known keys, brackets for dynamic access
- Optional chaining (`?.`) safely accesses nested properties
- Spread operator (`...`) clones and merges objects
- Destructuring extracts properties into variables
- Use regular functions (not arrows) for object methods that use `this`
- Objects are compared by reference, not value

---

**Previous:** [[06 - Arrays]]

**Next:** [[08 - DOM Manipulation]]

**Back to:** [[00 - Welcome]]
