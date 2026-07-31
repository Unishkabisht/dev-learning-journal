# The Event Loop in Node.js

Node.js is **single-threaded**, but it can still handle thousands of tasks at once. The secret is the **Event Loop** — a manager that decides what runs next.

There are 4 main parts to understand:

1. **Call Stack** – where your code actually runs, one thing at a time
2. **Web / Node APIs** – background helpers that do the slow waiting (timers, file reads, network)
3. **Callback Queue** – a waiting line for finished background jobs
4. **Event Loop** – constantly checks: "Is the stack empty? If yes, move the next job in."

---

## 1) The Big Picture

```
   CALL STACK                     WEB / NODE APIs
 ┌───────────────┐    slow job   ┌──────────────────┐
 │  (one at a     │ ───────────► │  timers, file     │
 │   time, top    │               │  reads, network,  │
 │   = newest)    │               │  database         │
 │                │ ◄───────────  │  (they wait here) │
 │   second()     │  when done,   └──────────────────┘
 │   first()      │  callback
 │   main()       │  joins queue
 └───────▲────────┘
         │                         CALLBACK QUEUE
         │ loop moves callback    ┌──────────────────┐
         │ to stack ONLY when     │  cb1 → cb2 → cb3  │
         │ the stack is empty     │  (waiting turn)   │
         │                        └─────────┬────────┘
         │                                  │
         │           ┌──────────────┐       │
         └───────────│  EVENT LOOP  │◄──────┘
                      └──────────────┘
```

**Rule of thumb:** Code runs on the stack → slow jobs go to the APIs → finished jobs wait in the queue → the loop moves them back to the stack only when the stack is empty.

---

## 2) Why "Stack" and Why "Queue"? (names matter!)

| Term | Behaves like | Rule |
|---|---|---|
| **Call Stack** | A stack of plates | **LIFO** – Last In, First Out. Newest call sits on top, finishes first. |
| **Callback Queue** | A line at a shop | **FIFO** – First In, First Out. First one waiting is first one served. |

---

## 3) Warm-up: Normal Code on the Call Stack (no async yet)

```js
console.log("start")

function second() {
  console.log("second")
}

function first() {
  console.log("first")
  second()
}

first()
console.log("end")
```

**Output:**
```
start
first
second
end
```

### Step by step:

| Step | What happens | Stack (top → bottom) |
|---|---|---|
| 1 | `console.log("start")` runs, prints `start` | `main()` |
| 2 | `first()` is called → goes on stack | `first()`, `main()` |
| 3 | Inside `first()`, prints `first` | `first()`, `main()` |
| 4 | `first()` calls `second()` → goes on top | `second()`, `first()`, `main()` |
| 5 | Inside `second()`, prints `second`, then `second()` finishes and pops off, then `first()` pops off | `main()` |
| 6 | Back in main, prints `end` | `main()` |

✅ **Key takeaway:** `second()` sits ON TOP of `first()` because `first()` called it while still running — LIFO in action.

---

## 4) Now the Real Example — `setTimeout`

This is the one that trips everyone up. Read it first, guess the output, then check:

```js
console.log("A")

setTimeout(function () {
  console.log("B")
}, 0)

console.log("C")
```

**Output:**
```
A
C
B
```

Surprise — `B` prints LAST, even though the timer is `0` ms! Here's exactly why, line by line.

### Step-by-step flow: where each line goes

| Step | Line | Stack | Web API | Queue |
|---|---|---|---|---|
| **1** | `console.log("A")` runs directly on stack, prints `A`, then pops off | `log(A)` → empty | idle | empty |
| **2** | `setTimeout(...)` goes on stack. It does **NOT** run the function. It hands `B`'s function to the Web API and says "start a 0ms timer", then pops off | `setTimeout` → empty | timer running (0ms) | empty |
| **3** | `console.log("C")` runs directly on stack, prints `C`, then pops off | `log(C)` → empty | timer done, `B` moves out | empty |
| **4** | The 0ms timer is already finished. `B`'s callback moves from the Web API into the **Callback Queue** and waits there | empty | idle | `[cb: log(B)]` |
| **5** | Main program ends → **stack is empty**. Event Loop sees this, grabs `B` from the queue, puts it on the stack. It runs, prints `B` | `log(B)` → empty | idle | empty |

