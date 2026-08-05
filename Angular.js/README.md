# Day 1: Introduction to Angular – Frontend Frameworks.


---

## 1. What is Angular?

Angular is a **JavaScript framework** used to build web applications. It is made and maintained by **Google**.

A lot of developers use it because it gives many benefits over writing plain JavaScript. Let's understand those benefits one by one.

Angular takes plain HTML and makes it dynamic — it can show/hide content, repeat items in a list, and update the screen automatically based on your code, without reloading the page.

It also connects your HTML directly to your data, so if the data changes, the screen updates instantly (this is called data binding).

And it breaks your page into small reusable pieces called components, so big apps stay organized and easy to manage.

---

## 2. Why use Angular? (Benefits)

### A) Performance (Speed)
Angular apps:
- Load fast in the beginning
- Detect changes efficiently (updates only the part of the screen that changed)
- Render (show) content quickly on screen

In short: **App opens fast + app updates fast.**

Angular also gives us:
- **Modularity** → code is split into small, clean, separate parts (easy to manage)
- **Dependency Injection** → an easy way to share code/services between different parts of the app
- **Testability** → it is easy to write tests for the app

Angular keeps getting faster with every new version. Right now Angular is on **version 22**, and speed improvement is a main goal in every update.

### B) Mobile Support
Angular is built keeping mobile phones in mind from day one — touch screens, small screens, less powerful hardware, everything is considered.

Because of this, we can build **one single app** that works properly on both **mobile and desktop**, without needing extra third-party tools.

### C) Language Choice
Angular lets us write code in:
- Plain JavaScript, OR
- Newer JavaScript versions, OR
- **TypeScript** (most popular, and what we will use in this course)

Angular itself is built using TypeScript.

---

## 3. What is ECMAScript?

**ECMAScript = the official name of the JavaScript language.**

- Every year, a new version of ECMAScript is released with new features.
- ECMAScript 6 was renamed to **ES2015** (same thing, different name).
- ES2015 gave us features we use daily now — classes, modules, arrow functions.

**One-line definition:** ECMAScript is just the official name for JavaScript, and it gets a new version every year.

---

## 4. What is TypeScript?

**TypeScript = JavaScript + extra features**, made by **Microsoft**.

- It is a **superset of JavaScript** → meaning: any JavaScript code is already valid TypeScript. TypeScript just adds more on top of it.
- Browsers cannot run TypeScript directly. So there is a **compiling step** that converts TypeScript into plain JavaScript.
- Main things TypeScript adds:
  - **Types** (so you catch mistakes early)
  - Object-Oriented features like **classes, interfaces, inheritance** (similar to Java/C++)

If you already know OOP (Object-Oriented Programming), TypeScript will feel easy.
---

## 5. Flow: JavaScript → TypeScript → Angular

```
        ECMAScript (official name of JS)
                  |
                  v
        JavaScript (the actual language)
                  |
                  v
        TypeScript (JS + Types + OOP features)
                  |
          (compiling step)
                  |
                  v
        Plain JavaScript (browser understands this)
                  |
                  v
        Angular App runs in the browser
```

---

## 6. What is Angular CLI?

**CLI = Command Line Interface.** It is Angular's official tool that you use with the `ng` command.

Instead of setting up files and folders manually, CLI does all the heavy work for you:
- Creates the project
- Generates code
- Runs the app
- Builds it for release/production

**One-line definition:** Angular CLI is a helper tool you run in the terminal — it creates, builds, and runs your Angular project so you can focus only on writing the app.

### Most Used CLI Commands

| Command | What it does |
|---|---|
| `ng new <name>` | Creates a brand-new Angular project, fully set up |
| `ng serve` | Runs the app on your machine, auto-reloads on save |
| `ng generate component <name>` (short: `ng g c <name>`) | Creates a new component with all its files |
| `ng build` | Packages the app into final files for a real server |
| `ng test` | Runs your tests |
| `ng version` | Shows installed Angular/CLI versions |

**Why CLI matters:** It gives every Angular project the same clean structure, and saves hours of manual setup. One command → a whole working feature appears, correctly wired up.

