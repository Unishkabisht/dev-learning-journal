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
# Angular Day 4 — Component Lifecycle Hooks

**Module 5 · Frontend Frameworks · Angular**
**Instructor:** Dinesh Rawat Sir
**Topic:** Understanding the life of a component, and how to "catch" its important moments

---

## 1. The Big Idea (in one line)

> A **lifecycle hook** is a method that Angular calls **automatically**, at a fixed moment in a component's life. You just write the method — Angular decides *when* to call it.

Think of it like a **delivery tracking app**:
- You don't manually check "has my order been packed yet?"
- The app **notifies you automatically** at each stage: Order Placed → Packed → Shipped → Delivered.

Angular does the same thing with components. It notifies your code automatically at each stage of a component's life — you just have to "listen" by writing the right method.

**Golden rule:** Every lifecycle hook method name starts with `ng` (e.g. `ngOnInit`, `ngOnDestroy`). This is Angular's way of saying "this method belongs to my internal system, not to you."

---

## 2. Why Does a Component Even Have a "Life"?

A component in Angular is not just static HTML. It goes through real stages, just like a living thing:

```
   BORN            LIVING             UPDATING           DYING
(created)     (shown on screen)    (data changes)     (removed)
    │                 │                   │                │
    ▼                 ▼                   ▼                ▼
constructor()   ngAfterViewInit()   ngOnChanges()      ngOnDestroy()
ngOnChanges()                       ngDoCheck()
ngOnInit()
```

At **each stage**, Angular gives you a "hook" — a chance to plug in your own code.

---

## 3. The Full Lifecycle — Order Matters!

Here is the **official order** Angular follows, from the moment a component is created to the moment it dies:

```
┌─────────────────────────────────────────────────────────────────┐
│                     COMPONENT LIFECYCLE FLOW                     │
└─────────────────────────────────────────────────────────────────┘

   START
     │
     ▼
┌───────────────┐
│  constructor() │   ← plain JS/TS class setup (NOT a real hook)
└───────┬────────┘
        │
        ▼
┌────────────────┐
│  ngOnChanges()  │   ← runs FIRST TIME too (if component has @Input)
└───────┬─────────┘
        │
        ▼
┌────────────────┐
│   ngOnInit()    │   ← runs ONCE. Best place for setup / API calls
└───────┬─────────┘
        │
        ▼
┌─────────────────┐
│   ngDoCheck()    │   ← runs on EVERY change detection cycle
└────────┬─────────┘
         │
         ▼
┌──────────────────────┐
│  ngAfterViewInit()     │   ← runs ONCE, after the HTML view is ready
└──────────┬─────────────┘
           │
           ▼
   ┌───────────────────────────────┐
   │   COMPONENT IS ALIVE ON PAGE    │
   │   (user interacts, data changes)│
   └───────────────┬─────────────────┘
                    │
      Whenever @Input changes:
                    │
                    ▼
         ┌────────────────────┐
         │   ngOnChanges()      │  (runs again)
         └──────────┬───────────┘
                    │
      Whenever ANYTHING changes:
                    │
                    ▼
         ┌────────────────────┐
         │    ngDoCheck()       │  (runs again)
         └──────────┬───────────┘
                    │
        ... this loop continues while
          the component is on screen ...
                    │
                    ▼
      When component is about to be removed
      (e.g. user navigates to another page):
                    │
                    ▼
         ┌────────────────────┐
         │   ngOnDestroy()      │  ← runs ONCE. Clean-up time!
         └──────────┬───────────┘
                    │
                    ▼
                  END
```

---

## 4. Quick Reference Table

| Hook | Runs When? | How Many Times? | What You Do Here |
|---|---|---|---|
| `constructor()` | Component class is created | Once | Simple variable setup (not real Angular data yet) |
| `ngOnChanges()` | An `@Input` value changes | Every time input changes (including the first time) | React to new data from parent |
| `ngOnInit()` | Right after component is created & inputs are set | Once | Load data, call API, set starting values |
| `ngDoCheck()` | Every single change detection run | Very frequently | Custom manual checks (rarely used) |
| `ngAfterViewInit()` | Once the template/HTML is fully rendered | Once | Access DOM elements, work with child components |
| `ngOnDestroy()` | Just before component is removed | Once | Clean up: stop timers, unsubscribe, remove listeners |

**Most used in real projects:** `ngOnInit()` and `ngOnDestroy()`. These two alone solve 90% of use cases.

---

## 5. Deep Dive — `ngOnInit()`

### What it means
`ngOnInit` runs **once**, right after Angular has finished creating the component **and** has set its `@Input` values. This is your "component is ready, start doing real work now" signal.

### Real-life comparison
Imagine you just moved into a new house (component created). `ngOnInit` is like **unpacking your bags and setting up furniture** — the setup work you do right after arriving, before you start "living" there.

### Code Example
```typescript
import { Component, OnInit } from "@angular/core";

@Component({
  selector: "app-hello",
  template: `<h3>{{ message }}</h3>`,
})
export class HelloComponent implements OnInit {
  message: string = "";

  ngOnInit() {
    this.message = "Component is ready!";
    console.log("ngOnInit ran");
  }
}
```

**What happens:** When `<app-hello>` appears on the page, Angular calls `ngOnInit()` automatically, sets `message`, and the browser shows **"Component is ready!"**

### Why not just use the constructor?

This is the **most common confusion** for beginners. Here's the clear difference:

```
┌─────────────────────┐         ┌─────────────────────┐
│     constructor()     │         │      ngOnInit()       │
├─────────────────────┤         ├─────────────────────┤
│ Runs FIRST            │         │ Runs AFTER constructor │
│ Plain TypeScript class │         │ Angular-specific        │
│ @Input NOT ready yet   │         │ @Input IS ready          │
│ Use for: simple wiring,│         │ Use for: real setup,     │
│ dependency injection   │         │ API calls, data loading   │
└─────────────────────┘         └─────────────────────┘
```

**Rule of thumb:** Constructor = simple wiring (like injecting a service). `ngOnInit` = real setup work (like calling an API).

---

## 6. Deep Dive — `ngOnChanges()`

### What it means
`ngOnChanges` runs **every time** a parent component changes a value passed via `@Input`. It also runs **once at the start**, when the input first gets its value.

### Real-life comparison
Think of a **food delivery tracker widget** on your phone. Every time the restaurant updates the order status (parent sends new data), the widget **reacts and updates itself** — that reaction is `ngOnChanges`.

### Code Example
```typescript
import { Component, Input, OnChanges } from "@angular/core";

@Component({
  selector: "app-child",
  template: `<p>Name is: {{ name }}</p>`,
})
export class ChildComponent implements OnChanges {
  @Input() name: string = "";

  ngOnChanges() {
    console.log("Input changed, name is now:", this.name);
  }
}
```

### Visual: Parent → Child Communication

```
   PARENT COMPONENT                    CHILD COMPONENT
┌─────────────────────┐            ┌──────────────────────┐
│  name = "Unishka"     │  @Input   │   ngOnChanges()         │
│                        │ ────────► │   fires automatically   │
│  (changes name later)  │           │   whenever "name"        │
│  name = "Rawat"        │ ────────► │   value changes here    │
└─────────────────────┘            └──────────────────────┘
```

**Key point:** `ngOnChanges` only fires for `@Input` properties — not for internal variables that change on their own.

---

## 7. Deep Dive — `ngOnDestroy()`

### What it means
`ngOnDestroy` runs **once**, right before Angular removes the component from the page. This is your **last chance to clean up** anything that would otherwise keep running in the background.

### Real-life comparison
Imagine leaving a hotel room (component being destroyed). Before you leave, you **turn off the lights, switch off the AC, and check out** — that's cleanup. If you forget, the AC keeps running and wasting electricity even though nobody's there — that's a **memory leak**.

### Code Example
```typescript
import { Component, OnInit, OnDestroy } from "@angular/core";

@Component({
  selector: "app-timer",
  template: `<p>Seconds: {{ count }}</p>`,
})
export class TimerComponent implements OnInit, OnDestroy {
  count: number = 0;
  timerId: any;

  ngOnInit() {
    // start a timer when the component appears
    this.timerId = setInterval(() => this.count++, 1000);
  }

  ngOnDestroy() {
    // stop the timer before the component is removed
    clearInterval(this.timerId);
    console.log("Timer cleaned up");
  }
}
```

### Visual: Why Cleanup Matters

```
WITHOUT ngOnDestroy cleanup:
┌───────────────┐     component removed     ┌───────────────┐
│  Timer running   │  ─────────────────────►  │  Timer STILL     │
│  on screen        │      (user navigates)     │  running in       │
│                    │                            │  background! ❌  │
└───────────────┘                            └───────────────┘
                                              → MEMORY LEAK

WITH ngOnDestroy cleanup:
┌───────────────┐     component removed     ┌───────────────┐
│  Timer running   │  ─────────────────────►  │  Timer STOPPED    │
│  on screen        │   ngOnDestroy() called    │  cleanly ✅        │
│                    │   → clearInterval()        │                    │
└───────────────┘                            └───────────────┘
```

**Things you should ALWAYS clean up in `ngOnDestroy`:**
- `setInterval` / `setTimeout` timers
- RxJS subscriptions (`.subscribe()`)
- Event listeners added manually (e.g. `window.addEventListener`)
- WebSocket connections

---

## 8. Simple Way to Remember Everything

```
BORN     →  constructor()  →  ngOnChanges() (first time)  →  ngOnInit()
LIVING   →  ngOnChanges() runs again on every input change
VIEW READY →  ngAfterViewInit() (once, when HTML is fully rendered)
DYING    →  ngOnDestroy() (once, just before removal)
```

## 9. Common Mistakes Beginners Make

