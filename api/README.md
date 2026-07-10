# 📘 Learning API Day 1.

**Topic:** Understanding APIs, HTTP methods, status codes, fetch(), and authentication basics

---

## 1. What is an API?

**Definition:** An API (Application Programming Interface) is a set of rules that lets one piece of software talk to another. It defines how to ask for something, and what you'll get back.

### The Restaurant Analogy

You sit at a restaurant table. You don't walk into the kitchen and cook your own food — you tell the waiter what you want. The waiter takes your order to the kitchen, waits, and brings your food back to you.

- **You** = the client (asking for something)
- **The waiter** = the API (carries the request and the response)
- **The kitchen** = the server (actually prepares/processes the data)

You never need to know how the kitchen cooks the dish. You only need to know how to order it. That's exactly what an API does between an app and a server.

---

## 2. Client and Server

**Client:** The one who starts the conversation — a browser, a mobile app, or JavaScript code. The client asks for something.

**Server:** The one who listens, processes, and replies. The server never speaks first.

**Golden Rule:** The client always speaks first. And every single request gets exactly **one** response — not zero, not two.

---

## 3. Anatomy of a Request and a Response

### A Request has 4 parts

| Part | Definition |
|---|---|
| **Method** | The action you want to perform (GET, POST, PUT, PATCH, DELETE) |
| **URL** | The address of the resource you are asking for |
| **Headers** | Extra information about the request, like metadata (content type, auth token) |
| **Body** | The actual data being sent (used in POST, PUT, PATCH — usually not in GET) |

### A Response has 3 parts

| Part | Definition |
|---|---|
| **Status Code** | A three-digit number telling you if the request succeeded or failed |
| **Headers** | Metadata about the response |
| **Body** | The actual data the server sends back |

---

## 4. Read the Status Code First

**Definition:** The status code is the first and most trustworthy thing to check in a response. It tells you the real outcome before you even look at the data.

**A body can lie, the status code doesn't.** A response body might look like normal data, but if the status code says `404` or `500`, the request actually failed. Always check the status code before trusting the body.

---

## 5. JSON as the Data Format

**Definition:** JSON (JavaScript Object Notation) is a lightweight, text-based format used to exchange data between client and server. It looks like a JS object, but it's actually just text.

```json
{
  "name": "iPhone 16 Pro",
  "price": 134900,
  "inStock": true
}
```

| Method | Purpose | Definition |
|---|---|---|
| `response.json()` | Parsing | Converts JSON text received from the server into a usable JavaScript object |
| `JSON.stringify()` | Sending | Converts a JavaScript object into JSON text so it can be sent to the server |

```
JavaScript Object → JSON.stringify() → JSON Text → sent over network → Server
Server → sends JSON text back → response.json() → JavaScript Object again
```

---

## 6. The Five HTTP Methods

**Definition:** HTTP methods are verbs that describe what action you want to perform on a resource.

| Method | Action | Definition |
|---|---|---|
| **GET** | Read | Ask the server for existing data, without changing anything |
| **POST** | Create | Ask the server to create a new piece of data |
| **PUT** | Replace | Ask the server to completely replace an existing resource |
| **PATCH** | Update | Ask the server to update only part of a resource |
| **DELETE** | Remove | Ask the server to delete a resource |

---

## 7. GET vs POST

**Definition:** GET sends its data as part of the URL itself (query parameters). POST sends its data hidden inside the request body.

| | GET | POST |
|---|---|---|
| **Where data goes** | In the URL (`?search=iphone16`) | In the body (hidden) |
| **Use case** | Fetching/reading data | Creating new data |
| **Safe to repeat?** | Yes | **No** |

**Why POST is not safe to repeat:** An action is "safe to repeat" if doing it multiple times gives the same result as doing it once. GET is safe — asking for the same data again just shows you the same thing. **POST is not safe** — if you submit a signup form and refresh the page right after, the browser may resend that same POST, and you end up creating the account twice.

---

## 8. Status Code Families

**Definition:** Status codes are grouped into five families by their first digit, each representing a category of outcome.

| Family | Meaning |
|---|---|
| **1xx** | Informational — request received, still processing |
| **2xx** | Success — request completed successfully |
| **3xx** | Redirection — resource has moved, follow the new location |
| **4xx** | Client Error — something is wrong with the request you sent |
| **5xx** | Server Error — something broke on the server's side |

### Everyday codes