---

## 7. Quick Revision (Remember This)

- Angular = popular framework from Google for building web apps
- **Performance:** fast loads + fast updates + clean modularity + dependency injection + easy testing
- **Mobile:** one single app works on both mobile & desktop
- **Language:** we write Angular in TypeScript (most popular choice)
- **ECMAScript** = official name of JavaScript
- **TypeScript** = JavaScript + types, made by Microsoft
- **Install steps:** Node.js → `npm install -g @angular/cli` → `ng new` → `ng serve`
- **CLI (`ng`)** = the tool that creates, runs, and builds your app for you

---
---

# Angular Day 2 — Components
**Full-Stack Internship · Module 5 · Frontend Frameworks**
**Instructor:** Dinesh Rawat Sir

---

## 1. What is a Component? (Simple Idea)

A **component** is a reusable, self-contained piece of the user interface (UI). It bundles three things together in one place:

- Its own **HTML** (template)
- Its own **CSS** (styles)
- Its own **TypeScript** (logic)

A website is just many components joined together, like:

```
Header component
Navigation component
Login form component
Product card component
Footer component
```

Instead of writing the same code again and again, you build a component **once** and reuse it everywhere.

### The Repetition Problem (Why Components Exist)

**Without components** — you copy-paste the same block for every product:

```html
<div class="card">
  <h2>iPhone 16</h2>
  <button>Buy</button>
</div>

<div class="card">
  <h2>Samsung S25</h2>
  <button>Buy</button>
</div>
```

Now imagine 100 products — that's 100 copies to write and fix.

**With components** — you build one `ProductCard` component and reuse it, just passing different data:

```html
<product-card name="iPhone 16"></product-card>
<product-card name="Samsung S25"></product-card>
```

Same component, different data. One piece of code, reused everywhere.

---

## 2. Why Use Components? (15 Advantages)

| # | Advantage | Meaning |
|---|-----------|---------|
| 1 | Code reusability | Write once, use many times |
| 2 | Easy maintenance | Fix a bug in one place, not many |
| 3 | Better organisation | Code split into smaller parts |
| 4 | Improved readability | Smaller files, easier to understand |
| 5 | Faster development | Reuse instead of starting from scratch |
| 6 | Consistency | Same button/card/form looks same everywhere |
| 7 | Independent development | Different devs can work on different components together |
| 8 | Easy testing | Components tested on their own |
| 9 | Scalability | Large apps easier to build & extend |
| 10 | Encapsulation | Each component manages its own logic/style without affecting others |
| 11 | Reduced duplication | No repeated HTML/CSS/JS |
| 12 | Better performance | Only changed components update, not whole page |
| 13 | Simpler debugging | Problems isolated to one component |
| 14 | Flexible composition | Complex pages built from smaller pieces |
| 15 | Easier collaboration | Teams work independently, fewer conflicts |

---

## 3. Real-World Analogy — The Car

Think of a car. It's made of independent, reusable parts:

```
Engine → Wheels → Doors → Steering → Seats
```

If a wheel breaks, you don't rebuild the whole car — you just replace that part.

Same with software: a webpage = header + sidebar + product list + cart + footer, each an independent, reusable component.

> **Note:** Plain JavaScript has **no built-in component feature**. This idea comes from frameworks/libraries like Angular, React, Vue, Svelte, and Web Components.

---

## 4. What is a Component in Angular?

In Angular, **everything on screen is a component** — the basic building block of the app.

> **An Angular component = Class + Template + Decorator**

```
┌─────────────────────────────┐
│      ANGULAR COMPONENT       │
│                               │
│  ┌─────────┐  ┌────────────┐│
│  │  CLASS  │  │  TEMPLATE  ││
│  │ (logic) │  │   (HTML)   ││
│  └─────────┘  └────────────┘│
│         ┌─────────────┐      │
│         │  DECORATOR   │      │
│         │ @Component() │      │
│         └─────────────┘      │
└─────────────────────────────┘
```