| Mistake | Why It's Wrong | Fix |
|---|---|---|
| Doing API calls inside `constructor()` | `@Input` and view aren't ready yet | Move API calls to `ngOnInit()` |
| Forgetting `ngOnDestroy()` for timers/subscriptions | Causes memory leaks, app slows down over time | Always clean up in `ngOnDestroy()` |
| Expecting `ngOnChanges()` to fire for non-`@Input` variables | It only tracks `@Input` properties | Use `ngDoCheck()` if you need to track other changes (rarely needed) |
| Confusing `ngOnInit()` with constructor | They run at different times with different data readiness | Constructor = wiring, `ngOnInit` = setup |

---

## 10. Summary — Remember This

- Lifecycle hooks = methods Angular calls **automatically** at set moments in a component's life.
- **`ngOnInit()`** → runs once at the start. Do your setup here (load data, set values, call APIs).
- **`ngOnChanges()`** → runs when an `@Input` changes. React to new data from parent.
- **`ngOnDestroy()`** → runs once at the end. Clean up here (timers, subscriptions, listeners).

> **Rule of thumb:** Set up in `ngOnInit`, clean up in `ngOnDestroy`. These two cover most real-world needs.

---
---

# Day-5  Frontend Frameworks
## Angular — Binding, Directives & Pipes (Deep Dive)
**Everything that happens inside the template.

---

The template is the HTML the user sees. Angular gives it superpowers: showing data, reacting to clicks, looping over lists, showing things conditionally, and formatting values. This note breaks each of those superpowers down properly — what it does, why it exists, and how data actually flows.

---

## 1. Data Binding: The Four Kinds

Binding is simply the **connection** between your class (the TypeScript data) and your template (the HTML view). The direction of that connection is what changes, and the brackets tell you which direction.

```
   CLASS (TypeScript)                    TEMPLATE (HTML)
   ┌───────────────┐                    ┌───────────────┐
   │  name = "X"    │                    │  <h1>{{name}}  │
   │  imageUrl = ".."│  ───── data ────► │  <img [src]=..│
   │  isBusy = true │                    │  <button [dis..│
   └───────────────┘                    └───────────────┘
                                                 │
   ┌───────────────┐                            │
   │  save() {...}  │  ◄──── event ──────────────┘
   └───────────────┘         <button (click)=..>
```

### 1.1 Interpolation — `{{ }}`

This is the simplest binding. It takes a value from the class and **prints it as text** inside the HTML. It is **one-way** and **read-only** — class to view, nothing goes back.

```html
<h1>Hello {{ name }}</h1>
```
```ts
// class
name = "Angular";
```
Output on page: `Hello Angular`

Think of `{{ }}` as a **placeholder** — wherever it sits in the HTML, Angular quietly replaces it with the class value, and keeps it updated automatically whenever that value changes.

---

### 1.2 Property Binding — `[ ]`

Interpolation only writes **text**. But what if you want to set an actual **property** of an HTML element — like whether a button is disabled, or which image an `<img>` tag points to? That's what square brackets do.

```html
<img [src]="imageUrl" />
<button [disabled]="isBusy">Save</button>
```

Here, `[src]` is not text on the page — it is literally setting the `src` property of the `<img>` element to whatever `imageUrl` holds in the class. Same with `[disabled]` — if `isBusy` is `true`, the button becomes disabled; if `false`, it becomes clickable again.

**Key difference from `{{ }}`:**

| | `{{ }}` Interpolation | `[ ]` Property Binding |
|---|---|---|
| Used for | Displaying text between tags | Setting a property/attribute on a tag |
| Example | `<h1>{{ name }}</h1>` | `<img [src]="imageUrl" />` |
| Data type | Always becomes a string | Can be any type (string, boolean, number, object) |

---

### 1.3 Event Binding — `( )`

So far both directions moved data **into** the template. Event binding flips it — it lets the **view talk back to the class**. When something happens on the page (a click, a keypress, a form submit), round brackets catch that event and call a method in your class.

```html
<button (click)="save()">Save</button>
```
```ts
// class
save() {
  console.log("saved!");
}
```

Every time the user clicks the button, Angular runs `save()`. This is **view to class** — the opposite direction of `{{ }}` and `[ ]`.

```
   [ ]  Property Binding    class ──────► view    (data goes IN)
   ( )  Event Binding        view ──────► class    (event goes OUT)
```

---

### 1.4 Two-Way Binding — `[( )]`

What if you need **both directions at once**? Type something in a box, and the class property should update immediately — *and* if the class property changes some other way, the box should reflect that too. That's two-way binding, nicknamed **"banana in a box"** because of how `[()]` looks.

```html
<input [(ngModel)]="username" />
<p>You typed: {{ username }}</p>
```

```
        ┌─────────────────────┐
        │   <input>  (view)     │
        └──────────┬───────────┘
             ▲              │
      class updates    user types
      box shows it      box updates class
             │              ▼
        ┌─────────────────────┐
        │  username  (class)    │
        └─────────────────────┘
```

**Important setup note:** Two-way binding with `ngModel` requires `FormsModule`.
- In an **older NgModule-based project** → add `FormsModule` to that module's `imports` array.
- In a **standalone component** → add `FormsModule` directly to the component's own `imports` array.

Without this import, `[(ngModel)]` will throw an error, because Angular doesn't know what `ngModel` means without `FormsModule` providing it.

---

### 1.5 The Four Bindings, Side by Side

```
┌──────────────┬─────────────────┬────────────────────────────┐
│   Syntax       │   Direction       │   What it does               │
├──────────────┼─────────────────┼────────────────────────────┤
│  {{ value }}   │  class → view     │  Shows a value as text        │
│  [ property ]  │  class → view     │  Sets an element's property   │
│  ( event )     │  view → class     │  Runs a method on an event     │
│  [( ngModel )] │  class ⇄ view     │  Keeps both in sync, always    │
└──────────────┴─────────────────┴────────────────────────────┘
```

**One-line memory trick:** Square brackets = data going **in**. Round brackets = event coming **out**. Both together = **two-way**.

---

## 2. Directives: `*ngIf`, `*ngFor`, `ngSwitch`

A **directive** is a special instruction you place on an HTML element to change how that element behaves — whether it shows up, how many times it repeats, or which version of it appears. The three structural directives you'll use constantly all start reshaping the actual DOM structure (not just styling it).

```
                     TEMPLATE ELEMENT
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        *ngIf           *ngFor         ngSwitch
     (show/hide)     (repeat for      (pick ONE
                       each item)      of many)
```

---

### 2.1 `*ngIf` — Show or Hide

`*ngIf` decides whether an element exists on the page **at all**, based on a condition. If the condition is `false`, Angular doesn't just hide it with CSS — it **removes the element completely** from the DOM.

```html
<p *ngIf="isLoggedIn">Welcome back!</p>
<p *ngIf="!isLoggedIn">Please log in.</p>
```

```
   isLoggedIn = true                 isLoggedIn = false
   ┌─────────────────┐              ┌─────────────────┐
   │ <p>Welcome back!</p>│              │  (nothing here)   │
   │ (removed: 2nd <p>)  │              │ <p>Please log in.│
   └─────────────────┘              └─────────────────┘
```

This matters because a hidden-with-CSS element still exists in memory and in the DOM tree, while an `*ngIf`-removed element is **completely gone** until the condition becomes true again — which is more efficient when the content is heavy or shouldn't even be reachable.

---

### 2.2 `*ngFor` — Loop Over a List

`*ngFor` repeats one element **once for every item** in an array. It's how you turn a list of data into a list of visible elements, without manually writing each one.

```html
<ul>
  <li *ngFor="let fruit of fruits">{{ fruit }}</li>
</ul>
```
```ts
// class
fruits = ["Apple", "Mango", "Banana"];
```

```
   fruits = ["Apple", "Mango", "Banana"]
                    │
                    ▼   *ngFor repeats the <li> once per item
   ┌───────────────────────────────┐
   │ <ul>                            │
   │   <li>Apple</li>                │
   │   <li>Mango</li>                │
   │   <li>Banana</li>               │
   │ </ul>                          │
   └───────────────────────────────┘
```

Three items in the array → three `<li>` elements on the page. If the array changes (an item added or removed), Angular automatically updates the list to match — you never manually add or remove `<li>` tags yourself.

---

### 2.3 `ngSwitch` — Pick One of Many

`ngSwitch` is like a `switch` statement, but for your template. Instead of showing/hiding one thing (`*ngIf`) or repeating something (`*ngFor`), it picks exactly **one block** to display out of several possible options, based on a matching value.

```html
<div [ngSwitch]="role">
  <p *ngSwitchCase="'admin'">You are an admin</p>
  <p *ngSwitchCase="'user'">You are a user</p>
  <p *ngSwitchDefault>Unknown role</p>
</div>
```

```
                     role = "admin"
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        case 'admin'   case 'user'    default
         ✅ MATCH         skip           skip
              │
              ▼
     Only shows: "You are an admin"
```

If `role` matches `"admin"`, only that line renders — the others are skipped entirely. If `role` doesn't match any case, `*ngSwitchDefault` acts as the fallback, similar to the `default` case in a normal JavaScript switch statement.

---

### 2.4 Directives, Side by Side

```
┌────────────┬──────────────────────────────────────────┐
│  Directive   │  What it decides                            │
├────────────┼──────────────────────────────────────────┤
│  *ngIf       │  Should this element exist at all? (yes/no)   │
│  *ngFor      │  How many copies of this element are needed?  │
│  ngSwitch    │  Which ONE of several elements should show?   │
└────────────┴──────────────────────────────────────────┘
```

---

## 3. Pipes: Formatting a Value for Display

A **pipe** transforms how a value **looks on screen**, without ever touching or changing the actual data stored in the class. You apply a pipe using the `|` symbol, right inside interpolation.

```
   RAW DATA (class)              PIPE (formatting)              DISPLAYED (view)
   ┌───────────────┐            ┌──────────────┐            ┌───────────────┐
   │  name = "angular"│  ─────►   │   | uppercase   │  ─────►   │    ANGULAR      │
   └───────────────┘            └──────────────┘            └───────────────┘

   The original "name" value in the class is still "angular" — only the DISPLAY changed.
```

