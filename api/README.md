# API, HTTP & REST Notes

---

# Day 1 – API Fundamentals

## What is an API?

Definition: An API (Application Programming Interface) is a set of rules that allows one piece of software to talk to another. It defines how a request should be made and what response will be returned. The client never accesses the server's database directly; the API sits between them and handles the communication.

Real-life example: When you use a weather app, the app does not calculate weather itself. It sends a request to a weather API, the API asks the server for the data, and the server sends back the temperature and forecast, which the API delivers to the app.

Roles involved:

| Role | Description |
|---|---|
| Client | The one who makes the request (browser, app, JavaScript code) |
| API | The interface that carries the request and the response |
| Server | The one who processes the request and prepares the response |
| Database | Where the actual data is stored |

---

## Client–Server Architecture

Definition: Client-server architecture is a model where the client sends requests and the server processes them and sends back responses. The client always initiates the communication; the server only replies.

Rules:
- The client always speaks first.
- Every request gets exactly one response.
- HTTP is stateless — the server does not remember previous requests. Each request must carry its own identity (through a cookie or token) if the app needs to recognize the same user again.

Real-life example: Logging into an email account. Each time you open a new page in Gmail, your browser sends your session token again, because the server does not remember you from the last request on its own.

```mermaid
flowchart LR
    A[Client - browser or app] -->|sends request| B[Server]
    B -->|sends response| A
```

---

## HTTP Request & Response

Definition: HTTP (HyperText Transfer Protocol) is the protocol that defines how a client and a server exchange messages. Every interaction consists of one request from the client and one response from the server.

### Structure of a Request

| Part | Description |
|---|---|
| Method | The action to be performed (GET, POST, PUT, PATCH, DELETE) |
| URL | The address of the resource being requested |
| Headers | Extra information about the request, such as content type or authorization |
| Body | The data being sent (used with POST, PUT, PATCH; usually absent in GET) |

### Structure of a Response

| Part | Description |
|---|---|
| Status Code | A three-digit number indicating success or failure |
| Headers | Metadata about the response |
| Body | The actual data returned by the server |

Real-life example: Submitting a login form sends a POST request with an email and password in the body. The server replies with a status code (200 if successful, 401 if the credentials are wrong) and a body containing the response data.

---

## JSON

Definition: JSON (JavaScript Object Notation) is a lightweight, text-based format used to exchange data between a client and a server. It resembles a JavaScript object but is transmitted as plain text.

```json
{
  "name": "iPhone 16 Pro",
  "price": 134900,
  "inStock": true
}
```

| Method | Purpose |
|---|---|
| response.json() | Converts JSON text received from the server into a JavaScript object |
| JSON.stringify() | Converts a JavaScript object into JSON text so it can be sent to the server |

Real-life example: When a shopping app displays a product list, the server sends that list as JSON text. The app uses response.json() to turn it into an object it can actually read and display.

---

## HTTP Methods (GET, POST, PUT, PATCH, DELETE)

Definition: HTTP methods are verbs that describe the action to be performed on a resource identified by a URL.

| Method | Action | Definition |
|---|---|---|
| GET | Read | Requests existing data without changing anything |
| POST | Create | Asks the server to create a new piece of data |
| PUT | Replace | Asks the server to replace an existing resource entirely |
| PATCH | Update | Asks the server to update only part of a resource |
| DELETE | Remove | Asks the server to delete a resource |

Real-life example: On an online store — viewing a product list is GET, placing a new order is POST, editing your entire saved address is PUT, changing only your phone number in that address is PATCH, and removing an item from the cart is DELETE.

---

## GET vs POST

Definition: GET sends data as part of the URL (query parameters); POST sends data hidden inside the request body.

| | GET | POST |
|---|---|---|
| Where data goes | In the URL, for example ?search=iphone16 | In the request body |
| Use case | Fetching or reading data | Creating new data |
| Safe to repeat | Yes | No |

Explanation: An action is safe to repeat if doing it multiple times produces the same result as doing it once. GET is safe because reading the same data again does not change anything. POST is not safe because if a signup form is submitted and the page is refreshed right after, the browser may resend that POST, creating the account twice.

---