| Part | What it does |
|------|---------------|
| **Template** | Defines what the user *sees* — HTML + Angular's special syntax + data bindings |
| **Class** | Holds the data (properties) and logic (methods), written in TypeScript |
| **Decorator** | `@Component` — a special marker that adds metadata, turning a plain class into an Angular component |

---

## 5. Creating a Component with the CLI

Instead of making files by hand, ask the CLI:

```bash
ng generate component hello
```

Short form:

```bash
ng g c hello
```

This creates a folder with the component's files — the main one being **`hello.component.ts`**, where all three parts (class, template, decorator) live.

---

## 6. Building a Component — Step by Step

### Step 1: The Class

```typescript
export class AppComponent {
  name: string = "Angular";
}
```

- `name` → a **property**, type `string`, value `"Angular"`
- `export` → lets other parts of the app use this component

### Step 2: Import the Decorator

```typescript
import { Component } from "@angular/core";
```

### Step 3: Apply the Decorator + Metadata

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-hello",
  template: `<h1>Hello {{ name }}</h1>`,
})
export class AppComponent {
  name: string = "Angular";
}
```

This is a **complete Angular component**: class + template + decorator, all in one file.
Note: the template sits inside backticks (`` ` ``) so HTML can span multiple lines.

### Build Flow

```
CLASS (data + logic)
        │
        ▼
DECORATOR (@Component) ──► adds metadata (selector, template)
        │
        ▼
   TEMPLATE (HTML shown to user)
        │
        ▼
  FINAL COMPONENT
```

---

## 7. The Two Key Parts — Explained

### A. Template & Data Binding

```html
<h1>Hello {{ name }}</h1>
```

- `{{ name }}` → **data binding (interpolation)**
- Angular takes the `name` property from the class and inserts its value into the page
- Since `name = "Angular"` → page shows **"Hello Angular"**
- Change the property → page updates automatically

### B. The Selector

The **selector** is the custom HTML tag for the component.

```
selector: "app-hello"
```

Wherever Angular sees:

```html
<app-hello></app-hello>
```

...it replaces that tag with the component's template.

```
<app-hello></app-hello>   ──►   <h1>Hello Angular</h1>
     (selector tag)              (rendered output)
```

This is exactly like the `<product-card>` tag example from earlier — the selector is how you *place* a component on a page.

---

## 8. Running the App

```bash
ng serve
```

Then open:

```
http://localhost:4200
```

Result: page shows **"Hello Angular"**
- `<app-hello>` tag was replaced by the template
- `{{ name }}` was filled in from the class

---

## 9. Component Communication (Theory Only — Practice Tomorrow)

Angular components can talk to each other in a **parent → child** relationship:

```
        PARENT COMPONENT
              │
     @Input ──┼──► sends data DOWN to child
              │
              ▼
        CHILD COMPONENT
              │
    @Output ──┼──► sends events UP to parent
              │
              ▲
        PARENT COMPONENT
```

| Decorator | Direction | Purpose |
|-----------|-----------|---------|
| `@Input()` | Parent → Child | Pass data down into a child component |
| `@Output()` | Child → Parent | Send events up from child to parent |

*(Hands-on practice for this comes in the next class.)*

---

## 10. Quick Recap

- A component = reusable, self-contained UI piece (HTML + CSS + logic)
- Why: reusability, maintenance, consistency, testing, teamwork
- In Angular: **Component = Class + Template + Decorator**
  - Class → data & logic
  - Template → HTML shown to user (with `{{ }}` binding)
  - Decorator (`@Component`) → marks the class, adds selector + template
- Selector → custom tag (e.g. `app-hello`) that Angular replaces with the template
- CLI command: `ng generate component <name>` (short: `ng g c <name>`)


---
---

# Angular Learning Notes — Day 3

**Topic:** Angular Modules (NgModule) + Component Communication
**Course:** Frontend Frameworks (Module 5) — Instructor: Dinesh Rawat Sir

---

## Part 1: What is an Angular Module (NgModule)?

An **NgModule** is a container. It groups related pieces of an Angular app together — components, services, directives, and pipes — so Angular knows how everything fits and works together.

Think of it like a **folder that organizes your app's parts** so Angular can compile and run them correctly.