```html
<p>{{ name | uppercase }}</p>            <!-- ANGULAR -->
<p>{{ price | currency:'INR' }}</p>      <!-- Rs 500.00 -->
<p>{{ today | date:'longDate' }}</p>     <!-- August 5, 2026 -->
```

**Commonly used built-in pipes:**

| Pipe | Purpose |
|---|---|
| `uppercase` | Converts text to ALL CAPS |
| `lowercase` | Converts text to all lowercase |
| `titlecase` | Capitalizes The First Letter Of Each Word |
| `date` | Formats a date value |
| `currency` | Formats a number as currency (e.g. `₹500.00`) |
| `number` | Formats a number (decimals, separators) |
| `percent` | Formats a number as a percentage |
| `json` | Converts an object to a readable JSON string (great for debugging) |
| `slice` | Cuts a portion of a string or array |

### 3.1 Chaining Pipes

Pipes can be **chained** — the output of one pipe becomes the input of the next, read left to right.

```html
{{ name | slice:0:5 | uppercase }}
```

```
   name = "angular development"
              │
              ▼   slice:0:5  (takes first 5 characters)
          "angul"
              │
              ▼   uppercase
          "ANGUL"
```

---

## 4. Custom Pipes: Building Your Own

When none of the built-in pipes do what you need, you can write your **own** pipe. A pipe is simply a class marked with the `@Pipe` decorator, containing one required method: `transform`.

```
   TEMPLATE            PIPE CLASS                    RESULT
   ┌──────────┐       ┌───────────────────┐       ┌──────────┐
   │ {{ 10 | double }}│ ──►│ transform(value) {   │ ──►  │    20      │
   └──────────┘       │   return value * 2;   │       └──────────┘
                       │ }                     │
                       └───────────────────┘
```

```ts
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({ name: "double" })
export class DoublePipe implements PipeTransform {
  transform(value: number): number {
    return value * 2;
  }
}
```

Using it in a template:
```html
<p>{{ 10 | double }}</p> <!-- shows 20 -->
```

The `transform` method receives the value sitting on the **left** side of the `|`, does whatever calculation or formatting you write, and returns the changed result — which is what actually appears on the page. You can also generate a pipe file automatically using the Angular CLI: `ng generate pipe double`.

### 4.1 Pipes That Take Arguments

A pipe can also accept extra arguments, written after a colon `:` — just like the built-in `currency:'INR'` or `date:'longDate'` you saw earlier.

```ts
@Pipe({ name: "multiply" })
export class MultiplyPipe implements PipeTransform {
  transform(value: number, times: number): number {
    return value * times;
  }
}
```

```html
<p>{{ 10 | multiply:3 }}</p> <!-- shows 30 -->
```

```
   10 | multiply:3
        │      │
        │      └── second argument (times = 3)
        └───────── value going into transform() (value = 10)

   transform(10, 3)  →  10 * 3  →  30
```

The first value (before `|`) always maps to the pipe's main `value` parameter. Anything after the colon maps to the additional parameters of `transform`, in order.

---

## 5. How It All Fits Together

```
                         ANGULAR TEMPLATE
        ┌──────────────────────────────────────────────┐
        │                                                    │
        │   BINDING           connects class ⇄ view           │
        │   {{ }} [ ] ( ) [( )]                                │
        │                                                    │
        │   DIRECTIVES        reshapes WHAT is on the page      │
        │   *ngIf *ngFor ngSwitch                              │
        │                                                    │
        │   PIPES             changes HOW data LOOKS            │
        │   | uppercase | date | custom pipes                  │
        │                                                    │
        └──────────────────────────────────────────────┘
```

Binding moves data between the class and the template. Directives decide **which elements exist** and **how many** of them appear. Pipes decide **how a value is displayed**, without ever changing the underlying data. Together, these three tools are what make an Angular template dynamic instead of static HTML.
---
---
# Angular Day 6 — Services, Dependency Injection, Singletons & Pipes

---

# 1. Angular Services

## What is an Angular Service?

An **Angular Service** is a normal TypeScript class used to store **shared logic or shared data** that multiple components may need.

For example:

- Fetching data from an API
- Storing logged-in user information
- Storing a company name
- Sharing data between components
- Keeping reusable logic in one place

### Simple Definition

> **Components are mainly used for the view/UI, while Services are used for shared logic and data.**

Instead of writing the same logic again and again inside different components, we put that logic inside a service.

### Without a Service

```text
                 Application
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
       Header       Footer      Profile
          |           |           |
          v           v           v
       Same        Same        Same
       Logic       Logic       Logic

Problem:
Same logic/data is repeated in multiple components.
```

### With a Service

```text
                    LogoService
                        |
              +---------+---------+
              |         |         |
              v         v         v
           Header     Footer    Profile
              |         |         |
              +---------+---------+
                        |
                   Shared Data
```

Now the shared logic exists in one place.

---

# 2. Creating an Angular Service

Angular CLI can create a service.

### Full Command

```bash
ng generate service logo
```

### Short Command

```bash
ng g s logo
```

Angular creates a file such as:

```text
logo.service.ts
```

---

## Basic Service Example

```typescript
import { Injectable } from "@angular/core";

@Injectable({ providedIn: "root" })
export class LogoService {

  companyName = "Resume Loop";

  getCompanyName() {
    return this.companyName;
  }

  setCompanyName(name: string) {
    this.companyName = name;
  }

}
```

---

# 3. Understanding the Service Code

## `@Injectable`

```typescript
@Injectable(...)
```

`@Injectable` tells Angular that this class can participate in Angular's **Dependency Injection system**.

```text
@Injectable
     |
     v
Angular knows this class
can participate in DI
     |
     v
Components can request it
```

---

## `providedIn: "root"`

```typescript
@Injectable({
  providedIn: "root"
})
```

`providedIn: "root"` makes the service available throughout the application.

It also gives the service the important singleton behavior discussed later.

```text
                 Angular Application
                         |
                         v
                    LogoService
                         |
                  providedIn: root
                         |
                         v
              Available throughout app
```

---

# 4. Understanding the Service Class

Our service contains:

```typescript
export class LogoService {

  companyName = "Resume Loop";

  getCompanyName() {
    return this.companyName;
  }

  setCompanyName(name: string) {
    this.companyName = name;
  }

}
```

It can be understood as:

```text
                    LogoService
                        |
          +-------------+-------------+
          |             |             |
          v             v             v
    companyName   getCompanyName()  setCompanyName()
          |             |             |
          |             |             |
       Stores       Reads data      Changes data
        data
```

### `companyName`

```typescript
companyName = "Resume Loop";
```

This stores the company name.

### `getCompanyName()`

```typescript
getCompanyName() {
  return this.companyName;
}
```

This method returns the current company name.

### `setCompanyName()`

```typescript
setCompanyName(name: string) {
  this.companyName = name;
}
```

This method changes the company name.

---

# 5. Why Do We Need Services?

Suppose multiple components need the same data.

Without a service:

```text
Header Component
      |
      +---- companyName

Footer Component
      |
      +---- companyName

Profile Component
      |
      +---- companyName
```

Each component has its own copy of the logic/data.

This causes:

- Repeated code
- More maintenance
- Difficult updates
- Less reusable code

With a service:

```text
                    LogoService
                        |
                Shared companyName
                        |
          +-------------+-------------+
          |             |             |
          v             v             v
       Header        Footer        Profile
```

Now the shared information is maintained in one place.

---

# 6. Dependency Injection

## What is Dependency Injection?

**Dependency Injection (DI)** is the mechanism through which Angular provides a required service to a component or class.

A component does not need to manually create the service.

Instead, it says:

> "I need this service."

Angular provides it.

```text
Component
    |
    | "I need LogoService"
    v
Angular Dependency Injection
    |
    | provides service
    v
Component
```

---

# 7. What is a Dependency?

A **dependency** is something that a class needs to perform its work.

For example:

```text
HeaderComponent
       |
       | needs
       v
LogoService
```

Here:

- `HeaderComponent` is the class that needs something.
- `LogoService` is its dependency.
- Angular provides that dependency.

---

# 8. Without Dependency Injection

Normally, we can manually create an object:

```typescript
const service = new LogoService();
```

Here the developer is directly responsible for creating the service.

```text
Component
    |
    | creates manually
    v
new LogoService()
    |
    v
Service Object
```

But Angular provides a system for managing these dependencies.

---

# 9. With Dependency Injection

Instead of:

```typescript
const service = new LogoService();
```

we write:

```typescript
constructor(public logoService: LogoService) {}
```

Angular sees that the component requires `LogoService`.

Then Angular provides it.

```text
             HeaderComponent
                    |
                    |
             constructor()
                    |
                    v
            "I need LogoService"
                    |
                    v
            Angular DI System
                    |
                    v
              LogoService
```

### Important Rule

> **When using Angular Dependency Injection, you normally do not write `new LogoService()` yourself.**

Angular handles the creation/provision of the dependency.

---

# 10. Injecting a Service into a Component

Example:

```typescript
import { Component } from "@angular/core";
import { LogoService } from "./logo.service";

@Component({
  selector: "app-header",

  template: `
    <h1>{{ logoService.getCompanyName() }}</h1>

    <button
      (click)="logoService.setCompanyName('Snapied')">
      Change
    </button>
  `,
})
export class HeaderComponent {

  constructor(public logoService: LogoService) {}

}
```

The important line is:

```typescript
constructor(public logoService: LogoService) {}
```

This means:

```text
HeaderComponent
       |
       | needs
       v
LogoService
```

Angular provides the `LogoService`.

---

# 11. Dependency Injection Flow

```text
+--------------------------------+
| Angular creates the component  |
+---------------+----------------+
                |
                v
+--------------------------------+
| Angular checks the constructor |
|                                |
| LogoService is required        |
+---------------+----------------+
                |
                v
+--------------------------------+
| Angular DI system looks for    |
| the required service           |
+---------------+----------------+
                |
                v
+--------------------------------+
| Angular creates or reuses      |
| the service instance           |
+---------------+----------------+
                |
                v
+--------------------------------+
| Angular provides the service   |
| to the component               |
+---------------+----------------+
                |
                v
+--------------------------------+
| Component uses the service     |
+--------------------------------+
```

