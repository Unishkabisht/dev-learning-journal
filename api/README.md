# 📘 Learning API

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

*Notes by Unishka Bisht — BCA 3rd Sem, Amrapali University, Haldwani*