| Code | Name | Definition |
|---|---|---|
| `200` | OK | Request succeeded, here's your data |
| `201` | Created | A new resource was successfully created |
| `204` | No Content | Request succeeded, nothing to send back |
| `400` | Bad Request | The request was malformed or missing data |
| `401` | Unauthorized | You're not logged in / no valid credentials |
| `403` | Forbidden | You're identified, but don't have permission |
| `404` | Not Found | The resource doesn't exist |
| `429` | Too Many Requests | You're being rate limited |
| `500` | Internal Server Error | Something broke on the server |

---

## 9. REST URL Design — URLs are Nouns, Methods are Verbs

**Definition:** REST is a design style where the URL identifies *what thing* you're working with (a noun), and the HTTP method identifies *what action* you want to perform (a verb).

```
✅ Correct:
GET    /mobiles          → read all mobiles
GET    /mobiles/5        → read mobile with id 5
POST   /mobiles          → add a new mobile
PUT    /mobiles/5        → replace mobile 5 entirely
PATCH  /mobiles/5        → update part of mobile 5
DELETE /mobiles/5        → delete mobile 5

❌ Wrong (verb baked into the URL):
GET /getAllMobiles
POST /createNewMobile
POST /deleteMobile5
```

---

## 10. fetch() — .then() vs async/await

**Definition:** `fetch()` is a built-in JavaScript function used to make HTTP requests from the browser to a server.

### Style 1: `.then()` chaining

```js
fetch("https://resumeflow-api.example.com/login", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    email: "yashi@example.com",
    password: "mypassword123"
  })
})
  .then(res => res.json())
  .then(data => console.log("Logged in:", data))
  .catch(err => console.log("Error:", err));
```

### Style 2: async/await (cleaner)

```js
async function loginUser() {
  const res = await fetch("https://resumeflow-api.example.com/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      email: "yashi@example.com",
      password: "mypassword123"
    })
  });
  const data = await res.json();
  console.log("Logged in:", data);
}
```

### Why you await twice

**Definition:** Both `fetch()` and `.json()` are asynchronous — they each take time and return a Promise, so each needs its own `await`.

1. **First await** — waits for the request to reach the server and the response to start arriving
2. **Second await** — waits for the response body to be fully read and converted from JSON text into a JS object

---

## 11. Sending Data with fetch()

**Definition:** To send data, you pass a second argument to `fetch()` — an object with `method`, `headers`, and `body`.

```js
async function createAccount() {
  const res = await fetch("https://resumeflow-api.example.com/signup", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      name: "Unishka Bisht",
      email: "yashi@example.com",
      password: "mypassword123"
    })
  });
  const data = await res.json();
  console.log(data);
}
```

| Field | Definition |
|---|---|
| `method` | Which HTTP verb to use |
| `headers` | Tells the server what kind of data you're sending |
| `body` | The actual data, converted to JSON text using `JSON.stringify()` |

---

## 12. Error Handling with fetch()

**Definition:** `fetch()` only rejects (throws an error) on a **network failure** — like no internet or the server being unreachable. It does **NOT** throw on `404` or `500`. If the server responds with an error status, `fetch()` still treats it as a technically successful request. You have to check this yourself.

```js
async function loginUser() {
  try {
    const res = await fetch("https://resumeflow-api.example.com/login", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        email: "yashi@example.com",
        password: "wrongpassword"
      })
    });

    if (!res.ok) {
      throw new Error(`Login failed with status ${res.status}`);
    }

    const data = await res.json();
    console.log("Welcome:", data);
  } catch (err) {
    console.log("Something went wrong:", err.message);
  }
}
```

**`res.ok`** is `true` for status codes 200–299, and `false` for anything else.

---

## 13. Auth Basics — API Keys, Bearer Tokens, and .env

**Definition:** Authentication is proving *who you are* to a server before it lets you access protected data.

### API Keys

A unique string identifying who's making the request, usually sent as a header.

```js
fetch("https://api.example.com/data", {
  headers: {
    "x-api-key": "your-secret-key-here"
  }
});
```

### Bearer Tokens

A token sent in the `Authorization` header, proving the client already logged in. "Bearer" means whoever is holding this token is trusted.

```js
fetch("https://resumeflow-api.example.com/profile", {
  headers: {
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIs..."
  }
});
```

### Keeping keys in .env

**Definition:** A `.env` file stores secret values (keys, passwords, tokens) outside your actual code, so they're never accidentally exposed.

```
# .env
API_KEY=abc123secretkey
```

```js
// Used only on the backend (Node.js)
const apiKey = process.env.API_KEY;
```

### The Golden Rule

> **Secret keys never go in frontend code or git.**

- **Never in frontend code** — anything in browser JS is visible to anyone who opens DevTools.
- **Never in git** — if a key gets committed and pushed, it stays in commit history forever, even after deleting it later. Always add `.env` to `.gitignore`.

---

## 14. The Other Side — Express