---

# 12. Real-Life Example of Dependency Injection

Think about electricity.

You do not build an electricity generator every time you want to use electricity.

You simply plug your device into a socket.

```text
          You
           |
           | plug in
           v
    Electricity System
           |
           | provides electricity
           v
        Your Device
```

Angular DI works similarly:

```text
       Component
           |
           | asks for service
           v
      Angular DI
           |
           | provides service
           v
       Component
```

The component **asks**, and Angular **provides**.

---

# 13. Singleton

## What is a Singleton?

When a service is provided using:

```typescript
providedIn: "root"
```

Angular creates one shared instance of that service for the application.

That one shared instance is called a **Singleton**.

### Main Idea

```text
                  LogoService
                      |
                      v
               ONE INSTANCE
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
       Header       Footer      Profile
```

All these components can use the same service instance.

---

# 14. Why is Singleton Important?

The main advantage is **shared state/data**.

Because multiple components use the same service instance:

```text
                SAME SERVICE
                     |
        +------------+------------+
        |            |            |
        v            v            v
      Header       Footer       Profile
        |            |            |
        +------------+------------+
                     |
                     v
                Shared Data
```

If one component changes a value in the service, another component using the same service can access the changed value.

---

# 15. Singleton Example 1 — TV Remote

Imagine a family has **one TV remote**.

```text
                  ONE TV REMOTE
                        |
             +----------+----------+
             |          |          |
             v          v          v
           Papa       Sister     Brother
```

Papa changes the channel to cricket.

Everyone sees cricket.

Then the sister takes the same remote and changes the channel to cartoons.

Everyone sees cartoons.

There is not a separate remote for every person.

### Angular Connection

```text
One TV Remote
      |
      v
One Singleton Service

Family Members
      |
      v
Angular Components
```

The TV remote represents the shared service instance.

---

# 16. Singleton Example 2 — Washing Machine

Imagine a small family has one washing machine.

```text
             ONE WASHING MACHINE
                     |
          +----------+----------+
          |          |          |
          v          v          v
       Mother       Son       Father
```

Mother starts a washing cycle.

Later, the son uses the same machine in whatever state it was left.

There are not separate machines automatically created for each person.

### Angular Connection

```text
One Washing Machine
        |
        v
One Service Instance

Different People
        |
        v
Different Components
```

Everyone uses the same shared thing.

---

# 17. Singleton Example 3 — Shopping Cart

Imagine you walk through a mall with one shopping cart.

You add:

```text
Shirt
  |
  v
Shoes
  |
  v
Toy
```

Everything remains inside the same cart.

```text
Shop 1 ----> Shirt ----+
                       |
Shop 2 ----> Shoes ----+----> ONE CART ----> Billing
                       |
Shop 3 ----> Toy ------+
```

The same idea applies to a singleton service.

Different components can add or read information from the same service.

---

# 18. What Happens Without a Singleton?

Suppose every component had a separate service instance.

```text
Header
  |
  +----> Service Copy A

Footer
  |
  +----> Service Copy B

Profile
  |
  +----> Service Copy C
```

If Header changes its service:

```text
Header
   |
   v
Service Copy A
   |
   v
companyName = "Snapied"
```

Footer still has:

```text
Service Copy B
   |
   v
companyName = "Resume Loop"
```

So Footer would not automatically see Header's change.

With a singleton:

```text
Header ----+
           |
Footer ----+----> SAME SERVICE INSTANCE
           |
Profile ---+
```

Everyone works with the same shared service.

---

# 19. Sharing Data Through a Singleton

One of the main benefits of a service is sharing data between components.

The components do not have to be parent and child.

For example:

```text
Header Component
       |
       | changes company name
       v
+------------------+
|   LogoService    |
|                  |
| companyName      |
+--------+---------+
         |
         | same instance
         v
Footer Component
       |
       | reads company name
       v
   "Snapied"
```

### Header changes the value

```typescript
this.logoService.setCompanyName("Snapied");
```

### Footer reads the value

```html
<p>{{ logoService.getCompanyName() }}</p>
```

The Footer can show:

```text
Snapied
```

because both components are using the same service instance.

---

# 20. Important Mistake When Sharing Data

Suppose a component copies the service value only once inside `ngOnInit()`:

```typescript
this.companyName = this.logoService.getCompanyName();
```

At that moment:

```text
LogoService
     |
     v
"Resume Loop"
     |
     | copied once
     v
Component.companyName
     |
     v
"Resume Loop"
```

Later, the service changes:

```text
LogoService
     |
     v
"Snapied"
```

But the component's copied property may still contain:

```text
"Resume Loop"
```

because it took the value only once.

### Better Approach

Read the service value directly in the template:

```html
{{ logoService.getCompanyName() }}
```

Conceptually:

```text
             LogoService
                  |
                  | current value
                  v
               Template
                  |
                  v
            Latest Display
```

Think of it like a whiteboard.

If you take a photograph of the whiteboard once, you only have the old information.

If you keep looking at the actual whiteboard, you can see the latest information.

---

# 21. Why Angular 13 Instead of Angular 22?

A common question is:

> "If newer Angular versions exist, why are we learning Angular 13?"

The lesson gives several reasons.

---

## Reason 1 — Core Ideas Are the Same

Important Angular concepts include:

- Components
- Services
- Dependency Injection
- Pipes
- Modules

The fundamental concepts remain transferable across Angular versions.

```text
Angular 13
    |
    +---- Components
    |
    +---- Services
    |
    +---- Dependency Injection
    |
    +---- Pipes
    |
    +---- Modules
              |
              v
       Strong Fundamentals
              |
              v
       Newer Angular Versions
```

What you learn about the core concepts can be carried into newer versions.

---

## Reason 2 — Real Applications Can Use Older Versions

Companies do not necessarily upgrade every application every year.

Therefore, developers can encounter older Angular applications in real projects.

```text
        New Angular Versions
                 |
                 | coexist with
                 v
       Older Production Apps
                 |
                 v
      Developers may need
      older-version knowledge
```

Therefore, learning an older version is not automatically useless.

---

## Reason 3 — Angular 13 Is Stable and Well Documented

Angular 13 has many existing:

- Tutorials
- Examples
- Answers
- Learning resources

This makes it easier to find information when learning.

---

## Reason 4 — Fewer Moving Parts for Beginners

Newer Angular versions introduce additional features and concepts.

The lesson specifically mentions:

- Standalone components
- Signals

These features are useful, but they can add complexity when someone is still learning the basic Angular concepts.

A simple learning path is:

```text
Learn Fundamentals
        |
        v
Understand Angular Concepts
        |
        v
Learn New Features
        |
        v
Move to Newer Angular
```

### Main Takeaway

> Learn the strong fundamentals first. Once the basics are clear, moving to newer Angular versions becomes easier.

---

# 22. Pipes

## What is a Pipe?

A **Pipe** changes how a value looks when it is displayed in an Angular template.

It changes the **display format** without changing the actual original data.

Pipes use the pipe symbol:

```text
|
```

### Basic Syntax

```html
{{ value | pipeName }}
```

### Basic Flow

```text
Original Value
      |
      v
    PIPE
      |
      v
Formatted Display Value
```

---

# 23. Built-in Pipes

Angular provides several built-in pipes.

Common examples:

| Pipe | Purpose |
|------|---------|
| `uppercase` | Converts text to uppercase |
| `lowercase` | Converts text to lowercase |
| `titlecase` | Formats text as title case |
| `date` | Formats a date |
| `currency` | Formats currency |
| `number` | Formats a number |
| `percent` | Formats a percentage |
| `json` | Displays data as JSON |
| `slice` | Takes a part of a string/array |

---

# 24. uppercase Pipe

Example:

```html
<p>{{ name | uppercase }}</p>
```

Suppose:

```text
name = "Resume Loop"
```

The displayed result becomes:

```text
RESUME LOOP
```

### Flow

```text
"Resume Loop"
      |
      | uppercase
      v
"RESUME LOOP"
```

---

# 25. lowercase Pipe

Example:

```html
<p>{{ name | lowercase }}</p>
```

Flow:

```text
"Resume Loop"
      |
      | lowercase
      v
"resume loop"
```

---

# 26. titlecase Pipe

The `titlecase` pipe formats text into title case.

Example:

```html
<p>{{ name | titlecase }}</p>
```

It is useful when text needs to be displayed in a title-like format.

---

# 27. currency Pipe

Example:

```html
<p>{{ price | currency:'INR' }}</p>
```

If:

```text
price = 500
```

The value can be displayed in Indian currency formatting:

```text
₹500.00
```

The important part is:

```text
currency:'INR'
```

Here `INR` is an argument given to the currency pipe.

### Flow

```text
500
 |
 | currency
 | argument = INR
 v
₹500.00
```

---

# 28. date Pipe

Example:

```html
<p>{{ today | date:'longDate' }}</p>
```

The pipe formats the date for display.

For example:

```text
August 7, 2026
```

The exact output depends on the actual date value.

### Flow

```text
Date Value
    |
    | date:'longDate'
    v
Long Date Format
```

---

# 29. Pipe Arguments

A pipe can receive an argument after a colon.

### General Syntax

```html
{{ value | pipeName:argument }}
```

Example:

```html
{{ price | currency:'INR' }}
```

Flow:

```text
price
  |
  v
currency pipe
  |
  | argument = INR
  v
Formatted Currency
```

---

# 30. Chaining Pipes

Angular allows multiple pipes to be used together.

Example:

```html
{{ name | slice:0:5 | uppercase }}
```

The output of the first pipe becomes the input of the next pipe.

### Flow

```text
Original Value
      |
      v
slice:0:5
      |
      v
First 5 Characters
      |
      v
uppercase
      |
      v
Final Result
```

### General Pipe Chain

