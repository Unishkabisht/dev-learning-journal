# JavaScript Learning Notes

Notes from daily JavaScript learning sessions during internship.

---

## What We Learnt

**Day 1** — DOM, element selection, DOM traversal
**Day 2** — Functions & Events
**Day 3** — Objects & Array Methods

---

# Day 1 — DOM Basics

## 1. What does JavaScript actually do?

HTML gives structure (what's on the page), CSS gives look (how it appears), and **JavaScript gives behaviour** — how the page *reacts* when a user does something (click, type, scroll, etc.).

Simple example: if clicking a button should change something — color, text, show/hide something — that's all JavaScript's job. HTML/CSS are static; JS is what makes a page **interactive**.

```
HTML (Structure) + CSS (Styling) + JavaScript (Behaviour) = Interactive Website
```

## 2. Ways to embed JavaScript

### a) Inline JS
Written directly inside an HTML tag's attribute. Fine for a quick test, not used in real projects.
```html
<button onclick="alert('Hello')">Click me</button>
```

### b) Internal JS
Written inside a `<script>` tag in the HTML file itself.
```html
<script>
  console.log("Hello from internal script");
</script>
```

### c) External JS
Code lives in its own `.js` file and gets linked into the HTML.
```html
<script src="script.js"></script>
```
This is standard practice for real projects — keeps HTML and JS separate, easier to manage, and the same file can be reused across multiple pages.

### Head vs end of body — where to put `<script>`

| Placement | What happens |
|---|---|
| `<script>` in `<head>` | Runs **before** the body's HTML exists. If the script tries to select an element at this point, it may not be loaded yet → returns `null` or throws an error |
| `<script>` at the **end of `<body>`**, just before `</body>` | By the time this runs, all the HTML has already loaded, so every element exists and is safe to select |

**Best practice: put `<script>` right before `</body>`.** That way the whole page is ready by the time JS runs, so nothing comes back as `null`.

## 3. What is the DOM?

**DOM = Document Object Model**

The DOM is a tree-like structure created by the browser when an HTML page is loaded. Every HTML element becomes an object (node) in this tree. JavaScript uses the DOM to access, modify, add, or remove elements, change text, update styles, and respond to user actions.

**DOM Traversing** means moving from one element to another within the DOM tree — finding a related parent, child, or sibling — without searching the entire document.

JavaScript doesn't edit the HTML file directly — it accesses this DOM tree and makes changes to it. The browser then instantly re-renders those changes on screen. That's why we can change/hide/recolor content without reloading the page.

Think of the DOM like a **family tree**:
```
html
 └── body
      ├── aside (class="sidebar")
      │    ├── h1: Testing
      │    └── h2: Testing2
      └── div (class="content")
           └── ul
                ├── li
                ├── li
                └── li
```

- `html` is at the top (root)
- `body` is its child
- `aside` is a child of body, and `h1`, `h2` are children of aside
- This is the **parent → child → sibling** relationship

## 4. Inspecting the DOM in Console

Open Chrome DevTools → **Console tab** → write JS directly here to poke at the DOM.

```js
document.querySelector('h2').parentElement
// <aside class="sidebar"> ... </aside>

document.querySelector('aside').children
// HTMLCollection(2) [h1, h2]
```

`document` is a global object given by the browser that represents the entire page's DOM — every DOM query starts from here.

## 5. Selecting elements — `getElement...` methods

Before `querySelector`, these were (and still are) the standard ways to grab elements:

### `getElementById`
Selects one element by its `id`. Returns a single element, since ids are meant to be unique.
```js
document.getElementById("header")
```

### `getElementsByClassName`
Selects **all** elements with a given class. Returns an `HTMLCollection` (array-like, but not a real array).
```js
document.getElementsByClassName("content")
```

### `getElementsByTagName`
Selects all elements of a given tag.
```js
document.getElementsByTagName("li")
```

`querySelector`/`querySelectorAll` are the modern replacement — they accept normal CSS selector syntax (`.class`, `#id`, `tag`, `[attr=value]`, `:nth-child()`) instead of needing a different method for every case.

**Class vs ID — the important rule:**
- **Class (`class="..."`)** — reusable. The same class can be added to multiple elements. Selector uses `.` (dot) — `.content`
- **ID (`id="..."`)** — unique, should exist on only one element on the whole page. Selector uses `#` — `#header`

Rule of thumb: if multiple elements need the same styling/behaviour → class. If you need to target one specific unique element → id.

## 6. Three ways to change content

| Property | What it does |
|---|---|
| `innerHTML` | Returns/sets the **HTML code** inside an element — if you write tags, they get rendered too |
| `textContent` | Gives/sets only **plain text**, ignores tags (includes even hidden text) |
| `innerText` | Gives only **visible text** (skips CSS-hidden text), and is styling-aware |

Simple way to remember:
- `innerHTML` → understands HTML
- `textContent` → all text, hidden or not
- `innerText` → only what's actually visible on screen

## 7. Selecting an element and changing it

```js
document.querySelector('.content ul li')
```
This selects the **first** `li` inside the `ul` inside the `.content` class (`querySelector` always returns only **one** element — the first match).

**Changing color — the risky way:**
```js
document.querySelector('.content ul li').style = "color:red"
```
This overwrites the entire inline `style` attribute (risky — wipes out any existing style).

**Safer way — change only the specific property:**
```js
document.querySelector('.content ul li').style.color = "red"
```

**Changing text:**
```js
document.querySelector('.content ul li').textContent = "HTML 4.1"
```

## 8. `:nth-child()` selector — selecting by position

```js
document.querySelector('.content ul li:nth-child(even)')
// only the first matching element (single <li>)

document.querySelectorAll('.content ul li:nth-child(even)')
// NodeList(3) [li, li, li]  → all even-positioned li's

document.querySelectorAll('.content ul li:nth-child(odd)')
// NodeList(3) [li, li, li]  → all odd-positioned li's
```

**`querySelector` vs `querySelectorAll`:**
- `querySelector` → one element (or `null` if nothing found)
- `querySelectorAll` → a `NodeList` (array-like) — loop through it to work on each element

**What `even`/`odd` means:** position is 1-indexed. So `odd` → 1st, 3rd, 5th... li. `even` → 2nd, 4th, 6th... li.

## 9. What does `()` mean?

`()` shows that we're **calling/executing a function**, and whatever is written inside it is that method's **argument/parameter**.

```js
document.querySelector('h2')
//                       ^^^^ this is the argument — tells WHAT to find
```

Without `()`, a function is just a reference, it doesn't run.

## 10. Selecting by attribute

We can also select an element by the value of one of its attributes, using square brackets `[]`:
```js
document.querySelector('[class="sidebar"]')
document.querySelector('[href="index.html"]')
document.querySelector('input[type="text"]')
```
Format: `[attributeName="value"]` — useful when an element has no class/id, but has some custom attribute.

## 11. Navigating Parent, Child, Sibling (DOM Traversal)

| Property | What it does |
|---|---|
| `.parentElement` | Gives the element directly above (parent) |
| `.children` | Gives all direct children as an `HTMLCollection` |
| `.firstElementChild` | The first child element |
| `.lastElementChild` | The last child element |
| `.nextElementSibling` | The next element beside it, within the same parent |
| `.previousElementSibling` | The previous element within the same parent |

```js
document.querySelector('h2').parentElement
// <aside class="sidebar">...</aside>

document.querySelector('aside').children
// HTMLCollection(2) [h1, h2]

document.querySelector('aside').firstElementChild
// <h1>Testing</h1>

document.querySelector('h1').nextElementSibling
// <h2>Testing2</h2>

document.querySelector('h2').previousElementSibling
// <h1>Testing</h1>
```

⚠️ If a property name is even slightly wrong, JS doesn't throw an error — it just returns `undefined`. So spelling has to be exact.

Chaining example:
```js
document.querySelector('h2').previousElementSibling.style.backgroundColor = "red"
```
Meaning: start from h2 → go to its previous sibling (h1) → set its background color to red.

---

# Day 2 — Functions & Events

## 1. What is a Function?

A function is a reusable block of code that does **one job**. Write it once, run it as many times as you need.

```js
function greet() {
  console.log("Hello!");
}

greet(); // calling it
greet(); // calling it again
```

## 2. Why Use Functions?

- **Reusability** — write once, use many times
- **Maintainability** — fix a bug in one place, not ten
- **Organized code** — each job lives in its own box
- **Easier debugging** — problems are easy to locate
- **Readability** — a good name explains what it does
- **Unit testing** — small pieces are easy to test alone

## 3. What Makes a Good Function?

- Does **one job** (single responsibility)
- Kept **short** — around 20–30 lines is a good target
- If it grows too big → **split it into smaller functions**

> Rule of thumb: if you can't describe what a function does in one short sentence, it's doing too much. Split it.

## 4. Parameters vs Arguments

```js
function add(a, b) {   // a, b = parameters (placeholders)
  return a + b;
}

let total = add(2, 3); // 2, 3 = arguments (real values)
```

**Easy trick:** Parameters = **P**laceholders. Arguments = **A**ctual values.

## 5. The `return` Statement

`return` sends a value back out of the function. Once `return` runs, the function **stops immediately**.

```js
function square(n) {
  return n * n;
  console.log("never runs"); // dead code
}
```

Functions with no `return` just *do* something (like print output) and give back `undefined`.

## 6. Function vs Procedure

| | Function | Procedure |
|---|---|---|
| Meaning | Takes input, returns a value | Just does a job |
| Example | `add(2,3)` gives back `5` | Printing to screen |
| Returns value? | Yes | No (or optional) |

**In JavaScript:** both are just called "functions." There's no separate procedure keyword.

## 7. Pure vs Impure Functions

```js
// Pure — same input, same output, no side effects
function add(a, b) {
  return a + b;
}

// Impure — changes something outside itself
let count = 0;
function tick() {
  count++;
}
```

Aim for **pure functions** where possible — predictable, easy to test and trust.

## 8. Five Ways to Write the Same Function

```js
// 1. Function declaration
function add(a, b) { return a + b; }

// 2. Function expression
const add = function(a, b) { return a + b; };

// 3. Arrow function (full body)
const add = (a, b) => { return a + b; };

// 4. Arrow function (implicit return)
const add = (a, b) => a + b;

// 5. Arrow, single param — brackets optional
const add = a => a + 1;
```

**Quick guide:**
- One line of logic? → use implicit return
- One parameter? → `()` optional
- Zero or 2+ parameters? → keep `()`

## 9. What is an Event?

An event is something that **happens on the page** — a click, key press, mouse move, form submit. You attach a function that runs when it happens.

```html
<button onclick="isClicked()">Click me!</button>

<script>
function isClicked() {
  alert("Hello!");
}
</script>
```

This is the **inline** way — quick, but not recommended for real projects. The better way is `addEventListener`.

## 10. addEventListener — the Main Tool

Give it two things: the **event name**, and the **function to run** (callback).

```js
btn.addEventListener("click", () => {
  console.log("clicked!");
});
```

Or pass a named function:
```js
function changeColor() { ... }
btn.addEventListener("mouseout", changeColor);
```

⚠️ Pass the function name **without brackets** (`changeColor`, not `changeColor()`). Brackets run it immediately instead of waiting for the event.

**Callback** = the function you hand over; the browser "calls it back" when the event fires.

## 11. The Event Object

The browser passes an `event` object with details about what happened.

```js
btn.addEventListener("click", (event) => {
  console.log(event.target); // element clicked
  console.log(event.type);   // "click"
});
```

## 12. Common Events

| Event | Fires When... |
|---|---|
| `click` | element is clicked |
| `dblclick` | element is double-clicked |
| `mousemove` | mouse moves over element |
| `mouseover` | mouse enters element |
| `mouseout` | mouse leaves element |
| `mousedown` | mouse button pressed |
| `keydown` | key is pressed down |
| `keyup` | key is released |
| `input` | field value changes while typing |
| `change` | field changes and loses focus |
| `submit` | form is submitted |
| `blur` | element loses focus |
| `scroll` | user scrolls |
| `resize` | window is resized |
| `load` | page/image finishes loading |

## 13. The Event-Handling Pattern: Select → Listen → Do

```js
// 1. Select
const btn = document.querySelector(".btn");

// 2. Handler function
function changeBackgroundColor() {
  document.body.style.background = "lightblue";
}

// 3. Listen + pass handler as callback
btn.addEventListener("mouseout", changeBackgroundColor);
```

Almost every interactive web feature is this same loop with a different event and action.

## 14. removeEventListener

```js
btn.addEventListener("click", changeColor);
// later:
btn.removeEventListener("click", changeColor);
```

**Why remove a listener?**
- One-time actions (e.g. "claim reward" button)
- Cleanup — avoid memory pile-up when element is removed
- Turning behavior off once something is done

⚠️ Only works with the **same named function**. An inline arrow `() => {...}` creates a new function each time, so it can't be removed.

## 15. What if JavaScript is Off?

This idea is called **graceful degradation** — the page should still make basic sense without JS.
- Write real HTML content and real links first
- Use JS to **enhance**, not to hold the whole page together
- If JS is the only thing making the page usable, users with it off see a broken page

**Testing tip:** Open DevTools (F12) → Settings/command menu → "Disable JavaScript" → reload and see what still works.

## Key Takeaways — Day 2

- A function should do **one thing**, and its name should say what
- **Parameters** = placeholders, **arguments** = real values
- Pass a callback **by name** (no brackets) to `addEventListener`
- To remove a listener, you need the **same named function**
- Every interactive feature = **select → listen → do**
- **Graceful degradation**: page should work without JS too

---

# Day 3 — Objects & Array Methods

## Part 1: The Brackets — `{}`, `[]`, `()`

### `{ }` Curly braces — Objects & Code Blocks

Used for two different things:

1. **Creating an object** (key-value pairs)
```js
const student = { name: "Rahul", age: 16 };
```

2. **Wrapping a block of code** — functions, loops, if-conditions
```js
function greet() {          // <- code block starts
  console.log("Hello");
}                            // <- code block ends
```

**Rule of thumb:** `key: value` pairs inside → object. Statements/logic inside → code block.

### `[ ]` Square brackets — Arrays & Bracket Access

1. **Creating an array** (ordered list of values)
```js
const marks = [92, 81, 96];
```

2. **Accessing something using a key/index**
```js
student["age"];   // access object property by key name
marks[0];          // access array item by index → 92
```

### `( )` Round brackets — Function Calls & Parameters

1. **Calling a function**
```js
console.log("Hi");
student.greet();
```

2. **Defining parameters**
```js
function add(a, b) {
  return a + b;
}
```

3. **Holding the small function you pass into an array method**
```js
products.map(p => p.name);
```

**Rule of thumb:** `( )` = "run this" or "here's the input." Never used to store data by itself.

## Part 2: Objects vs Arrays — Concept Flow

- Is it **ONE thing** with multiple properties (e.g. one student's details)? → Use an **OBJECT `{ }`**
- Is it a **LIST** of multiple things? → Use an **ARRAY `[ ]`**
- Is each item in the list also complex, with its own properties? → **Array of Objects** `[ {..}, {..}, {..} ]` ← this is the real shape of most API data

**Objects** — one entity, many properties: `{ name: "Rahul", age: 16 }`
**Arrays** — ordered collection of items: `[92, 81, 96]`
**Array of objects** — a list of entities: `[{name:"Rahul"}, {name:"Aman"}]`

## Part 3: Objects — Full Definition

An **object** stores information as **key-value pairs**, grouping related properties of one "thing" together.

```js
const student = {
  name: "Rahul",
  age: 16,
  city: "Delhi",
  marks: 92
};
```

**Accessing:**
```js
student.name;        // dot notation — most common
student["age"];       // bracket notation — key in a variable, or has spaces
```

**Add / Update / Delete:**
```js
student.school = "ABC School";  // add
student.marks = 95;             // update
delete student.city;            // delete
```

**Methods & `this`:**
```js
const student = {
  name: "Rahul",
  greet() {
    console.log("Hello " + this.name);  // this = student object
  }
};
student.greet(); // Hello Rahul
```

**Looping:**
```js
for (const key in student) {
  console.log(key, student[key]);
}
```

| Helper | Definition |
|---|---|
| `Object.keys(obj)` | new array of just the keys |
| `Object.values(obj)` | new array of just the values |
| `Object.entries(obj)` | new array of `[key, value]` pairs |

## Part 4: Array Methods — Full Definitions

```js
const products = [
  { id:1, name:"Laptop",   price:65000, stock:true },
  { id:2, name:"Mouse",    price:500,   stock:true },
  { id:3, name:"Keyboard", price:1200,  stock:false },
  { id:4, name:"Monitor",  price:18000, stock:true }
];
```

### 1. `forEach()`
Runs a function once per item. Returns nothing — pure action.
```js
products.forEach(p => console.log(p.name));
```

### 2. `map()`
Runs a function on every item, **builds a new array** from the results.
```js
const names = products.map(p => p.name);
```

### 3. `filter()`
Tests every item, keeps only ones passing the condition, returns a **new array**.
```js
const expensive = products.filter(p => p.price > 10000);
```

### 4. `find()`
Returns the **first single item** matching the condition, then stops.
```js
const laptop = products.find(p => p.name === "Laptop");
```

### 5. `some()`
`true` if **at least one** item matches.
```js
products.some(p => p.stock);
```

### 6. `every()`
`true` only if **all** items match.
```js
products.every(p => p.stock);
```

### 7. `sort()`
Reorders items using a comparison rule.
```js
products.sort((a, b) => a.price - b.price);
```

### 8. `reduce()`
Combines the whole array into **one final value**, starting from a given value.
```js
const total = products.reduce((sum, p) => sum + p.price, 0);
```

## Part 5 & 6: Which Method Do I Use? — Memorize This

| Method | Returns | One-line meaning |
|---|---|---|
| `forEach` | nothing | just do something to each item |
| `map` | new array | transform every item |
| `filter` | new array | keep matching items |
| `find` | one item | get the first match |
| `some` | true/false | is there at least one match? |
| `every` | true/false | do ALL items match? |
| `sort` | sorted array | reorder the items |
| `reduce` | one value | combine into a total |

## Part 7: Mini Practice

```js
const students = [
  { id:1, name:"Rahul", marks:92 },
  { id:2, name:"Aman",  marks:81 },
  { id:3, name:"Riya",  marks:96 }
];

// map    -> get array of all names
// filter -> get students with marks above 90
// find   -> get the student with id 2
// reduce -> get total marks of everyone
```

---

*Notes by Unishka Bisht — BCA 3rd Sem, Amrapali University, Haldwani*