**Definition:** Express is a Node.js framework used to build servers — this is the code that *receives* the fetch requests sent above.

```js
const express = require("express");
const app = express();
app.use(express.json());

// GET - read data
app.get("/mobiles", (req, res) => {
  res.status(200).json({ mobiles: ["iPhone 16", "Galaxy S25"] });
});

// POST - create data
app.post("/login", (req, res) => {
  const { email, password } = req.body;
  if (password !== "mypassword123") {
    return res.status(403).json({ message: "Incorrect email or password" });
  }
  res.status(200).json({ message: "Login successful" });
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

---

## 15. Live Demo — PokeAPI in the Console

Tried this directly in the browser console to see everything together — real URL, GET method, checking `res.ok`, then parsing with `.json()`.

```js
async function getPokemon(name) {
  const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);

  if (!res.ok) {
    console.log("Pokemon not found, status:", res.status);
    return;
  }

  const data = await res.json();
  console.log(data.name, data.height, data.weight);
}

getPokemon("pikachu");
```

Output in console:
```
pikachu 4 60
```

---
---

# Day 2 — APIs & Backend Basics

> Node.js · Class Notes
> ★ = exam important &nbsp;&nbsp; ↯ = interview favourite &nbsp;&nbsp; ✎ = note-worthy &nbsp;&nbsp; ✗ = common mistake

---

## 1. What is an API?

**Definition:** An **API (Application Programming Interface)** is a middleman that allows two separate programs to talk to each other, without the client ever needing to touch the database directly.

**Restaurant analogy:**
- **You (the customer)** place an order — this is the client making a request.
- **The waiter (the API)** carries your order to the kitchen and later brings your food back.
- **The kitchen (the server)** does the actual work of preparing your order.
- **The pantry (the database)** is where all the raw data/ingredients are stored.

★ You never walk into the kitchen yourself — the waiter (API) protects it. A client never touches the database directly; it always goes through the API.

```mermaid
flowchart LR
    A["YOU (Customer)<br/>'1 paneer pizza'"] -->|request| B["WAITER = API<br/>carries messages both ways"]
    B -->|routes it| C["KITCHEN = SERVER<br/>does the work"]
    C -->|query| D["PANTRY = DB<br/>stores everything"]
    D -->|food comes back| C
    C -->|response = JSON| B
    B -->|response| A
```

---

## 2. The Round Trip

**Client → API → Server → Database → data flows back up as JSON**

```mermaid
flowchart LR
    Client["CLIENT"] --> API["API"] --> Server["SERVER"] --> DB["DATABASE"]
    DB -.->|JSON response| Server -.-> API -.-> Client