```text
Value
  |
  v
Pipe 1
  |
  v
Pipe 2
  |
  v
Pipe 3
  |
  v
Final Display
```

Pipes are processed from left to right.

---

# 31. Custom Pipes

Sometimes the built-in Angular pipes do not do exactly what you need.

In that case, you can create your own **Custom Pipe**.

A custom pipe is a class that uses:

```typescript
@Pipe
```

and implements:

```typescript
PipeTransform
```

The main method is:

```typescript
transform()
```

---

# 32. Creating a Custom Pipe

Angular CLI can create a custom pipe:

```bash
ng generate pipe double
```

Short form:

```bash
ng g pipe double
```

Example custom pipe:

```typescript
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({ name: "double" })
export class DoublePipe implements PipeTransform {

  transform(value: number): number {
    return value * 2;
  }

}
```

---

# 33. Understanding `@Pipe`

This code:

```typescript
@Pipe({ name: "double" })
```

tells Angular that this class is a pipe.

The pipe will be used in the template with the name:

```text
double
```

Therefore:

```html
{{ 10 | double }}
```

means:

```text
Use the "double" pipe on 10.
```

---

# 34. Understanding `PipeTransform`

The class uses:

```typescript
implements PipeTransform
```

This means the pipe follows Angular's pipe transformation structure.

The main method is:

```typescript
transform()
```

---

# 35. Understanding `transform()`

Example:

```typescript
transform(value: number): number {
  return value * 2;
}
```

The `transform()` method:

1. Receives the input value.
2. Performs some operation.
3. Returns the transformed value.

### Flow

```text
Input
  |
  v
transform()
  |
  | Perform operation
  v
Output
```

For the `double` pipe:

```text
10
 |
 v
transform(10)
 |
 | 10 × 2
 v
20
```

---

# 36. Using a Custom Pipe

After creating the pipe:

```html
<p>{{ 10 | double }}</p>
```

The result is:

```text
20
```

### Complete Flow

```text
Template
   |
   | 10 | double
   v
DoublePipe
   |
   v
transform(10)
   |
   | 10 × 2
   v
20
   |
   v
Displayed in Template
```

---

# 37. Custom Pipe with an Argument

A custom pipe can also accept arguments.

Example:

```typescript
@Pipe({ name: "multiply" })
export class MultiplyPipe implements PipeTransform {

  transform(value: number, times: number): number {
    return value * times;
  }

}
```

Here:

```typescript
value
```

is the original value.

And:

```typescript
times
```

is the argument supplied to the pipe.

### Using It

```html
<p>{{ 10 | multiply:3 }}</p>
```

### Flow

```text
10
 |
 | multiply
 | argument = 3
 v
transform(10, 3)
 |
 | 10 × 3
 v
30
```

Result:

```text
30
```

---

# 38. Angular 13 Module Declaration for Custom Pipes

In Angular 13, a custom pipe needs to be included in the appropriate module's `declarations`.

Conceptually:

```text
Custom Pipe
     |
     v
Angular Module
     |
     v
declarations
     |
     v
Pipe can be used by
templates in that module
```

Example:

```typescript
@NgModule({
  declarations: [
    DoublePipe
  ]
})
export class AppModule {}
```

---

# 39. Built-in Pipe vs Custom Pipe

| Built-in Pipe | Custom Pipe |
|---|---|
| Already provided by Angular | Created by the developer |
| Ready to use | Must be written |
| Examples: `uppercase`, `date`, `currency` | Examples: `double`, `multiply` |
| Used for common formatting | Used for application-specific transformation |

### Decision Flow

```text
Need to format/transform a value
              |
              v
     Does Angular already
     provide this pipe?
          /        \
        YES         NO
         |           |
         v           v
   Built-in Pipe  Custom Pipe
```

---

# 40. Service vs Pipe

Services and pipes have completely different purposes.

| Service | Pipe |
|---|---|
| Stores shared logic/data | Formats/transforms displayed values |
| Used by components/classes | Mainly used inside templates |
| Can store shared application data | Mainly performs transformation |
| Uses Dependency Injection | Uses `|` syntax |
| Example: `LogoService` | Example: `uppercase`, `DoublePipe` |

### Easy Way to Remember

```text
SERVICE
   |
   v
Shared Logic + Shared Data
```

```text
PIPE
   |
   v
Display Formatting + Transformation
```

---

# 41. Complete Angular Day 3 Concept Map

```text
                         ANGULAR
                            |
             +--------------+--------------+
             |                             |
             v                             v
         SERVICES                         PIPES
             |                             |
             v                             v
     Shared Logic/Data              Format/Transform
             |                             |
             v                             v
       @Injectable                   Built-in Pipes
             |                             |
             v                  +----------+----------+
    Dependency Injection        |          |          |
             |              uppercase    date     currency
             v
    providedIn: "root"
             |
             v
         Singleton
             |
             v
     One Shared Instance
             |
      +------+------+
      |      |      |
      v      v      v
   Header  Footer Profile

                                  Custom Pipes
                                       |
                                       v
                                     @Pipe
                                       |
                                       v
                                  transform()
```

---

# 42. Complete Service + DI + Singleton Flow

```text
                 Angular Application
                         |
                         v
                    LogoService
                         |
                         v
                    @Injectable
                         |
                         v
                 providedIn: "root"
                         |
                         v
                Singleton Instance
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
          Header       Footer      Profile
             |           |           |
             +-----------+-----------+
                         |
                         v
                    Shared Data
                    companyName
                         |
              +----------+----------+
              |                     |
              v                     v
      setCompanyName()       getCompanyName()
              |                     |
              v                     v
       Change shared data     Read shared data
```

---

# 43. Complete Pipe Processing Flow

```text
                 Template Value
                       |
                       v
                  Pipe Symbol |
                       |
                       v
              Built-in / Custom Pipe
                       |
                       v
                 Transformation
                       |
                       v
                Displayed Result
```

Example:

```text
"Resume Loop"
      |
      v
uppercase
      |
      v
"RESUME LOOP"
```

Another example:

```text
10
 |
 v
multiply:3
 |
 v
30
```

---

# 44. Complete Angular Day 3 Flow

```text
                         ANGULAR
                            |
             +--------------+--------------+
             |                             |
             v                             v
         COMPONENTS                       PIPES
             |                             |
             | need shared                 |
             | work/data                  |
             v                             |
          SERVICES                         |
             |                             |
             v                             |
        @Injectable                        |
             |                             |
             v                             |
    Dependency Injection                   |
             |                             |
             v                             |
    providedIn: "root"                     |
             |                             |
             v                             |
         Singleton                         |
             |                             |
             v                             |
     One Shared Instance                   |
             |                             |
       +-----+-----+                       |
       |     |     |                       |
       v     v     v                       v
    Header Footer Profile          Built-in / Custom
       |     |     |                     |
       +-----+-----+                     |
             |                            |
             v                            v
        Shared Data                 transform()
                                          |
                                          v
                                   Displayed Result
```

---

# 45. Service Creation Flow

```text
Developer
    |
    | ng g s logo
    v
Angular CLI
    |
    v
logo.service.ts
    |
    v
@Injectable
    |
    v
providedIn: "root"
    |
    v
Service available
throughout application
```

---

# 46. Component + Service Flow

```text
                Component
                    |
                    | needs shared work/data
                    v
                 Service
                    |
                    | provided through
                    v
           Dependency Injection
                    |
                    v
              Angular provides
              service instance
                    |
                    v
                Component
                    |
                    v
              Uses the service
```

---

# 47. Shared Data Flow

```text
                  LogoService
                      |
                  companyName
                      |
          +-----------+-----------+
          |                       |
          v                       v
      Header                   Footer
          |                       |
          |                       |
   setCompanyName()        getCompanyName()
          |                       |
          v                       v
      "Snapied"              "Snapied"
```

Both components are reading/writing the same service data.

---

# 48. Pipe Transformation Flow

```text
             Original Data
                  |
                  v
            Angular Template
                  |
                  v
             Pipe Operator |
                  |
                  v
          Pipe Transformation
                  |
                  v
            Displayed Value
```

Example:

```text
"resume loop"
      |
      v
uppercase
      |
      v
"RESUME LOOP"
```

---

# 49. Multiple Pipes Flow

```text
        Original Value
              |
              v
          Pipe 1
              |
              v
          Pipe 2
              |
              v
          Pipe 3
              |
              v
       Final Display
```

Example:

```html
{{ name | slice:0:5 | uppercase }}
```

Flow:

```text
Name
 |
 v
slice:0:5
 |
 v
First 5 Characters
 |
 v
uppercase
 |
 v
Final uppercase result
```

---

# 50. One-Line Memory Rules

```text
Service
→ A class used for shared logic and shared data.

@Injectable
→ Marks a class as injectable for Angular's DI system.

Dependency Injection
→ Angular provides the required dependency to a component/class.

providedIn: "root"
→ Makes the service available across the application and supports singleton behavior.

Singleton
→ One shared service instance.

Shared Data
→ Multiple components can use the same service instance to access shared data.

Pipe
→ Formats or transforms a value for display.

Built-in Pipe
→ A pipe already provided by Angular.

Custom Pipe
→ A pipe created by the developer.

@Pipe
→ Decorator used to define a custom pipe.

PipeTransform
→ Interface used by a pipe class.

transform()
→ Method that receives the value and returns the transformed value.

Pipe Argument
→ Extra value passed after ":".

Pipe Chaining
→ Applying multiple pipes one after another.

|
→ Pipe operator used in Angular templates.
```

---

# 51. Final Quick Revision

## Service

```text
Service
   ↓
Shared Logic + Shared Data
```

Example:

```typescript
@Injectable({ providedIn: "root" })
export class LogoService {

  companyName = "Resume Loop";

}
```

---

## Dependency Injection

```text
Component
    ↓
Requests Service
    ↓
Angular DI
    ↓
Provides Service
    ↓
Component Uses Service
```

---

## Singleton

```text
             ONE SERVICE INSTANCE
                      |
          +-----------+-----------+
          |           |           |
        Header      Footer      Profile
```