### The 4 Main Things a Module Holds

| Property | What it means | Simple explanation |
|---|---|---|
| `declarations` | List of components, directives, pipes that belong to THIS module | "These are mine, I own them" |
| `imports` | Other modules this module needs to use | "I am borrowing features from these modules" |
| `exports` | Declarations from this module that other modules are allowed to use | "I am sharing these with others" |
| `providers` | Services available for dependency injection in this module | "These services can be used/injected here" |

### Example Structure

```typescript
@NgModule({
  declarations: [AppComponent, HelloComponent],
  imports: [BrowserModule, FormsModule],
  exports: [HelloComponent],
  providers: [UserService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Flowchart: Inside a Module

```
                ┌─────────────────────────────┐
                │        NgModule (Box)        │
                │                              │
   declarations │  → HelloComponent            │
                │  → AppComponent              │
                │                              │
   imports      │  → BrowserModule             │
                │  → FormsModule                │
                │                              │
   exports      │  → HelloComponent (shared)   │
                │                              │
   providers    │  → UserService                │
                └─────────────────────────────┘
```

---

## Part 2: Why Do Modules Exist?

Modules exist to solve real problems in large applications. Four main reasons:

```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│ ORGANISATION │   │ REUSABILITY  │   │  SEPARATION  │   │ LAZY LOADING │
│              │   │              │   │              │   │              │
│ Groups       │   │ Share one    │   │ Keeps        │   │ Load only    │
│ related code │   │ module's     │   │ features      │   │ needed       │
│ together     │   │ features     │   │ independent  │   │ modules,     │
│              │   │ across app   │   │ of each other│   │ not all at   │
│              │   │              │   │              │   │ once         │
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
```

1. **Organisation** — Instead of one giant messy file, code is split into logical groups (e.g., `UserModule`, `AdminModule`).
2. **Reusability** — A module built once (like a `SharedModule` with common buttons/cards) can be reused in many places.
3. **Separation** — Different features (e.g., Login, Dashboard, Reports) stay independent, making bugs easier to isolate.
4. **Lazy Loading** — App loads faster because Angular only loads a module when the user actually navigates to that feature, not all at the start.

---

## Part 3: Important Point — Modules Are Now Optional

> ⚠️ **This is a key modern-Angular update.**

- Older Angular (before v14) — **Every component had to belong to a module.** No exceptions.
- Modern Angular (v14+) — **Standalone Components** were introduced. A component can now work on its own, without being declared inside an `NgModule`.

### Why This Matters

```
   OLD ANGULAR WAY                    MODERN ANGULAR WAY
┌───────────────────┐             ┌───────────────────┐
│     NgModule        │             │  Standalone         │
│  ┌──────────────┐   │             │  Component            │
│  │  Component    │   │    VS      │  (works alone,       │
│  │  (needs module)│   │             │   imports its own    │
│  └──────────────┘   │             │   dependencies        │
└───────────────────┘             │   directly)            │
                                     └───────────────────┘
```

**Rule of thumb:**
- Learn NgModules → to **read and understand old Angular projects** (still very common in real jobs).
- Use Standalone Components → for **new Angular projects going forward** (this is the modern default).

Good question to confirm with Dinesh Sir: check whether your `resume-forge` project has an `app.module.ts` file. If it does NOT, your project is already using standalone components.

---

## Part 4: Component Communication (Theory)

In Angular, components are often nested — a **parent** component contains a **child** component. They need ways to talk to each other.

### The Two Directions

```
              PARENT COMPONENT
                     │
        @Input()     │     @Output()
       (data goes    │    (event goes
          DOWN)       │        UP)
                     │
                     ▼
              CHILD COMPONENT
```

### @Input() — Parent sends data DOWN to Child

- Used when a **parent** wants to pass data **into** a child component.
- The child receives it like a normal property.

```typescript
// child.component.ts
@Input() userName: string;
```

```html
<!-- parent.component.html -->
<app-child [userName]="parentUserName"></app-child>
```

### @Output() — Child sends events UP to Parent

- Used when a **child** wants to tell the **parent** that something happened (like a button click).
- Works together with `EventEmitter`.
- The parent listens using `$event`.

```typescript
// child.component.ts
@Output() itemSelected = new EventEmitter<string>();