```

✎ This exact round trip happens for **every tap you make in any app**.

---

## 3. APIs Around You (Real-World Examples)

| App | What the API does |
|---|---|
| Google Maps | App asks Maps API — "where am I? fastest route?" |
| Instagram | Feed API fetches posts; like button = `POST /likes` |
| WhatsApp | Message API delivers your text + the ✓✓ receipts |
| YouTube | Video API sends the list, another streams the video |
| Paytm / UPI | UPI = APIs between banks! scan → pay → bank APIs settle it |
| Spotify | Search API finds the song; play = stream API |
| Netflix | Recommendation API decides your homepage rows |
| Weather App | `GET api.weather.com/pune` → `{ "temp": 31 }` |

✎ You use 100s of APIs before breakfast — without knowing!

---

## 4. Resources — the "Things" ★

**Definition:** A **resource** is any *noun* your app cares about: Student, Teacher, Product, Employee, Order, Book, Customer, Course, Payment…

✎ If you can put "a / an / the" before it → it can be a resource.

In REST, a resource is a noun with its own URL:
- All students → `/students`
- ONE student, roll 99 → `/students/99`
- Their courses → `/students/99/courses`

**↯ Golden rule:** Nouns live in the URL, verbs live in the method — never `/getStudents`!
> URL says WHICH thing. Method says WHAT to do.

---

## 5. CRUD — Only 4 Things Ever Happen to Data ★

**Definition:** **CRUD** = **Create, Read, Update, Delete** — the only four operations that ever happen to stored data.

| CRUD | HTTP | SQL | Example |
|---|---|---|---|
| Create | `POST` | `INSERT` | `POST /students` — new admission |
| Read | `GET` | `SELECT` | `GET /students/99` |
| Update | `PUT` / `PATCH` | `UPDATE` | `PATCH /students/99` — fix marks |
| Delete | `DELETE` | `DELETE` | `DELETE /students/99` — TC issued! |

★ EVERY app — Instagram to ISRO — is just CRUD on resources, dressed up nicely.

**Memory trick:** *Create Posts — Read Gets — Update Puts — Delete Deletes*

### CRUD Everywhere

- **College:** C — admit a student · R — view student list · U — update marks · D — remove student
- **Library:** C — add new book · R — search catalogue · U — mark "issued" · D — remove torn book
- **Hospital:** C — register patient · R — read reports · U — update prescription · D — discharge record
- **Amazon:** C — place order · R — view orders · U — change address · D — cancel order
- **Instagram:** C — new post · R — scroll feed · U — edit caption · D — delete post

---

## 6. The Five HTTP Methods, Explained

### `GET` — "GIVE me data"

**Definition:** Fetch data. Never changes anything!

- **Analogy:** Reading a library book — look, don't write in it.
- **When:** Lists, details, search results, feeds.
- ✗ **Mistakes:** Sending a body with `GET`; using `GET` to change data (crawlers will click your "delete" links!)
- **Response:** `200 OK`

**Trick:** GET = GIVE

### `POST` — "PUSH something new"

**Definition:** Create a NEW resource. The server assigns the id.

- **Analogy:** Dropping a filled admission form in the college box.
- **When:** Signup, new order, new post, send message.
- URL used is the **collection**, e.g. `/students` — no id yet!
- ✗ **Mistakes:** POSTing to `/students/99` to create; forgetting `Content-Type`; expecting POST to be idempotent (2 clicks = 2 orders!)
- **Response:** `201 Created` (not 200!)

**Trick:** POST = POSTbox — new letter every time ✉

### `PUT` — "REPLACE the whole thing"

**Definition:** Replace the resource ENTIRELY with what you send.

- **Analogy:** Swapping the whole SIM card — old one is gone.
- **When:** "Save profile" forms that send every field.
- ✗ **Mistake:** Sending only 1 field with PUT — the rest become empty/null! (that job is PATCH's)
- **Idempotent ✓** — PUT the same body 10 times → same result. Safe to retry!

**Trick:** PUT = PUT a new one in its place ↺

### `PATCH` — "Fix just this PART"

**Definition:** Update SOME fields, leave the rest untouched.

- **Analogy:** Puncture repair — patch the hole, keep the tyre.
- **When:** Change password only, edit caption, mark as read.
- ✗ **Mistakes:** Using PUT when you mean PATCH (wipes fields!); assuming PATCH is always idempotent (usually yes, not guaranteed).

**↯ PUT vs PATCH:** PUT → repaint the whole wall. PATCH → touch up one spot.

**Trick:** PATCH = a patch on jeans ✂

### `DELETE` — "DESTROY it"

**Definition:** Remove the resource at that URL.

- **Analogy:** Shredding one file from the cabinet.
- **When:** Delete post, cancel booking, remove cart item.
- Usually **no body** at all.
- ✗ **Mistakes:** `DELETE /students` (boom — whole collection!); no auth check; returning 200 + body when 204 fits better.
- **Idempotent ✓** — delete twice → still gone. 2nd call just returns 404.

**Trick:** DELETE = DESTROY

---

## 7. Method Cheat Table ★

**safe** = never changes data · **idempotent** = repeat → same result

| Method | Safe? | Idempotent? | Body? | Success Code |
|---|---|---|---|---|
| `GET` | ✓ | ✓ | ✗ | 200 |
| `POST` | ✗ | ✗ | ✓ | 201 |
| `PUT` | ✗ | ✓ | ✓ | 200 |
| `PATCH` | ✗ | ~usually | ✓ | 200 |
| `DELETE` | ✗ | ✓ | rare | 204 |

**↯** idempotent = lift button — press 5× → same floor. POST = doorbell — press 5× → rings 5×!

---

## 8. The HTTP Request — Inside the Envelope

A request has 4 parts:

```mermaid
flowchart TD
    A["1. Start Line<br/>POST /students HTTP/1.1<br/><i>method + URL + version</i>"] --> B["2. Headers<br/>Host, Content-Type,<br/>Authorization, Cookie<br/><i>labels on the envelope</i>"]
    B --> C["3. Blank Line<br/><i>separates headers from body</i>"]
    C --> D["4. Body<br/>{ 'name':'Aman','course':'BCA' }<br/><i>the parcel inside</i>"]