## HTTP Status Codes (Basics)

Definition: A status code is a three-digit number returned in every HTTP response that tells the client the outcome of its request. Status codes are grouped into five families by their first digit.

| Family | Meaning |
|---|---|
| 1xx | Informational — request received, still processing |
| 2xx | Success — request completed successfully |
| 3xx | Redirection — resource has moved |
| 4xx | Client Error — something is wrong with the request sent |
| 5xx | Server Error — something broke on the server |

Common codes:

| Code | Name | Meaning |
|---|---|---|
| 200 | OK | Request succeeded |
| 201 | Created | A new resource was created |
| 204 | No Content | Request succeeded, nothing to return |
| 400 | Bad Request | The request was malformed or missing data |
| 401 | Unauthorized | Not logged in / no valid credentials |
| 403 | Forbidden | Identified, but not permitted |
| 404 | Not Found | The resource does not exist |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Something broke on the server |

Rule: The status code should always be checked first. A response body can look like valid data even when the request actually failed, but the status code tells the real outcome.

---

## REST URL Design

Definition: REST is a design style in which the URL identifies what resource (noun) is being worked with, and the HTTP method identifies what action (verb) is being performed on it.

```
Correct:
GET    /mobiles          read all mobiles
GET    /mobiles/5        read mobile with id 5
POST   /mobiles          add a new mobile
PUT    /mobiles/5        replace mobile 5 entirely
PATCH  /mobiles/5        update part of mobile 5
DELETE /mobiles/5        delete mobile 5

Incorrect (verb baked into the URL):
GET /getAllMobiles
POST /createNewMobile
POST /deleteMobile5
```

Real-life example: A well-designed college API uses GET /students/99 to view a student, not GET /getStudent99. The URL names the resource; the method decides the action.

---

## fetch() API (.then(), async/await, sending requests, parsing responses)

Definition: fetch() is a built-in JavaScript function used to make HTTP requests from the browser to a server.

### Style 1: .then() chaining

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

### Style 2: async/await

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

### Why fetch is awaited twice

Both fetch() and .json() are asynchronous — each takes time and returns a Promise, so each needs its own await.
1. First await — waits for the request to reach the server and the response to start arriving.
2. Second await — waits for the response body to be fully read and converted from JSON text into a JavaScript object.

### Sending data with fetch()

To send data, a second argument is passed to fetch() containing method, headers, and body.

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

| Field | Meaning |
|---|---|
| method | Which HTTP verb to use |
| headers | Tells the server what kind of data is being sent |
| body | The actual data, converted to JSON text using JSON.stringify() |

---

## Error Handling with fetch()

Definition: fetch() only rejects (throws an error) on a network failure, such as no internet connection or an unreachable server. It does not throw an error for a 404 or 500 response — the server responding with an error status is still treated as a technically successful fetch. This must be checked manually.

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

res.ok is true for status codes 200 to 299, and false for anything else.

---

## Authentication Basics (API Keys, Bearer Tokens, .env)

Definition: Authentication is the process of proving identity to a server before it allows access to protected data.

### API Keys

A unique string identifying who is making the request, usually sent as a header.

```js
fetch("https://api.example.com/data", {
  headers: {
    "x-api-key": "your-secret-key-here"
  }
});
```

### Bearer Tokens

A token sent in the Authorization header, proving that the client has already logged in. "Bearer" means whoever holds this token is trusted.

```js
fetch("https://resumeflow-api.example.com/profile", {
  headers: {
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIs..."
  }
});
```

### Keeping keys in .env

Definition: A .env file stores secret values, such as keys, passwords, and tokens, outside the actual code so they are not accidentally exposed.

```
# .env
API_KEY=abc123secretkey
```

```js
// Used only on the backend (Node.js)
const apiKey = process.env.API_KEY;
```

Rule: Secret keys should never go into frontend code or into git.
- Never in frontend code — anything in browser JavaScript is visible to anyone who opens DevTools.
- Never in git — if a key is committed and pushed, it remains in commit history forever even after deletion. .env should always be added to .gitignore.

---

## Introduction to Express (Creating Basic APIs)

Definition: Express is a Node.js framework used to build servers — this is the code that receives the fetch requests sent from the client.

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