selectItem() {
  this.itemSelected.emit('Item A');
}
```

```html
<!-- parent.component.html -->
<app-child (itemSelected)="onItemSelected($event)"></app-child>
```

```typescript
// parent.component.ts
onItemSelected(value: string) {
  console.log(value); // 'Item A'
}
```

### Flowchart: Full Communication Cycle

```
   PARENT                                      CHILD
┌─────────────┐                          ┌─────────────┐
│              │  [userName]="data"       │              │
│              │ ───────────────────────► │  @Input()    │
│              │      (data flows down)    │  userName    │
│              │                          │              │
│              │  (itemSelected)="fn()"    │              │
│  onItemSel-  │ ◄─────────────────────── │  @Output()   │
│  ected()     │   (event flows up via     │  itemSelected│
│              │    $event)                │  .emit()     │
└─────────────┘                          └─────────────┘
```

---

## Part 5: Understanding Brackets in Angular

This is one of the most confusing parts for beginners — here is the simple breakdown:

| Syntax | Name | Direction | What it does |
|---|---|---|---|
| `{{ }}` | Interpolation | Component → Template (display only) | Displays a value from TypeScript inside HTML text |
| `[ ]` | Property Binding | Parent → Child (data IN) | Passes data INTO an element or component property |
| `( )` | Event Binding | Child → Parent (event OUT) | Listens for an event and runs a function when it happens |
| `[( )]` | Two-Way Binding (Banana in a Box) | Both directions | Combines property binding + event binding together |

### 1. `{{ }}` — Interpolation

Used to **display** a value from your TypeScript class directly in the HTML.

```typescript
name = 'Unishka';
```
```html
<h1>Hello, {{ name }}!</h1>
<!-- Output: Hello, Unishka! -->
```

- It is **one-way**: data flows from component → template only, just to show text.
- Cannot be used to set attributes or listen to events — only to display data.

### 2. `[ ]` — Property Binding (Data IN)

Used to **pass data** into an HTML element's property or a child component's `@Input`.

```html
<img [src]="imageUrl">
<app-child [userName]="name"></app-child>
```

- One-way: component → element/child.
- Square brackets = "sending data in."

### 3. `( )` — Event Binding (Event OUT)

Used to **listen** for events like clicks, typing, or custom `@Output` events, and run a method in response.

```html
<button (click)="sayHello()">Click Me</button>
```

- One-way: element/child → component.
- Round brackets = "catching an event out."

### 4. `[( )]` — Two-Way Binding (Bonus, good to know)

Combines both — often used with form inputs via `ngModel`.

```html
<input [(ngModel)]="name">
```

- This is called **"banana in a box"** (funny nickname because `[( )]` looks like a banana inside a box).
- Data flows both ways: if `name` changes in TypeScript, the input updates; if user types in the input, `name` updates too.

### Quick Visual Summary

```
{{ }}   →  DISPLAY ONLY        (one-way, component → HTML text)
[ ]     →  DATA IN             (one-way, component → element/child)
( )     →  EVENT OUT           (one-way, element/child → component)
[( )]   →  DATA IN + EVENT OUT (two-way, both directions at once)
```

---

## Summary — Day 3 Key Takeaways

1. **NgModule** = container holding `declarations`, `imports`, `exports`, `providers`.
2. Modules exist for **organisation, reusability, separation, and lazy loading**.
3. Modern Angular (v14+) uses **standalone components by default** — modules are now optional. Learn modules to read old code; use standalone for new work.
4. **@Input()** sends data DOWN (parent → child). **@Output()** with `EventEmitter` sends events UP (child → parent), read using `$event`.
5. Bracket cheat sheet:
   - `{{ }}` = Interpolation (display, one-way)
   - `[ ]` = Property Binding (data in, one-way)
   - `( )` = Event Binding (event out, one-way)
   - `[( )]` = Two-Way Binding (both directions)

---
---

