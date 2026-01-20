# DOM Manipulation

## What is the DOM?

The **Document Object Model (DOM)** is a programming interface for web pages. It represents the page as a tree of objects that JavaScript can interact with.

```
document
└── html
    ├── head
    │   └── title
    └── body
        ├── h1
        ├── p
        └── div
            └── button
```

## Selecting Elements

### getElementById

```javascript
// Select by ID (returns single element)
const header = document.getElementById("main-header");
```

### getElementsByClassName

```javascript
// Select by class (returns live HTMLCollection)
const items = document.getElementsByClassName("list-item");
console.log(items.length);
console.log(items[0]);
```

### getElementsByTagName

```javascript
// Select by tag (returns live HTMLCollection)
const paragraphs = document.getElementsByTagName("p");
```

### querySelector (Recommended)

```javascript
// Select first matching element (CSS selector)
const header = document.querySelector("#main-header");
const firstItem = document.querySelector(".list-item");
const firstPara = document.querySelector("p");
const nested = document.querySelector("div.container > p.intro");
```

### querySelectorAll (Recommended)

```javascript
// Select all matching elements (returns static NodeList)
const items = document.querySelectorAll(".list-item");
const allParagraphs = document.querySelectorAll("p");

// Can use forEach
items.forEach(item => {
    console.log(item.textContent);
});
```

## Modifying Content

### textContent

```javascript
const heading = document.querySelector("h1");

// Get text
console.log(heading.textContent);

// Set text (safe - escapes HTML)
heading.textContent = "New Heading";
```

### innerHTML

```javascript
const container = document.querySelector(".container");

// Get HTML
console.log(container.innerHTML);

// Set HTML (careful - can execute scripts!)
container.innerHTML = "<p>New <strong>content</strong></p>";
```

### innerText

```javascript
// Similar to textContent but respects CSS styling
const element = document.querySelector(".hidden");
console.log(element.innerText);    // Empty if display:none
console.log(element.textContent);  // Shows hidden text
```

> [!warning] Security
> Never use `innerHTML` with user input - it can lead to XSS attacks!

## Modifying Attributes

### getAttribute & setAttribute

```javascript
const link = document.querySelector("a");

// Get attribute
const href = link.getAttribute("href");
console.log(href);

// Set attribute
link.setAttribute("href", "https://example.com");
link.setAttribute("target", "_blank");

// Remove attribute
link.removeAttribute("target");

// Check if exists
if (link.hasAttribute("href")) {
    console.log("Has href!");
}
```

### Direct Property Access

```javascript
const input = document.querySelector("input");

// Common properties
input.id = "username";
input.value = "Alice";
input.disabled = true;
input.placeholder = "Enter name...";

const img = document.querySelector("img");
img.src = "photo.jpg";
img.alt = "A photo";
```

### data-* Attributes

```javascript
// HTML: <div data-user-id="123" data-role="admin">
const element = document.querySelector("div");

// Access via dataset
console.log(element.dataset.userId);  // "123"
console.log(element.dataset.role);    // "admin"

// Set data attributes
element.dataset.status = "active";
```

## Modifying Styles

### Inline Styles

```javascript
const box = document.querySelector(".box");

// Set individual properties (camelCase)
box.style.backgroundColor = "blue";
box.style.width = "200px";
box.style.marginTop = "20px";

// Set multiple at once
box.style.cssText = "background: red; padding: 10px;";
```

### Classes (Recommended)

```javascript
const element = document.querySelector(".card");

// Add class
element.classList.add("active");
element.classList.add("highlight", "visible");  // Multiple

// Remove class
element.classList.remove("active");

// Toggle class
element.classList.toggle("active");  // Add if missing, remove if present

// Check for class
if (element.classList.contains("active")) {
    console.log("Is active!");
}

// Replace class
element.classList.replace("old-class", "new-class");
```

### getComputedStyle

```javascript
const element = document.querySelector(".box");
const styles = getComputedStyle(element);

console.log(styles.backgroundColor);  // Actual computed color
console.log(styles.width);            // Actual computed width
```

## Creating Elements

```javascript
// Create element
const newDiv = document.createElement("div");
newDiv.textContent = "Hello!";
newDiv.classList.add("message");

// Create text node
const text = document.createTextNode("Some text");

// Clone element
const clone = newDiv.cloneNode(true);  // true = deep clone
```

## Adding Elements to DOM

```javascript
const container = document.querySelector(".container");
const newElement = document.createElement("p");
newElement.textContent = "New paragraph";

// Append as last child
container.appendChild(newElement);

// Modern methods (recommended)
container.append(newElement);           // Last child
container.prepend(newElement);          // First child
container.before(newElement);           // Before container
container.after(newElement);            // After container

// Insert adjacent
container.insertAdjacentElement("beforebegin", newElement);  // Before
container.insertAdjacentElement("afterbegin", newElement);   // First child
container.insertAdjacentElement("beforeend", newElement);    // Last child
container.insertAdjacentElement("afterend", newElement);     // After

// Insert HTML string
container.insertAdjacentHTML("beforeend", "<p>New HTML</p>");
```