## Live API Demo (PokeAPI)

Demonstration of a real, public API used directly in the browser console — a GET request, checking res.ok, then parsing with .json().

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

Console output:
```
pikachu 4 60
```

---

# Day 2 – REST APIs & Backend

## REST API Architecture & Request Flow

Definition: REST (Representational State Transfer) is an architectural style for designing APIs where every piece of data is treated as a resource with its own URL, and standard HTTP methods are used to act on it.

Request flow: Client sends a request through the API, the API routes it to the Server, the Server queries the Database, and the data flows back up as a JSON response.

```mermaid
flowchart LR
    Client --> API --> Server --> Database
    Database -.JSON response.-> Server -.-> API -.-> Client
```

Real-life example: Opening Instagram's feed sends a request through the Feed API, which asks the server, which pulls the posts from the database, and the same posts return as JSON to render on screen. This same round trip happens for every action taken in any app.

---

## Resources & CRUD Operations

Definition: A resource is any noun the application deals with, such as Student, Product, Order, or Document. In REST, every resource has its own URL.

- All students: /students
- One student, roll 99: /students/99
- Their courses (nested resource): /students/99/courses

Definition of CRUD: CRUD stands for Create, Read, Update, Delete — the only four operations that ever happen to stored data.

| CRUD | HTTP | SQL | Example |
|---|---|---|---|
| Create | POST | INSERT | POST /students — new admission |
| Read | GET | SELECT | GET /students/99 |
| Update | PUT / PATCH | UPDATE | PATCH /students/99 — fix marks |
| Delete | DELETE | DELETE | DELETE /students/99 — record removed |

Real-life example: An Amazon order goes through the same four operations — placing an order (Create), viewing past orders (Read), changing the delivery address (Update), and cancelling the order (Delete).

---

## Deep Dive into HTTP Methods (Safe & Idempotent)

Definition: A method is safe if it never changes data on the server. A method is idempotent if calling it multiple times produces the same result as calling it once.

### GET
Definition: Fetches data, never changes anything.
Real-life example: Reading a library book — you look at it, you do not write in it.
Common mistakes: sending a body with GET; using GET to change data.
Response code: 200 OK.

### POST
Definition: Creates a new resource; the server assigns the id.
Real-life example: Dropping a filled admission form into a college's submission box — every form dropped creates a new admission record.
Common mistakes: sending a POST to a URL with an id already in it (e.g. /students/99) to create a record; forgetting Content-Type; assuming POST is safe to repeat.
Response code: 201 Created.

### PUT
Definition: Replaces the resource entirely with what is sent.
Real-life example: Swapping an old SIM card for a new one — the old one is completely gone.
Common mistake: sending only one field with PUT, which causes every other field to become empty or null.
Idempotent: yes — sending the same body ten times gives the same result.

### PATCH
Definition: Updates only some fields, leaving the rest untouched.
Real-life example: Repairing a puncture in a tyre — only the hole is patched, the rest of the tyre stays as it was.
Common mistakes: using PUT when PATCH was meant, which wipes other fields; assuming PATCH is always idempotent.

### DELETE
Definition: Removes the resource at that URL.
Real-life example: Shredding one specific file from a filing cabinet.
Common mistakes: calling DELETE on a collection URL such as /students instead of a specific id, which deletes everything; missing an authorization check.
Idempotent: yes — deleting twice still leaves it deleted; the second call simply returns 404.

### Method Cheat Table

| Method | Safe | Idempotent | Body | Success Code |
|---|---|---|---|---|
| GET | Yes | Yes | No | 200 |
| POST | No | No | Yes | 201 |
| PUT | No | Yes | Yes | 200 |
| PATCH | No | Usually | Yes | 200 |
| DELETE | No | Yes | Rarely | 204 |

---

## HTTP Headers

Definition: Headers are key-value pairs sent along with a request or response that carry metadata — extra information that is not part of the main data itself.

| Header | Meaning |
|---|---|
| Content-Type | Tells the server the format of the data being sent, for example application/json |
| Accept | Tells the server what format the client wants back |
| Authorization | Carries identity information, for example Bearer <JWT token> |
| Cookie | Small pieces of data the server gave earlier, sent back with every request |
| Host | Identifies which website is being requested on a server hosting multiple sites |
| User-Agent | Identifies the client software making the request, for example a browser and operating system |