---

## Pipe

```text
Original Value
      ↓
     Pipe
      ↓
Formatted / Transformed Value
```

Example:

```html
{{ name | uppercase }}
```

---

## Custom Pipe

```text
@Pipe
   ↓
Pipe Class
   ↓
PipeTransform
   ↓
transform()
   ↓
Transformed Value
```

---

# 52. Final Mental Model

```text
                         ANGULAR
                            |
             +--------------+--------------+
             |                             |
             v                             v
         COMPONENTS                       PIPES
             |                             |
             | need shared work            |
             | or data                     |
             v                             |
          SERVICES                         |
             |                             |
             v                             |
        @Injectable                        |
             |                             |
             v                             |
    Dependency Injection                   |
             |                             |
             v                             |
    providedIn: "root"                     |
             |                             |
             v                             |
         SINGLETON                         |
             |                             |
             v                             |
     One Shared Instance                   |
             |                             |
       +-----+-----+                       |
       |     |     |                       |
       v     v     v                       v
    Header Footer Profile          Built-in / Custom
       |     |     |                       |
       +-----+-----+                       v
             |                         transform()
             v                            |
        Shared Data                       v
                                    Displayed Result
```

# Final Summary

- **Service** → Used for shared logic and shared data.
- **`@Injectable`** → Makes a class available for Angular Dependency Injection.
- **Dependency Injection** → Angular provides the required service to a component.
- **`providedIn: "root"`** → Makes the service available throughout the application and supports singleton behavior.
- **Singleton** → One shared service instance.
- **Shared Data** → Multiple components can access the same service data.
- **Pipe** → Formats or transforms a value for display.
- **Built-in Pipe** → Already provided by Angular.
- **Custom Pipe** → Created by the developer.
- **`@Pipe`** → Defines a custom pipe.
- **`PipeTransform`** → Interface used by custom pipes.
- **`transform()`** → Receives a value, transforms it, and returns the result.
- **Pipe Argument** → Extra value passed using `:`.
- **Pipe Chaining** → Multiple pipes can be applied one after another.

---
---

# Angular Day 7 — Forms in Angular

## 1. What Are Forms in Angular?

Forms are used whenever an Angular application needs to collect information from a user.

Common examples include:

- Login forms
- Signup forms
- Registration forms
- Search forms
- Contact forms
- Profile forms
- Data-entry forms

Angular provides two main approaches for creating forms:

```text
                         ANGULAR FORMS
                              |
                +-------------+-------------+
                |                           |
                v                           v
       TEMPLATE-DRIVEN                  REACTIVE
            FORMS                        FORMS
                |                           |
                v                           v
          Logic mostly                Logic mostly
            in HTML                   in TypeScript
                |                           |
                v                           v
             ngModel              FormGroup + FormControl
                |                           |
                v                           v
          FormsModule            ReactiveFormsModule
```

Both approaches are valid. The main difference is **where the form logic is written and how much control we have over the form**.

---

# 2. Two Types of Angular Forms

Angular provides:

1. Template-Driven Forms
2. Reactive Forms

## Template-Driven Forms

The form is mainly created and controlled from the HTML template.

Main concept:

```text
ngModel
```

Required module:

```text
FormsModule
```

Best suited for:

```text
Simple and small forms
```

---

## Reactive Forms

The form is mainly created and controlled from the TypeScript class.

Main concepts:

```text
FormGroup
FormControl
Validators
```

Required module:

```text
ReactiveFormsModule
```

Best suited for:

```text
Bigger forms
Complex forms
Forms with more validation
```

---

# 3. Template-Driven vs Reactive Forms

| Feature | Template-Driven | Reactive |
|---|---|---|
| Main logic | HTML template | TypeScript class |
| Main concept | `ngModel` | `FormGroup`, `FormControl` |
| Required module | `FormsModule` | `ReactiveFormsModule` |
| Best for | Small/simple forms | Bigger/complex forms |
| Validation | Simpler | More control |
| Amount of code | Less | More |
| Form definition | Mostly HTML | Mostly TypeScript |

### Simple Difference

```text
                 ANGULAR FORMS
                       |
          +------------+------------+
          |                         |
          v                         v
   TEMPLATE-DRIVEN              REACTIVE
          |                         |
          v                         v
       HTML                    TypeScript
          |                         |
          v                         v
      ngModel                  FormGroup
          |                         |
          v                         v
 Component Properties          FormControl
                                    |
                                    v
                                Validators
```

Template-driven forms are simpler to start with, while reactive forms provide more control and are useful for larger forms and validation.

---

# 4. Template-Driven Forms

In a template-driven form, most of the form structure and behavior is written in the HTML template.

The component class usually contains only the properties that store the form values and the method that handles submission.

The main Angular feature is:

```text
[(ngModel)]
```

Template-driven forms require:

```text
FormsModule
```

### Basic Structure

```text
                  TEMPLATE-DRIVEN FORM
                           |
                           v
                          HTML
                           |
                           v
                         Input
                           |
                           v
                       ngModel
                           |
                           v
                  Component Property
                           |
                           v
                        Submit
```

---

# 5. FormsModule

Template-driven forms use:

```text
FormsModule
```

This provides Angular's template-driven form functionality.

The relationship is:

```text
Template-Driven Form
        |
        v
      ngModel
        |
        v
   FormsModule
        |
        v
Angular Form Support
```

---

# 6. Basic Template-Driven Form

Example:

```html
<form (ngSubmit)="onSubmit()">

  <input
    name="username"
    [(ngModel)]="username"
    placeholder="Name"
  />

  <input
    name="email"
    [(ngModel)]="email"
    placeholder="Email"
  />

  <button type="submit">
    Submit
  </button>

</form>
```

The TypeScript class can contain:

```typescript
username: string = "";
email: string = "";

onSubmit() {
  console.log(this.username, this.email);
}
```

The important idea is that each input is connected to a component property using `[(ngModel)]`.

---

# 7. Understanding the `<form>` Element

The form starts with:

```html
<form (ngSubmit)="onSubmit()">
```

The important part is:

```text
(ngSubmit)
```

`ngSubmit` is used to handle form submission.

This:

```html
(ngSubmit)="onSubmit()"
```

means:

> When the form is submitted, call the `onSubmit()` method.

### Flow

```text
User
  |
  v
Fills Form
  |
  v
Clicks Submit
  |
  v
Form Submitted
  |
  v
ngSubmit
  |
  v
onSubmit()
```

---

# 8. Understanding the `name` Attribute

Each input has a `name` attribute.

Example:

```html
<input
  name="username"
  [(ngModel)]="username"
/>
```

Another input:

```html
<input
  name="email"
  [(ngModel)]="email"
/>
```

The form therefore contains two named fields:

```text
Form
 |
 +---- username
 |
 +---- email
```

The `name` attribute identifies the input field within the form.

---

# 9. What Is `ngModel`?

`ngModel` connects a form input with a component property.

Example:

```html
<input
  name="username"
  [(ngModel)]="username"
/>
```

Here:

```text
HTML Input
    |
    v
[(ngModel)]
    |
    v
username property
```

The input and component property remain connected.

---

# 10. What Is Two-Way Data Binding?

The syntax:

```html
[(ngModel)]
```

provides **two-way data binding**.

Two-way means data can move in both directions.

### Component → Input

```text
Component Property
       |
       v
     Input
```

### Input → Component

```text
Input
  |
  v
Component Property
```

Together:

```text
          Component Property
                  ↕
              [(ngModel)]
                  ↕
                Input
```

This is why `[(ngModel)]` is called two-way binding.

---

# 11. Example of Two-Way Binding

Suppose the component has:

```typescript
username: string = "";
```

And the template has:

```html
<input
  name="username"
  [(ngModel)]="username"
/>
```

Initially:

```text
username = ""
```

Now the user types:

```text
Unishka
```

Angular updates the component property:

```text
username = "Unishka"
```

### Flow

```text
User types "Unishka"
        |
        v
      Input
        |
        v
    [(ngModel)]
        |
        v
    username
        |
        v
"Unishka"
```

The value is now available inside the component.

---

# 12. Component-to-Input Direction

Suppose the component contains:

```typescript
username: string = "Unishka";
```

and the template contains:

```html
<input
  name="username"
  [(ngModel)]="username"
/>
```

The input will initially show:

```text
Unishka
```

The flow is:

```text
username = "Unishka"
        |
        v
    [(ngModel)]
        |
        v
      Input
        |
        v
    Displays:
    Unishka
```

---

# 13. Input-to-Component Direction

Now suppose the user changes:

```text
Unishka
```

to:

```text
Yashi
```

The component property also changes:

```text
username = "Yashi"
```

The flow is:

```text
User changes input
        |
        v
      Input
        |
        v
    [(ngModel)]
        |
        v
 username property
        |
        v
username = "Yashi"
```

---

# 14. Understanding the Username Input

Example:

```html
<input
  name="username"
  [(ngModel)]="username"
  placeholder="Name"
/>
```

There are three important parts.

### `name`

```html
name="username"
```

Identifies the field.

### `[(ngModel)]`

```html
[(ngModel)]="username"
```

Connects the input with the component property.

### `placeholder`

```html
placeholder="Name"
```

Displays hint text inside the input.

---

# 15. Understanding the Email Input

Example:

```html
<input
  name="email"
  [(ngModel)]="email"
  placeholder="Email"
/>
```

This connects the input with:

```typescript
email: string = "";
```

The relationship is:

```text
Email Input
     |
     v
[(ngModel)]
     |
     v
email property
```

---

# 16. Template-Driven Form Class

The component class can remain very simple:

```typescript
username: string = "";
email: string = "";

onSubmit() {
  console.log(this.username, this.email);
}
```

The HTML controls most of the form behavior.

The component mainly stores the values and handles submission.

### Structure

```text
HTML
 |
 +---- Username Input
 |
 +---- Email Input
 |
 +---- ngModel
 |
 +---- Submit
 |
 v
Component
 |
 +---- username
 |
 +---- email
 |
 +---- onSubmit()
```