```

★ GET & DELETE usually have NO body — just the envelope.

### Headers to Know ↯

| Header | Meaning |
|---|---|
| `Content-Type` | "My body is JSON" → `application/json` — how should the server read this? |
| `Accept` | "Please reply in JSON" — what the client wants back |
| `Authorization` | The ID card → `Bearer <JWT token>` — who is asking? |
| `Cookie` | Small notes the server gave you earlier, returned every time |
| `Host` | Which website on this server — one IP, many sites! |
| `User-Agent` | "I am Chrome on Windows" — who's knocking |

✗ **Classic bug:** POST JSON without `Content-Type` → `req.body` = undefined!

> Content-Type = what I'm SENDING · Accept = what I want BACK

---

## 9. The HTTP Response — The Reply Packet

1. **Status line** — `HTTP/1.1 200 OK` → version + code + reason
2. **Headers** — `Content-Type`, `Content-Length`, `Set-Cookie`, `Cache-Control`
3. **Body** — the actual data (JSON!)

**Why JSON? ★**
- JavaScript Object Notation — Node speaks it natively
- Human-readable, machine-parseable
- Lighter than XML: `<name>Riya</name>` → `"name":"Riya"`
- Every language can parse it

**Read a response in 3 looks:** 1. status code → did it work? 2. `Content-Type` → what came back? 3. body → the goods

---

## 10. Status Codes — The Server's Mood ★

**Rhyme:** 1 wait • 2 great • 3 relocate • 4 YOUR mistake • 5 server's fate

```mermaid
flowchart TD
    S["HTTP Status Codes"] --> A["1xx<br/>hold on…<br/>informational"]
    S --> B["2xx<br/>here you go ✓<br/>success"]
    S --> C["3xx<br/>go there →<br/>redirection"]
    S --> D["4xx<br/>YOUR fault<br/>client error"]
    S --> E["5xx<br/>MY fault<br/>server error"]
```

### 1xx — "hold on"
- **100 Continue** — "go ahead, send the rest." Used before big uploads.
- **101 Switching Protocols** — "let's change languages!" HTTP → WebSocket upgrade.

### 2xx — "here you go ✓"
- **200 OK** — done, here it is. `GET /students` → list.
- **201 Created** — new thing made! `POST /students` → new admission. ↯ POST should return 201, not 200!
- **202 Accepted** — got your order, cooking later. Queued jobs, email sending.
- **204 No Content** — done, nothing to show. Perfect after DELETE. Empty body!

**Trick:** 2xx = "too good" • 201 = 2-0-WON a new row!

### 3xx — "not here, go there →"
- **301 Moved Permanently** — shop shifted forever, update your address book.
- **302 Found** — temporarily at a different counter today.
- **304 Not Modified** — "your saved copy is still fresh, use it!"
- **307 Temporary Redirect** — like 302, but the method must stay the same.
- **308 Permanent Redirect** — like 301, method preserved.

**Trick:** 3 = flee! 301 permanent, 302 temporary

### 4xx — "YOU messed up"
- **400 Bad Request** — gibberish form. Broken JSON, missing fields.
- **401 Unauthorized** — no ID card! Not logged in. (really: UN-authenticated) ↯
- **403 Forbidden** — ID seen, still NO. Logged in ≠ allowed! ↯
- **404 Not Found** — no such room. `GET /studnets` (typo!). The celebrity ★
- **405 Method Not Allowed** — right door, wrong action.
- **406 Not Acceptable** — "you'll only Accept: XML? I only cook JSON."
- **408 Request Timeout** — you took too long; the waiter walked away.
- **409 Conflict** — two people booked seat 14A. Duplicate email!
- **410 Gone** — existed once, deleted forever. Stronger than 404.
- **415 Unsupported Media Type** — a file type the server can't chew.
- **422 Unprocessable Entity** — valid JSON, nonsense values: `"age": -5`.
- **429 Too Many Requests** — "slow down!!" You hammered the API.

**↯** 401 = who are you? 403 = I know you… still no! 404 = "4-Oh!-4got to check the URL"

### 5xx — "MY fault, sorry"
- **500 Internal Server Error** — kitchen on fire. An uncaught exception in your Node code. Check the server logs, ALWAYS.
- **501 Not Implemented** — "we don't serve that dish yet." Method not built.
- **502 Bad Gateway** — the middleman got garbage. Nginx is fine, but your Node app behind it crashed. ↯
- **503 Service Unavailable** — "closed for maintenance, come later." Overloaded or deploying.
- **504 Gateway Timeout** — the middleman waited… the kitchen never answered. Slow DB query behind a proxy.

**The 5-line summary ✎**
1xx → hold on
2xx → here you go ✓
3xx → go there →
4xx → you messed up
5xx → I messed up

**Trick:** 5xx = "5erver's fault" — the user can't fix it!

---

## 11. REST Naming Rules ★

| ✗ Wrong | ✓ Right |
|---|---|
| `GET /getStudents` | `GET /students` (the verb lives in the method!) |
| `POST /createNewStudent` | `POST /students` |
| `GET /student` (singular) | `GET /students` (always plural!) |
| `GET /Students_List` | `GET /students` (lowercase, kebab-case) |
| `POST /students/delete/99` | `DELETE /students/99` |
| `GET /students/99/get-courses` | `GET /students/99/courses` (nesting = ownership) |

**★ Golden rule:** URL = noun (plural) • method = verb

---

## 12. Versioning & Consistency

**Versioning — never break old apps!**
- `/api/v1/students` — old apps keep working
- `/api/v2/students` — new shape ships here

✎ Like textbook editions — old-edition students can still study!

**Safe & idempotent — recap ↯**
- Safe methods: `GET` (+ HEAD, OPTIONS) — window shopping: look, never touch
- Idempotent: `GET`, `PUT`, `DELETE` — elevator button
- NOT idempotent: `POST` — doorbell, every press counts!

✎ Networks retry failed requests — retrying POST can double-charge a payment!

**Consistency checklist ✎**
- [ ] Plural nouns everywhere: `/students` `/courses` `/orders`
- [ ] Lowercase + kebab-case: `/course-modules`
- [ ] Filters in query: `/students?year=2&sort=name`
- [ ] Version prefix: `/api/v1/…`
- [ ] Right status codes: 201, 204, 404, 422…
- [ ] Same JSON shape for every error

---

## 13. One Click, Full Journey ↯

```mermaid
flowchart LR
    A["1. Browser<br/>types URL, hits ⏎"] --> B["2. DNS<br/>phonebook → IP"]
    B --> C["3. Internet<br/>TCP + TLS, hops"]
    C --> D["4. API Gate<br/>auth + rate limit"]
    D --> E["5. Node Server<br/>Express matches route"]
    E --> F["6. Controller<br/>validates<br/>(traffic police)"]
    F --> G["7. Service<br/>business logic<br/>(chef)"]
    G --> H["8. Database<br/>SELECT * FROM students"]
    H --> I["9. JSON Returns<br/>200 OK + gzip"]
    I --> J["10. Browser Paints ✓<br/>JSON → HTML, ~200 ms!"]