Real-life example: A single POST request without a Content-Type header is a common cause of bugs — the server cannot tell that the body is JSON, so req.body comes back as undefined on the server side.

Rule: Content-Type describes what is being sent. Accept describes what is wanted back.

---

## HTTP Status Codes (Detailed)

Definition: Beyond the basic five families, specific codes communicate precise outcomes for a request.

### 1xx and 2xx

| Code | Meaning |
|---|---|
| 100 Continue | Server has received the request headers, client should proceed to send the body |
| 101 Switching Protocols | The connection is being upgraded, for example from HTTP to WebSocket |
| 200 OK | Request succeeded and data is returned |
| 201 Created | A new resource was successfully created |
| 202 Accepted | The request was received but processing will happen later |
| 204 No Content | Request succeeded, no data to return, commonly used after DELETE |

### 3xx

| Code | Meaning |
|---|---|
| 301 Moved Permanently | The resource has moved to a new URL permanently |
| 302 Found | The resource is temporarily available at a different URL |
| 304 Not Modified | The client's cached copy is still valid, no new data sent |
| 307 Temporary Redirect | Same as 302, but the original method must be reused |
| 308 Permanent Redirect | Same as 301, but the original method must be reused |

### 4xx

| Code | Meaning |
|---|---|
| 400 Bad Request | The request was malformed or missing required data |
| 401 Unauthorized | The client is not authenticated |
| 403 Forbidden | The client is authenticated but not permitted to perform this action |
| 404 Not Found | The requested resource does not exist |
| 405 Method Not Allowed | The URL exists but does not support this method |
| 406 Not Acceptable | The server cannot produce a response matching the Accept header |
| 408 Request Timeout | The client took too long to send the request |
| 409 Conflict | The request conflicts with the current state, such as a duplicate entry |
| 410 Gone | The resource existed before but has been permanently removed |
| 415 Unsupported Media Type | The server does not support the format of the request body |
| 422 Unprocessable Entity | The request is well-formed but contains invalid data |
| 429 Too Many Requests | The client has sent too many requests in a given time |

### 5xx

| Code | Meaning |
|---|---|
| 500 Internal Server Error | An unhandled error occurred in the server's code |
| 501 Not Implemented | The server does not support the functionality required |
| 502 Bad Gateway | A server acting as a gateway received an invalid response from another server |
| 503 Service Unavailable | The server is temporarily overloaded or under maintenance |
| 504 Gateway Timeout | A gateway server did not receive a timely response from an upstream server |

Real-life example: A 401 means you never showed an ID card at all (not logged in). A 403 means you showed the ID card, the server recognized you, and still said no because you don't have permission. This is a common interview distinction.

---

## REST Naming Conventions & API Versioning

Definition: Naming conventions are the agreed rules for writing URLs consistently across an API, so that any resource's address is predictable.

| Incorrect | Correct |
|---|---|
| GET /getStudents | GET /students |
| POST /createNewStudent | POST /students |
| GET /student (singular) | GET /students (plural) |
| GET /Students_List | GET /students (lowercase, kebab-case) |
| POST /students/delete/99 | DELETE /students/99 |
| GET /students/99/get-courses | GET /students/99/courses |

Rule: URLs should be nouns, written in plural, lowercase. Methods should carry the verb.

Definition of API Versioning: Versioning allows the API's structure to change over time without breaking applications that were built against an older version.

```
/api/v1/students   old applications keep working against this version
/api/v2/students    new response format ships under this version
```

Real-life example: This is similar to different editions of the same textbook — students studying from the old edition can continue to use it while a new edition exists for new students.

---

## API Design Best Practices (Consistency)

Definition: Consistency means every part of an API follows the same rules, so a developer using it can predict behavior without checking documentation for every single endpoint.

Checklist:
- Plural nouns everywhere: /students, /courses, /orders
- Lowercase and kebab-case: /course-modules
- Filters passed in the query string: /students?year=2&sort=name
- Version prefix included: /api/v1/...
- Correct status codes used consistently: 201 for creation, 204 for deletion, 404 for missing resources, 422 for invalid data
- The same JSON error shape returned for every failure, so client code can handle errors in one place