### Visual flow:

```
Step 1                Step 2                  Step 3
┌─────────┐  ┌───────┐ ┌─────────┐  ┌───────┐ ┌─────────┐  ┌───────┐
│ stack   │  │ queue │ │ stack   │  │ queue │ │ stack   │  │ queue │
│ log(A)  │  │ empty │ │setTimeout│  │ empty │ │ log(C)  │  │ empty │
│ main()  │  │       │ │ main()  │  │       │ │ main()  │  │       │
└─────────┘  └───────┘ └─────────┘  └───────┘ └─────────┘  └───────┘
prints "A"             timer sent to Web API   prints "C"

Step 4                        Step 5
┌─────────┐  ┌────────────┐  ┌─────────┐  ┌───────┐
│ stack   │  │ queue      │  │ stack   │  │ queue │
│ (empty) │  │ cb: log(B) │  │cb:log(B)│  │ empty │
└─────────┘  └────────────┘  └─────────┘  └───────┘
stack empty, main done         loop moves cb in, prints "B"
```

**Output order: `A → C → B`**

###  The key point to remember:

> `setTimeout(fn, 0)` does **NOT** mean "run now." It means "hand this function to the background, and run it later — once the stack is completely empty." Later is almost always after ALL your normal code has finished.

---

## 5) Why Do We Even Do This?

Because some jobs are **slow**: reading a file, calling a database, waiting on the network. If the call stack waited for these directly, everything would **freeze** — no other request could be handled.

```js
// THE BAD WAY — this blocks/freezes everything
console.log("start")

const end = Date.now() + 2000
while (Date.now() < end) {}   // sits and waits 2 seconds, doing nothing

console.log("done")
```

For those 2 seconds, the stack is stuck. Nothing else can run. No other user gets served. This is called **blocking**.

The Event Loop exists exactly so we never have to do this — slow jobs go to the background (Web/Node APIs), and the stack stays free to keep working.

---

## 6) Bonus: Promises Jump the Line!

```js
console.log("1")

setTimeout(function () { console.log("2") }, 0)

Promise.resolve().then(function () { console.log("3") })

console.log("4")
```

**Output:**
```
1
4
3
2
```

Normal code runs first (`1`, then `4`). Then the Promise (`3`) runs **before** the timer (`2`) — even though both were "ready" around the same time.

### Why? There are actually TWO queues:

| Queue | Holds | Priority |
|---|---|---|
| **Microtask Queue** | Promises (`.then`) | Checked FIRST, emptied completely |
| **Macrotask Queue** | `setTimeout`, `setInterval` | Checked only AFTER microtasks are empty |

**The Rule:** After each task finishes, the Event Loop empties **ALL** microtasks before taking even one macrotask.

That's why a Promise always runs before a `setTimeout(.., 0)`.

>  **Remember the order: normal code → then Promises → then timers.**

---

##  Key Takeaways

- ✔️ Stack = where code runs, one thing at a time (LIFO)
- ✔️ Web/Node APIs = do the slow waiting so the stack stays free
- ✔️ Queue = finished background jobs wait here for their turn (FIFO)
- ✔️ Event Loop = moves the next job from queue → stack, but ONLY when stack is empty
- ✔️ `setTimeout(fn, 0)` still waits for all normal code to finish first
- ✔️ Promises (microtasks) always run before `setTimeout` (macrotasks)

## ❌ Common Mistakes

- Thinking `setTimeout(fn, 0)` runs the function immediately — it doesn't
- Forgetting that Promises jump ahead of timers
- Assuming Node.js is multi-threaded because it "handles many things at once" — it's actually single-threaded with a smart Event Loop

##  Interview Fact

Node.js achieves concurrency not through multi-threading, but by **offloading slow I/O work to the system (via libuv)** and using the Event Loop to bring results back to the single main thread at the right time.