## Removing Elements

```javascript
const element = document.querySelector(".to-remove");

// Modern way
element.remove();

// Old way (still works)
element.parentNode.removeChild(element);

// Clear all children
const container = document.querySelector(".container");
container.innerHTML = "";
// or
while (container.firstChild) {
    container.removeChild(container.firstChild);
}
```

## Event Handling

### addEventListener

```javascript
const button = document.querySelector("button");

// Basic event listener
button.addEventListener("click", function(event) {
    console.log("Button clicked!");
    console.log(event.target);  // The clicked element
});

// Arrow function
button.addEventListener("click", (e) => {
    console.log("Clicked!");
});

// Named function (can be removed later)
function handleClick(e) {
    console.log("Clicked!");
}
button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);
```

### Common Events

```javascript
// Mouse events
element.addEventListener("click", handler);
element.addEventListener("dblclick", handler);
element.addEventListener("mouseenter", handler);
element.addEventListener("mouseleave", handler);
element.addEventListener("mousemove", handler);

// Keyboard events
document.addEventListener("keydown", (e) => {
    console.log(e.key);      // "Enter", "a", "Escape"
    console.log(e.code);     // "Enter", "KeyA", "Escape"
    console.log(e.ctrlKey);  // true if Ctrl pressed
});

// Form events
form.addEventListener("submit", (e) => {
    e.preventDefault();  // Stop form submission
    // Handle form data
});

input.addEventListener("input", (e) => {
    console.log(e.target.value);  // Current input value
});

input.addEventListener("change", handler);  // On blur after change
input.addEventListener("focus", handler);
input.addEventListener("blur", handler);

// Window events
window.addEventListener("load", handler);
window.addEventListener("resize", handler);
window.addEventListener("scroll", handler);
```

### Event Delegation

Handle events on parent for dynamic children:

```javascript
const list = document.querySelector("ul");

// Instead of adding listeners to each <li>
list.addEventListener("click", (e) => {
    if (e.target.tagName === "LI") {
        console.log("Clicked:", e.target.textContent);
    }
});

// Works for dynamically added items too!
```

### Event Object

```javascript
element.addEventListener("click", (e) => {
    e.target;           // Element that triggered event
    e.currentTarget;    // Element with the listener
    e.type;             // "click"
    e.preventDefault(); // Stop default behavior
    e.stopPropagation(); // Stop bubbling

    // Mouse events
    e.clientX;          // X position in viewport
    e.clientY;          // Y position in viewport
});
```

## Traversing the DOM

```javascript
const element = document.querySelector(".item");

// Parent
element.parentElement;
element.parentNode;

// Children
element.children;           // HTMLCollection of child elements
element.childNodes;         // NodeList including text nodes
element.firstElementChild;
element.lastElementChild;

// Siblings
element.previousElementSibling;
element.nextElementSibling;

// Closest ancestor matching selector
element.closest(".container");
```

## Practical Examples

### Todo List

```javascript
const form = document.querySelector("#todo-form");
const input = document.querySelector("#todo-input");
const list = document.querySelector("#todo-list");

form.addEventListener("submit", (e) => {
    e.preventDefault();

    const text = input.value.trim();
    if (!text) return;

    const li = document.createElement("li");
    li.textContent = text;

    const deleteBtn = document.createElement("button");
    deleteBtn.textContent = "Delete";
    deleteBtn.addEventListener("click", () => li.remove());

    li.appendChild(deleteBtn);
    list.appendChild(li);

    input.value = "";
});
```

### Toggle Dark Mode

```javascript
const toggleBtn = document.querySelector("#theme-toggle");

toggleBtn.addEventListener("click", () => {
    document.body.classList.toggle("dark-mode");

    const isDark = document.body.classList.contains("dark-mode");
    localStorage.setItem("theme", isDark ? "dark" : "light");
});

// Load saved preference
if (localStorage.getItem("theme") === "dark") {
    document.body.classList.add("dark-mode");
}
```

### Form Validation

```javascript
const form = document.querySelector("#signup-form");
const emailInput = document.querySelector("#email");
const errorDiv = document.querySelector("#error");

form.addEventListener("submit", (e) => {
    e.preventDefault();

    const email = emailInput.value;

    if (!email.includes("@")) {
        errorDiv.textContent = "Please enter a valid email";
        errorDiv.classList.add("visible");
        emailInput.classList.add("error");
        return;
    }

    errorDiv.classList.remove("visible");
    emailInput.classList.remove("error");
    // Submit form...
});
```

## Key Takeaways

- Use `querySelector` and `querySelectorAll` for selecting elements
- Modify content with `textContent` (safe) or `innerHTML` (be careful)
- Use `classList` methods for class manipulation
- `addEventListener` is the preferred way to handle events
- Event delegation handles dynamically created elements
- Always `preventDefault()` on form submissions you handle with JS

---

**Previous:** [[07 - Objects]]

**Next:** [[09 - Introduction to TypeScript]]

**Back to:** [[00 - Welcome]]