---

## Complete Request Lifecycle (Browser → DNS → API → Server → Database → Response)

Definition: The request lifecycle describes every stage a single request passes through, from being typed in the browser to the final response being rendered.

```mermaid
flowchart LR
    A[Browser - user enters URL] --> B[DNS - domain resolved to IP]
    B --> C[Internet - TCP and TLS connection established]
    C --> D[API Gateway - authentication and rate limiting]
    D --> E[Node Server - Express matches the route]
    E --> F[Controller - validates the request]
    F --> G[Service - business logic runs]
    G --> H[Database - data is read or written]
    H --> I[JSON Response - sent back with a status code]
    I --> J[Browser renders the result]
```

Real-life example: Typing a URL and pressing enter triggers all of these stages within roughly 200 milliseconds for a typical API call — DNS lookup, the TCP/TLS handshake, the request reaching the server, the server validating and processing it, the database being queried, and the JSON response being parsed and displayed.

Where failures happen at each stage:
- DNS fails: "server not found"
- API gateway rejects: 401, 403, or 429
- Controller rejects invalid input: 400 or 422
- Service crashes: 500
- Database is slow behind a proxy: 504

---

# Day 3 – Advanced REST & Browser Storage

## REST Concepts Revision (Resources, Endpoints, Stateless APIs)

Definition of Resource: A resource is any noun the application manages — a Student, a Document, an Order — and it is represented by its own URL.

Definition of Endpoint: An endpoint is one specific URL combined with one specific HTTP method, representing exactly one action on a resource, for example POST /api/documents ("create a new document").

Definition of Stateless API: A stateless API means the server does not retain any memory of previous requests from the same client. Every request must carry all the information the server needs to process it, typically through a token or cookie.

Real-life example: Each time a mobile app requests data, it resends its authentication token, because the server treats every request as if it is meeting the client for the first time.

---

## Resources vs Action Endpoints

Definition: Most REST endpoints correspond to actual stored data (resources). Some endpoints instead represent an action or computation that produces a result without necessarily being tied to one saved row of data — these are called action endpoints.

Example from an AI Resume Builder API:

| Type | Example | Description |
|---|---|---|
| Resource | GET /api/documents/:id | Returns a stored, saved document |
| Resource | POST /api/documents | Creates and stores a new document |
| Action endpoint | POST /api/ai/bullets | Generates bullet point text using AI, not a saved row |
| Action endpoint | POST /api/ats/check | Scores a document and returns issues, a computed result |
| Action endpoint | POST /api/exports/pdf | Renders a PDF file and returns its file URL |

Real-life example: Requesting a bank statement (a stored resource) is different from asking the bank to calculate your loan eligibility (an action) — the second one produces a computed result rather than returning something already saved.

Rule: Non-CRUD work is modeled as a POST to a verb-like resource name, because HTTP has no dedicated method for "compute" or "generate."

---

## Nested REST URLs

Definition: A nested URL places one resource inside another in the path, to show that the inner resource belongs to and only exists within the outer resource.

```
GET    /students/99/courses                      courses belonging to student 99
POST   /api/documents/:id/sections                add a section to document :id
PATCH  /api/documents/:id/sections/:sectionId     edit a specific section
DELETE /api/documents/:id/sections/:sectionId     remove a specific section
POST   /api/documents/:id/sections/:sectionId/items   add an item to a section
```

Real-life example: A section inside a resume document does not exist on its own — it only makes sense as part of that particular document, so its URL is nested under the document's URL.

Note: In practice, many applications save an entire resource in one PUT call (for example, PUT /api/documents/:id saving a whole document at once) rather than editing each nested piece separately over the network. Both approaches are valid; nested routes matter most when fine-grained, field-by-field autosave behavior is needed.

One endpoint is often deliberately made public and unnested from authentication, such as GET /api/share/:slug for a shared link, and it typically uses an unguessable random slug instead of the actual resource id, so records cannot be guessed or enumerated.

---

## Browser Storage