---

# 17. What Happens When the Form Is Submitted?

Suppose the user enters:

```text
Name:
Unishka

Email:
unishka@example.com
```

Because of `[(ngModel)]`, the component contains:

```typescript
username = "Unishka";
email = "unishka@example.com";
```

When the user clicks Submit:

```text
User
  |
  v
Clicks Submit
  |
  v
ngSubmit
  |
  v
onSubmit()
  |
  v
this.username
this.email
  |
  v
Form values are available
```

---

# 18. Complete Template-Driven Form Flow

```text
                         USER
                          |
                          v
                     HTML FORM
                          |
              +-----------+-----------+
              |                       |
              v                       v
        Username Input            Email Input
              |                       |
              v                       v
         [(ngModel)]              [(ngModel)]
              |                       |
              v                       v
         username                 email
         property                 property
              |                       |
              +-----------+-----------+
                          |
                          v
                    User clicks Submit
                          |
                          v
                       ngSubmit
                          |
                          v
                       onSubmit()
                          |
                          v
                    Form values ready
```

---

# 19. Why Template-Driven Forms Are Simple

Most of the form configuration exists inside the HTML.

```text
HTML
 |
 +---- Form
 |
 +---- Input
 |
 +---- ngModel
 |
 +---- Submit
 |
 v
Component Properties
```

There is less TypeScript code.

Therefore, template-driven forms are suitable for:

- Small login forms
- Simple search forms
- Small registration forms
- Basic forms with limited validation

---

# 20. Reactive Forms

Reactive Forms work differently.

The form is created mainly inside the TypeScript class.

The HTML template connects to that form.

The three important concepts are:

```text
FormGroup
FormControl
Validators
```

Reactive forms require:

```text
ReactiveFormsModule
```

### Basic Structure

```text
                  REACTIVE FORM
                       |
                       v
                  TypeScript
                       |
                       v
                   FormGroup
                       |
             +---------+---------+
             |                   |
             v                   v
        FormControl         FormControl
             |                   |
             v                   v
         username              email
             |                   |
             +---------+---------+
                       |
                       v
                    Template
```

---

# 21. ReactiveFormsModule

Reactive forms require:

```text
ReactiveFormsModule
```

The basic relationship is:

```text
Reactive Form
      |
      v
  FormGroup
      |
      v
 FormControl
      |
      v
ReactiveFormsModule
```

---

# 22. FormGroup

`FormGroup` represents the **complete form**.

Example:

```typescript
signupForm = new FormGroup({
  username: ...,
  email: ...
});
```

Think of `FormGroup` as a container that holds the controls of the form.

```text
                 signupForm
                 FormGroup
                     |
          +----------+----------+
          |                     |
          v                     v
      username                email
```

---

# 23. FormControl

A `FormControl` represents **one individual form field**.

Example:

```typescript
username: new FormControl("")
```

represents the username field.

And:

```typescript
email: new FormControl("")
```

represents the email field.

### Simple Rule

```text
FormGroup
   ↓
Whole Form

FormControl
   ↓
One Field
```

---

# 24. FormGroup + FormControl Relationship

```text
                  FormGroup
                     |
          +----------+----------+
          |                     |
          v                     v
    FormControl           FormControl
          |                     |
          v                     v
      username                email
```

So if a form has five fields, it can have five `FormControl`s inside one `FormGroup`.

---

# 25. Creating a Reactive Form

Example:

```typescript
import { Component } from "@angular/core";
import {
  FormGroup,
  FormControl,
  Validators
} from "@angular/forms";

@Component({
  /* ... */
})
export class SignupComponent {

  signupForm = new FormGroup({

    username: new FormControl(
      "",
      Validators.required
    ),

    email: new FormControl(
      "",
      [
        Validators.required,
        Validators.email
      ]
    )

  });

  onSubmit() {
    console.log(this.signupForm.value);
  }

}
```

The form is created inside the TypeScript class using `FormGroup` and `FormControl`.

---

# 26. Understanding the Imports

The reactive form uses:

```typescript
import {
  FormGroup,
  FormControl,
  Validators
} from "@angular/forms";
```

These have different purposes:

```text
FormGroup
    ↓
Represents the complete form

FormControl
    ↓
Represents one form field

Validators
    ↓
Checks whether form values are valid
```

---

# 27. Creating the FormGroup

The form starts with:

```typescript
signupForm = new FormGroup({
```

This creates the overall form object.

```text
signupForm
    |
    v
FormGroup
```

Inside the `FormGroup`, individual fields are defined.

```text
signupForm
    |
    +---- username
    |
    +---- email
```

---

# 28. Creating the Username FormControl

The username control is:

```typescript
username: new FormControl(
  "",
  Validators.required
)
```

It has two important parts.

### Initial Value

```text
""
```

The field initially contains an empty string.

### Validator

```text
Validators.required
```

The field cannot be empty.

### Structure

```text
Username
    |
    v
FormControl
    |
    +---- Initial value: ""
    |
    +---- Validator: required
```

---

# 29. Creating the Email FormControl

The email control is:

```typescript
email: new FormControl(
  "",
  [
    Validators.required,
    Validators.email
  ]
)
```

It contains:

```text
Initial Value
      ↓
""

Validators
      ↓
required
email
```

Therefore:

1. The email field cannot be empty.
2. The value must have a valid email format.

---

# 30. Reactive Form Template

The template connects to the `FormGroup`:

```html
<form
  [formGroup]="signupForm"
  (ngSubmit)="onSubmit()"
>

  <input
    formControlName="username"
    placeholder="Name"
  />

  <input
    formControlName="email"
    placeholder="Email"
  />

  <button
    type="submit"
    [disabled]="signupForm.invalid"
  >
    Submit
  </button>

</form>
```

---

# 31. Understanding `[formGroup]`

The HTML form contains:

```html
[formGroup]="signupForm"
```

This connects the HTML form to the `signupForm` object created in TypeScript.

```text
TypeScript
    |
    v
signupForm
    |
    | [formGroup]
    v
HTML Form
```

So the template knows which `FormGroup` it belongs to.

---

# 32. Understanding `formControlName`

The username input contains:

```html
formControlName="username"
```

The email input contains:

```html
formControlName="email"
```

These connect the inputs to the corresponding `FormControl`s.

```text
                    FormGroup
                        |
            +-----------+-----------+
            |                       |
            v                       v
    username FormControl     email FormControl
            |                       |
            v                       v
formControlName="username" formControlName="email"
            |                       |
            v                       v
      Username Input            Email Input
```

---

# 33. Reactive Form Data Flow

```text
                TypeScript
                    |
                    v
                FormGroup
                    |
          +---------+---------+
          |                   |
          v                   v
     FormControl         FormControl
      username               email
          |                   |
          v                   v
 formControlName       formControlName
          |                   |
          v                   v
     HTML Input           HTML Input
          |                   |
          +---------+---------+
                    |
                    v
                User Input
```

---

# 34. Understanding `[disabled]`

The submit button contains:

```html
[disabled]="signupForm.invalid"
```

This means:

> Disable the submit button when the form is invalid.

The flow is:

```text
                 signupForm
                      |
                      v
                 Is invalid?
                 /        \
               YES         NO
                |           |
                v           v
            Disabled      Enabled
              Button        Button
```

So:

```text
Valid Form
    ↓
Submit Enabled
```

and:

```text
Invalid Form
    ↓
Submit Disabled
```

---

# 35. Reactive Form Submission

The component contains:

```typescript
onSubmit() {
  console.log(this.signupForm.value);
}
```

When the user submits:

```text
User clicks Submit
       |
       v
(ngSubmit)
       |
       v
onSubmit()
       |
       v
signupForm.value
       |
       v
All form values
```

For example:

```text
{
  username: "Unishka",
  email: "unishka@example.com"
}
```

---

# 36. Validation

Validation means checking whether the data entered by the user is acceptable.

For example:

```text
Username
    |
    v
Required
    |
    v
Cannot be empty
```

And:

```text
Email
    |
    +----> Required
    |
    +----> Valid Email Format
```

Reactive forms make validation easier because validators can be directly attached to `FormControl`s.

---

# 37. Validators.required

```typescript
Validators.required
```

means:

> The field cannot be empty.

Example:

```typescript
username: new FormControl(
  "",
  Validators.required
)
```

### Flow

```text
             Username Input
                    |
                    v
           Validators.required
                    |
                    v
              Is it empty?
                /       \
              YES        NO
               |          |
               v          v
            Invalid      Valid
```

---

# 38. Validators.email

```typescript
Validators.email
```

means:

> The value must have a valid email format.

Example:

```typescript
email: new FormControl(
  "",
  Validators.email
)
```

### Flow

```text
              Email Input
                   |
                   v
           Validators.email
                   |
                   v
        Valid Email Format?
             /          \
           YES           NO
            |             |
            v             v
          Valid         Invalid
```

---

# 39. Validators.minLength()

Example:

```typescript
Validators.minLength(6)
```

Meaning:

> The value must contain at least 6 characters.

### Flow

```text
Input
  |
  v
minLength(6)
  |
  v
Count Characters
  |
  +------> 6 or more ------> Valid
  |
  +------> Less than 6 ----> Invalid
```

Example:

```text
"abcdef"
   ↓
6 characters
   ↓
Valid
```

But:

```text
"abc"
  ↓
3 characters
  ↓
Invalid
```

---

# 40. Validators.maxLength()

Example:

```typescript
Validators.maxLength(20)
```

Meaning:

> The value can contain at most 20 characters.

### Flow

```text
Input
  |
  v
maxLength(20)
  |
  v
Count Characters
  |
  +------> 20 or less ------> Valid
  |
  +------> More than 20 ----> Invalid
```

---

# 41. Multiple Validators

A field can have multiple validators.

Example:

```typescript
email: new FormControl(
  "",
  [
    Validators.required,
    Validators.email
  ]
)
```

This means the email must satisfy both conditions.