```

**One breath:** browser → DNS → internet → API → Node → controller → service → DB → JSON → browser

**Errors by stop:**
- DNS fails → "server not found"
- Gate says no → 401 / 403 / 429
- Controller rejects → 400 / 422
- Service crashes → 500
- DB slow → 504

---

### ✎ Quick Recap

- An API is the safe middleman between a client and a database — you never touch the DB directly.
- Every feature in every app is really just **CRUD**, mapped to `GET`, `POST`, `PUT`/`PATCH`, `DELETE`.
- URLs should be **plural nouns**; methods carry the **verb**.
- Status codes tell you exactly what happened: `2xx` good, `3xx` moved, `4xx` your mistake, `5xx` server's mistake.
- Follow the naming + consistency rules so your API doesn't confuse the next dev (or you, in 3 months).

---
---

# Day 3 of API Learning — REST APIs & Browser Storage Explained My Way

## 1. What REST API Actually Does

Forget the textbook definition for a second. Here's the simplest way to picture it:

You never directly touch a database. There's always a **middleman** standing between your app's screen and the server's storage. That middleman is the API. It takes your request, forwards it to the backend, waits for a reply, and hands that reply back to you.

- **Frontend (Angular)** → what you see and click
- **Backend (Express/Node)** → the logic that decides what to do
- **Database (MySQL)** → where the actual data lives
- **API** → the connector between all three

## 2. Everything in the App Has an Address

Every single item — a resume, a user account, a template — gets its own unique URL. That URL is basically an ID card for that item.

`/api/documents/42` doesn't mean "documents" in general — it points to exactly ONE resume, the one numbered 42. It's like a house number on a street; there's only one house with that number.

## 3. Only 4 Actions Exist in REST

No matter how big or small the app is, you're limited to four core operations:

| HTTP Verb | Action | Everyday Example |
|---|---|---|
| GET | Fetch/read data | Open and view your resume |
| POST | Create new data | Add a brand-new resume |
| PUT | Update existing data | Edit a section of your resume |
| DELETE | Remove data | Delete a resume permanently |

Important trick to remember: **the URL doesn't change, only the verb does.**

`GET /documents/42` → reads resume 42
`DELETE /documents/42` → deletes resume 42

Same address, completely different outcome — just because of the verb used.

## 4. REST is Stateless — and That's a Feature, Not a Bug

Every time your app talks to the server, it has to prove who it is again (usually through a token). The server doesn't "remember" you from the last call.

Sounds inconvenient, but it's actually what makes apps scalable — any server in a cluster of thousands can handle your request because none of them need to keep your history in memory.

## 5. Data Travels as JSON

Requests and responses are packaged in **JSON** format — basically key-value pairs, easy for both frontend and backend to parse.

And every response carries a status code telling you what happened:

| Code | Meaning |
|---|---|
| 200 | Success, here's your data |
| 201 | Success, something new was created |
| 404 | Couldn't find what you asked for |
| 500 | Something broke on the server |

**Two terms to lock in:**
- **Resource** = the actual "thing" (a document, a user, a template)
- **Endpoint** = a specific URL + verb combo that does one job, e.g. `POST /api/documents`

## 6. Request Flow (Flowchart)

```
                 USER ACTION
             (clicks "Save Resume")
                      |
                      v
        ┌───────────────────────────┐
        │   FRONTEND (Angular)       │
        │  builds request + JSON    │
        └─────────────┬─────────────┘
                      |
              PUT /api/documents/42
                      |
                      v
        ┌───────────────────────────┐
        │  API LAYER (Express/Node)  │
        │  - checks auth token       │
        │  - validates request       │
        └─────────────┬─────────────┘
                      |
                 SQL query
                      |
                      v
        ┌───────────────────────────┐
        │      DATABASE (MySQL)      │
        │   reads / writes the row   │
        └─────────────┬─────────────┘
                      |
               result rows back
                      |
                      v
        ┌───────────────────────────┐
        │  API LAYER (Express/Node)  │
        │  wraps result in JSON +    │
        │  attaches status code      │
        └─────────────┬─────────────┘
                      |
              200 OK + JSON body
                      |
                      v
        ┌───────────────────────────┐
        │   FRONTEND (Angular)       │
        │   updates screen for user  │
        └───────────────────────────┘