Definition: Browser storage refers to the different mechanisms a browser provides to save small amounts of data directly on the user's own computer, rather than on the server.

```mermaid
flowchart TD
    Browser --> Cookies
    Browser --> LocalStorage[Local Storage]
    Browser --> SessionStorage[Session Storage]
    Browser --> IndexedDB
```

### Cookies

Definition: A cookie is a small piece of data the server sends to the browser, which the browser then automatically attaches to every future request to that same server.

Real-life example: Logging into Gmail saves a cookie such as user=dinesh, token=abc123. On every later visit, the browser automatically sends that cookie back, and the server recognizes the same user without requiring login again.

Characteristics: about 4 KB in size, sent to the server automatically with every request, and can be set to expire after a period of time, for example seven days.

Common uses: login sessions, "remember me" functionality, shopping carts, language preference.

### Local Storage

Definition: Local Storage saves data in the browser that stays there indefinitely, until it is explicitly removed by code or the user.

Real-life example: Selecting dark mode on a website saves theme=dark in Local Storage. Returning to the site any time later, even after closing the browser completely, the site reads theme=dark and dark mode is restored automatically.

```js
localStorage.setItem("theme", "dark");
localStorage.getItem("theme");
localStorage.removeItem("theme");
```

Characteristics: around 5 to 10 MB in size, never expires on its own, not sent to the server, and only accessible by scripts running in the browser.

### Session Storage

Definition: Session Storage saves data only for the duration that a browser tab remains open. It is cleared automatically the moment that tab is closed.

Real-life example: Filling out a long online form, the site can hold the entered values temporarily. An accidental page refresh keeps the data, but closing the tab clears it completely. Each browser tab also keeps its own separate copy — searching "laptop" in one tab and "shoes" in another tab on the same site does not mix the two.

```js
sessionStorage.setItem("name", "Unishka");
sessionStorage.getItem("name");
```

Characteristics: around 5 MB in size, exists only while the tab stays open, not sent to the server, and kept separate per tab.

### IndexedDB

Definition: IndexedDB is a browser database capable of storing large amounts of structured data, including whole objects, files, and images, directly in the browser.

Real-life example: Google Docs stores a document in IndexedDB so that editing can continue even if the internet connection drops, and Spotify stores downloaded songs in IndexedDB so they can play back offline.

Characteristics: capacity of hundreds of MB or more, and unlike the other storage types it can store whole objects, files, and binary data directly rather than only text strings.

---

## Browser Storage Comparison

| Feature | Cookies | Local Storage | Session Storage | IndexedDB |
|---|---|---|---|---|
| Size | 4 KB | 5 to 10 MB | 5 MB | Hundreds of MB or more |
| Sent to server | Yes | No | No | No |
| Expires | Yes | No | On tab close | No |
| Suitable for large data | No | No | No | Yes |
| Stores objects directly | No | No, strings only | No, strings only | Yes |
| Best use | Login, authentication | Theme, preferences | Temporary form data | Offline data, large files |

Note: Local Storage and Session Storage can only store strings. To save an object, it must first be converted using JSON.stringify() before saving, and converted back using JSON.parse() after reading. IndexedDB does not have this limitation and can store objects directly.

---

## Real-World Browser Storage Use Cases

| Website | Storage used | Reason |
|---|---|---|
| Gmail | Cookies | Keeps the user logged in across requests |
| YouTube | Local Storage | Remembers dark mode, volume level, preferences |
| Amazon | Cookies and Local Storage | Handles login, shopping cart, and saved preferences |
| Google Docs | IndexedDB | Saves documents locally so editing works offline |
| Spotify | IndexedDB | Caches downloaded songs for offline playback |
| Google Maps | IndexedDB | Stores offline map data, which is too large for cookies or Local Storage |

Common interview questions on this topic:
- Which storage type is sent to the server on every request: Cookies.
- Which storage types survive a full browser restart: Local Storage and IndexedDB.
- Which storage type is deleted when the tab closes: Session Storage.
- Which storage type is best suited for offline applications and large data: IndexedDB.
- Can Local Storage store objects directly: No, it can only store strings; objects must be converted with JSON.stringify() and JSON.parse().