```text
                       Email
                         |
             +-----------+-----------+
             |                       |
             v                       v
      Validators.required     Validators.email
             |                       |
             v                       v
       Cannot be empty        Valid email format
             |                       |
             +-----------+-----------+
                         |
                         v
                    Valid Field
```

If any required condition fails, the control becomes invalid.

---

# 42. Validation Flow

```text
                    User Input
                        |
                        v
                    FormControl
                        |
                        v
                     Validators
                        |
             +----------+----------+
             |                     |
             v                     v
           Valid                Invalid
             |                     |
             v                     v
       Form is valid         Form is invalid
             |                     |
             v                     v
      Submit possible       Submit disabled
```

---

# 43. Form State

Angular allows us to check whether a form is valid or invalid.

### Check if the complete form is valid

```typescript
signupForm.valid
```

### Check if the complete form is invalid

```typescript
signupForm.invalid
```

### Check a specific field

```typescript
signupForm.get('email')?.invalid
```

This checks the validation state of the email control.

---

# 44. Form State Flow

```text
                    signupForm
                         |
             +-----------+-----------+
             |                       |
             v                       v
           valid                   invalid
             |                       |
             v                       v
          true                    true
```

For a single field:

```text
signupForm
    |
    v
get('email')
    |
    v
Email FormControl
    |
    v
invalid
    |
    v
true / false
```

---

# 45. Complete Reactive Validation Flow

```text
                     USER
                      |
                      v
                  Form Input
                      |
                      v
                 FormControl
                      |
                      v
                  Validators
                      |
          +-----------+-----------+
          |                       |
          v                       v
        Valid                  Invalid
          |                       |
          v                       v
    Form is valid           Form is invalid
          |                       |
          v                       v
 Submit can be enabled      Submit is disabled
```

---

# 46. Complete Template-Driven Form Flow

```text
                         USER
                          |
                          v
                     HTML FORM
                          |
              +-----------+-----------+
              |                       |
              v                       v
        Username Input            Email Input
              |                       |
              v                       v
         [(ngModel)]              [(ngModel)]
              |                       |
              v                       v
         username                 email
         property                 property
              |                       |
              +-----------+-----------+
                          |
                          v
                    User clicks Submit
                          |
                          v
                       ngSubmit
                          |
                          v
                       onSubmit()
                          |
                          v
                    Form Values Ready
```

---

# 47. Complete Reactive Form Flow

```text
                      USER
                       |
                       v
                  HTML FORM
                       |
                       v
                [formGroup]
                       |
                       v
                  FormGroup
                       |
             +---------+---------+
             |                   |
             v                   v
        FormControl         FormControl
         username               email
             |                   |
             v                   v
      formControlName      formControlName
             |                   |
             v                   v
      Username Input         Email Input
             |                   |
             +---------+---------+
                       |
                       v
                  User enters data
                       |
                       v
                   Validators
                       |
             +---------+---------+
             |                   |
             v                   v
           Valid              Invalid
             |                   |
             v                   v
      Submit Enabled       Submit Disabled
```

---

# 48. Template-Driven Form Architecture

```text
                  TEMPLATE-DRIVEN
                         |
                         v
                        HTML
                         |
          +--------------+--------------+
          |                             |
          v                             v
     Username Input                Email Input
          |                             |
          v                             v
     [(ngModel)]                   [(ngModel)]
          |                             |
          v                             v
       username                      email
          |                             |
          +--------------+--------------+
                         |
                         v
                     Component
                         |
                         v
                      Submit
                         |
                         v
                     ngSubmit
                         |
                         v
                     onSubmit()
```

---

# 49. Reactive Form Architecture

```text
                     REACTIVE FORM
                           |
                           v
                       TypeScript
                           |
                           v
                       FormGroup
                           |
              +------------+------------+
              |                         |
              v                         v
        FormControl               FormControl
         username                    email
              |                         |
              +------------+------------+
                           |
                           v
                        Template
                           |
              +------------+------------+
              |                         |
              v                         v
        formControlName          formControlName
              |                         |
              v                         v
        Username Input             Email Input
                           |
                           v
                       Validators
                           |
                   +-------+-------+
                   |               |
                   v               v
                 Valid          Invalid
```

---

# 50. When to Use Template-Driven Forms

Template-driven forms are suitable when the form is:

- Small
- Simple
- Quick to build
- Not heavily dependent on complex validation

Examples:

```text
Simple Login Form
       |
       v
Template-Driven


Simple Search Form
       |
       v
Template-Driven


Small Registration Form
       |
       v
Template-Driven
```

---

# 51. When to Use Reactive Forms

Reactive forms are suitable when the form:

- Has many fields
- Requires multiple validators
- Needs complex validation
- Requires more programmatic control
- Has complicated form state

Example:

```text
Large Signup Form
       |
       +---- Many Fields
       |
       +---- Complex Validation
       |
       +---- Form State
       |
       v
Reactive Form
```

---

# 52. Simple Decision Flow

```text
                  Need an Angular Form
                           |
                           v
                    Is the form simple?
                     /            \
                   YES             NO
                    |               |
                    v               v
             Template-Driven     Reactive
                    |               |
                    v               v
                 ngModel       FormGroup
                                  +
                              FormControl
                                  +
                              Validators
```

---

# 53. Template-Driven Mental Model

```text
HTML
  |
  v
Form
  |
  v
Input
  |
  v
[(ngModel)]
  |
  v
Component Property
  |
  v
Submit
  |
  v
ngSubmit
  |
  v
onSubmit()
```

The main idea:

> **The template controls most of the form.**

---

# 54. Reactive Mental Model

```text
TypeScript
    |
    v
FormGroup
    |
    v
FormControl
    |
    v
Validators
    |
    v
HTML Template
    |
    v
User Input
    |
    v
Form State
    |
    +----> Valid
    |
    +----> Invalid
```

The main idea:

> **The TypeScript class controls most of the form.**

---

# 55. Important Syntax to Remember

## Template-Driven

```html
<form (ngSubmit)="onSubmit()">

  <input
    name="username"
    [(ngModel)]="username"
  />

  <input
    name="email"
    [(ngModel)]="email"
  />

  <button type="submit">
    Submit
  </button>

</form>
```

Remember:

```text
FormsModule
ngModel
[(ngModel)]
name
ngSubmit
```

---

## Reactive

```typescript
signupForm = new FormGroup({

  username: new FormControl(
    "",
    Validators.required
  ),

  email: new FormControl(
    "",
    [
      Validators.required,
      Validators.email
    ]
  )

});
```

Template:

```html
<form
  [formGroup]="signupForm"
  (ngSubmit)="onSubmit()"
>

  <input
    formControlName="username"
  />

  <input
    formControlName="email"
  />

  <button
    type="submit"
    [disabled]="signupForm.invalid"
  >
    Submit
  </button>

</form>
```

Remember:

```text
ReactiveFormsModule
FormGroup
FormControl
Validators
[formGroup]
formControlName
```

---

# 56. Quick Revision Table

| Concept | Meaning |
|---|---|
| Angular Form | Used to collect user input |
| Template-Driven Form | Form mainly controlled from HTML |
| Reactive Form | Form mainly controlled from TypeScript |
| `FormsModule` | Required for template-driven forms |
| `ReactiveFormsModule` | Required for reactive forms |
| `ngModel` | Connects an input with a component property |
| `[(ngModel)]` | Two-way data binding |
| `ngSubmit` | Handles form submission |
| `FormGroup` | Represents the complete reactive form |
| `FormControl` | Represents one individual field |
| `[formGroup]` | Connects HTML form to a `FormGroup` |
| `formControlName` | Connects an input to a `FormControl` |
| `Validators.required` | Field cannot be empty |
| `Validators.email` | Must be a valid email |
| `Validators.minLength(6)` | At least 6 characters |
| `Validators.maxLength(20)` | At most 20 characters |
| `.valid` | Checks whether form/control is valid |
| `.invalid` | Checks whether form/control is invalid |

---

# 57. Final Revision Flowchart

```text
                              ANGULAR FORMS
                                   |
                    +--------------+--------------+
                    |                             |
                    v                             v
             TEMPLATE-DRIVEN                  REACTIVE
                    |                             |
                    v                             v
                  HTML                       TypeScript
                    |                             |
                    v                             v
                ngModel                     FormGroup
                    |                             |
                    v                             v
            Two-Way Binding                 FormControl
                    |                             |
                    v                             v
          Component Property                Validators
                    |                             |
                    v                             v
                 Submit                    Valid / Invalid
                    |                             |
                    v                             v
                ngSubmit                    Form State
                    |                             |
                    v                             v
                onSubmit()               Submit Enabled/
                                         Submit Disabled
```

---

# 58. Final Summary

> **Angular provides two main approaches for handling forms: Template-Driven Forms and Reactive Forms. Template-driven forms are mainly created in HTML and use `ngModel` for two-way data binding. They are simple and suitable for small forms. Reactive forms are mainly created in TypeScript using `FormGroup` and `FormControl`. They provide more control and work well for larger forms and complex validation. Validators such as `Validators.required`, `Validators.email`, `Validators.minLength()`, and `Validators.maxLength()` are used to check user input.**

```text
TEMPLATE-DRIVEN
      ↓
HTML-based
      ↓
ngModel
      ↓
Two-way Binding
      ↓
FormsModule
      ↓
Small / Simple Forms
```

```text
REACTIVE
      ↓
TypeScript-based
      ↓
FormGroup
      ↓
FormControl
      ↓
Validators
      ↓
ReactiveFormsModule
      ↓
Large / Complex Forms
```

```text
VALIDATION
      ↓
Validators.required
      ↓
Validators.email
      ↓
Validators.minLength()
      ↓
Validators.maxLength()
      ↓
valid / invalid
```
# Final Summary

> ** For user input, Angular provides two form approaches: template-driven forms, which are mainly built in HTML using `ngModel` and are suitable for simple forms, and reactive forms, which are mainly built in TypeScript using `FormGroup`, `FormControl`, and validators and are better suited for larger forms and validation.**