```

## 7. Resources vs Actions

Not everything in an API is "stored data." Some endpoints just perform a job and hand back a result, without saving a permanent row.

**Stored resources (actual data that sits in the database):**
- User account
- Document (resume/cover letter)
- Section & section items
- Version history
- Template
- Application (job tracking)
- Share link

**Action-only endpoints (compute something, don't necessarily save it):**
- Auth (login/register)
- AI writing (bullets, summary, rewrite)
- ATS scoring
- Tailoring to a job description
- Export (PDF/DOCX generation)

## 8. Patterns That Make REST APIs Predictable

- **Nested URLs = ownership.** An item lives inside a section, which lives inside a document, so the path itself shows the hierarchy: `/documents/42/sections/3/items/7`
- **Actions still use POST**, even if there's no permanent save happening — because POST generally means "process this and give me a result."
- **Some endpoints skip authentication on purpose** — like a public share link. It uses a random unguessable code instead of a real internal ID, so nobody can just guess and access someone else's data by changing numbers.
- **The verb decides the action, the URL decides the target.** That's the whole logic of REST in one line.

## 9. Why Browser Storage Exists

A website often needs to remember something about you — that you're logged in, that you prefer dark mode, or the item you left in your cart. Instead of asking the server every single time, the browser itself can hold onto small pieces of data on your computer.

There are four main storage options a browser gives, and each one is meant for a different purpose. They differ in three things:

1. How much data they can hold
2. How long the data survives
3. Whether that data automatically gets sent to the server

## 10. Storage Decision Flowchart

```
                        START: Need to store some data?
                                    |
                                    v
                  Does the server need this data automatically
                  attached to every request (like login info)?
                                    |
                    ----------------------------------
                    |                                |
                   YES                               NO
                    |                                |
                    v                                v
              Use COOKIES                Does this data need to survive
          (auth tokens, sessions,        even after the browser is closed
           "remember me")                and reopened later?
                                                    |
                                  --------------------------------
                                  |                              |
                                 YES                              NO
                                  |                                |
                                  v                                v
                    Is it a large amount of data          Use SESSION STORAGE
                    or does it need to store objects,     (temporary form data,
                    files, or images (not just text)?     one-tab-only data)
                                  |
                  ------------------------------------
                  |                                  |
                 YES                                NO
                  |                                  |
                  v                                  v
           Use INDEXEDDB                    Use LOCAL STORAGE
     (offline documents, cached          (theme preference, saved
      files, large datasets)              settings, language choice)
```

## 11. Cookies

**Definition:** A cookie is a small piece of text data that the browser stores and automatically attaches to every request sent to the server it belongs to.

Think of it like a visitor badge at a mall entrance. Once you're given the badge, every shop you walk into can glance at it and instantly know it's the same visitor, without you introducing yourself again.

**Key properties:**
- Very small size, roughly 4 KB
- Automatically sent to the server with every single request
- Can have an expiry date (for example, it self-deletes after 7 days)
- Accessible by both the browser and the server

**Real-life best use:** Staying logged into Gmail. When you sign in once, a cookie stores your session token, and every time you revisit Gmail, that cookie is silently sent along, so the server instantly recognizes you instead of asking you to log in again.

## 12. Local Storage

**Definition:** Local Storage is a browser-only storage space that keeps data permanently, until it is manually cleared, either by the code or by the user.

Think of it as a drawer in your room. Whatever you place inside stays exactly where you left it, whether you check tomorrow, next week, or next month.

**Key properties:**
- Holds around 5 to 10 MB
- Never expires automatically
- Never gets sent to the server — it stays purely on the browser side
- Can only store plain text (strings); objects must be converted using `JSON.stringify()` before saving and `JSON.parse()` after reading

**Real-life best use:** YouTube remembering that you prefer dark mode. Once you switch the theme, YouTube saves that choice in Local Storage, so even after closing and reopening the browser weeks later, dark mode is still active.

## 13. Session Storage

**Definition:** Session Storage is browser storage that only lives for as long as that particular browser tab stays open. The moment the tab is closed, the data disappears completely.

Think of it as a classroom whiteboard. Notes can be written during the class, but the moment the class ends, everything gets wiped clean.

**Key properties:**
- Holds around 5 MB
- Exists only while the tab is open; closing the tab erases it instantly
- Never sent to the server
- Completely separate per tab — two tabs of the same website do not share this data

**Real-life best use:** Filling out a long form online. If you accidentally refresh the page, your entered data can still be recovered from Session Storage. But if you close the tab entirely, that data is gone for good.

## 14. IndexedDB

**Definition:** IndexedDB is a browser-based database capable of storing large amounts of structured data, including actual files, images, and complete objects, not just plain text.

Think of it as an entire library compared to Local Storage's single drawer. It's built to hold serious volumes of organized information.

**Key properties:**
- Can store hundreds of MB or more
- Can directly store objects, files, images, and videos, unlike the string-only limitation of Cookies or Local Storage
- Commonly used to make apps work offline

**Real-life best use:** Google Docs saving your document locally so that if your internet connection drops, your work isn't lost, and it automatically syncs once you're back online. Spotify similarly uses IndexedDB to store downloaded songs for offline playback.

## 15. Complete Comparison Table

| Feature | Cookies | Local Storage | Session Storage | IndexedDB |
|---|---|---|---|---|
| Storage size | ~4 KB | 5–10 MB | ~5 MB | Hundreds of MB+ |
| Sent to server automatically | Yes | No | No | No |
| Expires | Yes (can set expiry) | No, stays forever | Yes, on tab close | No |
| Can store large data | No | No | No | Yes |
| Can store objects/files directly | No, text only | No, strings only | No, strings only | Yes |
| Best real-life use | Login sessions, authentication | Theme, language, preferences | Temporary form data, per-tab data | Offline documents, cached media, large datasets |

## 16. Real Websites and What They Use

| Website | Storage Used | Reason |
|---|---|---|
| Gmail | Cookies | Keeps the user logged in across visits |
| YouTube | Local Storage | Remembers volume, dark mode, and preferences |
| Amazon | Cookies + Local Storage | Handles login, cart contents, and preferences |
| Google Docs | IndexedDB | Saves documents locally to survive offline |
| Spotify | IndexedDB | Caches downloaded songs for offline listening |
| Google Maps | IndexedDB | Stores offline map data for areas without internet |

---

## Quick Recap

**REST API basics:**
- REST API = middleman between frontend and backend/database
- Every resource has a unique address (URL)
- Only 4 actions exist: GET (read), POST (create), PUT (update), DELETE (remove)
- REST is stateless — server doesn't remember previous requests, so every request must identify itself
- Data travels as JSON, and every response carries a status code (200, 201, 404, 500)
- Resource = the "thing" itself; Endpoint = URL + verb combo that acts on it
- Nested URLs show ownership; non-CRUD actions still use POST; some endpoints (like share links) skip auth on purpose

**Browser storage basics:**
- **Cookies** → Visitor Badge → ~4 KB, auto-sent to server, expires, best for login/auth
- **Local Storage** → Bedroom Drawer → 5–10 MB, never expires, not sent to server, best for saved preferences
- **Session Storage** → Classroom Whiteboard → ~5 MB, wiped on tab close, not sent to server, best for temporary form data
- **IndexedDB** → Library → hundreds of MB+, stores objects/files directly, best for offline apps and large data

**One-line memory hooks:**
- Cookie = small + auto-sent + login
- Local Storage = permanent + preferences
- Session Storage = temporary + per-tab
- IndexedDB = huge + offline + real files
