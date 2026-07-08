# 🌐 What happens when you open a website in Browser?

### When You Type a URL and Press Enter

Most people think a website loads instantly. In reality, a series of precise technical steps happen in milliseconds — from DNS all the way to browser rendering. Here is the documented journey using `shorterloop.com` as a real example.

---

## 🗺️ Full Overview

```
You press Enter
      |
      ▼
┌─────────────────┐
│  DNS Resolution │  ← shorterloop.com → 199.36.158.100
└────────┬────────┘
         |
         ▼
┌──────────────────────┐
│ TCP Connection       │  ← 3-way handshake on port 443
│ + TLS Handshake      │  ← SSL encryption setup
└────────┬─────────────┘
         |
         ▼
┌──────────────────┐
│  HTTP Request    │  ← GET / HTTP/1.1
└────────┬─────────┘
         |
         ▼
┌──────────────────┐
│  HTTP Response   │  ← 200 OK / 304 Not Modified
└────────┬─────────┘
         |
         ▼
┌──────────────────┐
│ Browser Renders  │  ← HTML → CSS → JS → Paint
└──────────────────┘
```

---

## Step 1: DNS Resolution 🔍

When you type a URL in the browser, it first needs the **IP address** — because the internet understands IP addresses, not domain names.

### How DNS Resolution Works

```
Check Browser Cache
      |
      ├── HIT  → IP found, move ahead
      |
      └── MISS → Send query to DNS Resolver
                        |
                        ▼
              ┌─────────────────────┐
              │   DNS Resolver      │
              └────────┬────────────┘
                       |
                       ▼
              ┌─────────────────────┐
              │   Root DNS Server   │
              │   (knows about .com)│
              └────────┬────────────┘
                       |
                       ▼
              ┌─────────────────────┐
              │  TLD DNS Server     │
              │  (has the domain's  │
              │   record)           │
              └────────┬────────────┘
                       |
                       ▼
              IP Address found ✅
```

### Real CMD Output (`nslookup shorterloop.com`)

```
Server:   reliance.reliance
Address:  2405:201:680d:d2be::c0a8:1d01

Non-authoritative answer:
Name:     shorterloop.com
Address:  199.36.158.100
```

**"Non-authoritative answer"** means this answer came from a DNS cache, not directly from the website's own DNS server.

---

## Step 2: TCP Connection + TLS Handshake 🔒

Once the IP is found, the browser establishes a **connection** with the server. Since HTTPS is used, it connects on port **443**.

### TCP 3-Way Handshake

```
Browser                          Server
   |                                |
   |──────────── SYN ─────────────>|
   |        "Hey, can we talk?"     |
   |                                |
   |<─────────── SYN-ACK ──────────|
   |        "Sure, I am ready!"     |
   |                                |
   |──────────── ACK ─────────────>|
   |        "Perfect, let us begin" |
   |                                |
   |     [Connection Established]   |
```

### TLS Handshake (Encryption Setup)

```
Browser                          Server
   |                                |
   |──── ClientHello ──────────────>|
   |  (list of encryption methods)  |
   |                                |
   |<─── ServerHello + Certificate ─|
   |  (server sends its SSL cert)   |
   |                                |
   |  Browser verifies certificate  |
   |  (is it from a trusted CA?)    |
   |                                |
   |──── Key Exchange ─────────────>|
   |                                |
   |<──────── Finished ─────────────|
   |                                |
   |    [Encrypted Channel Ready]   |
   |    🔒 All data now encrypted   |
```

After this, all data transferred is **encrypted**. Even if someone intercepts it, they only see gibberish.

---

## Step 3: HTTP Request 📤

With a secure connection established, the browser sends a request:

```
GET / HTTP/1.1
Host: shorterloop.com
Accept: text/html,application/xhtml+xml
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Cache-Control: max-age=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64)
```

- **GET /** → Request the homepage
- **Host** → Which website (one server can host many sites)
- **Cache-Control** → Do we need fresh content or is cache okay?
- **User-Agent** → Browser identifies itself to the server

---

## Step 4: HTTP Response 📥

The server processes the request and sends back a response.

### Common Status Codes

| Code | Status | Meaning |
|---|---|---|
| 200 | OK | Resource found and delivered |
| 301 | Moved Permanently | URL changed, redirecting |
| 304 | Not Modified | Use your cached version |
| 404 | Not Found | Page does not exist |
| 500 | Internal Error | Something broke on server side |

### Real Response Example

```
HTTP/1.1 304 Not Modified
```

**304 means:** The browser already had a cached copy. The server confirmed nothing has changed — use the cached file. This saves bandwidth and makes the page load faster.

---

## Step 5: Browser Rendering 🎨

Once the HTML is received, the browser **renders it on screen**:

```
HTML File Received
      |
      ▼
┌─────────────────────┐
│   HTML Parsing      │  → Builds the DOM Tree
└────────┬────────────┘
         |
         ├──── CSS file found → sends GET request
         |     → Builds CSSOM Tree
         |
         ├──── JS file found → sends GET request
         |     → JavaScript executes
         |
         ├──── Images/Fonts found → sends GET requests
         |
         ▼
┌─────────────────────┐
│  DOM + CSSOM merge  │
│  = Render Tree      │
└────────┬────────────┘
         |
         ▼
┌─────────────────────┐
│  Layout / Reflow    │  → Calculate position of elements
└────────┬────────────┘
         |
         ▼
┌─────────────────────┐
│  Paint & Composite  │  → Display pixels on screen
└─────────────────────┘
         |
         ▼
    🖥️ Website fully loaded!
```

---

## Step 6: Real Network Requests Example 📊

Data captured from Chrome DevTools Network Tab:

| File | Code | Type | Size / Time |
|---|---|---|---|
| / (main HTML) | 304 | document | cached |
| Google Analytics script | 200 | script | 180 kB/378ms |
| Web fonts (woff2) | 200 | font | memory cache |
| Images/gifs | 200 | image | memory cache |
| Logo (svg) | 200 | svg+xml | memory cache |
| favicon | 200 | png | disk cache |
| Analytics collect call | 204 | fetch | 0.0kB/315ms |

**Total:** 68 requests, 180kB transferred, loaded in 1.3s

### Cache Types Explained

```
Memory Cache  → Stored in RAM, ultra fast (0ms)
Disk Cache    → Stored on hard drive, fast (4ms)
No Cache      → Fresh download from server, slower
```

---

## 📈 Timeline — 0ms to 1300ms

```
0ms        200ms      400ms      600ms      800ms     1000ms    1300ms
|----------|----------|----------|----------|----------|---------|
[==DNS==]  |          |          |          |          |
    [=TCP+TLS=]       |          |          |          |
           [===HTML===]          |          |          |
                  [===CSS+Fonts==]          |          |
                           [=====JS========]          |
                                    [=====Images======]
                                                [===Analytics===]
                                                          |
                                              DOMContentLoaded: 665ms
                                                         Load: 1.30s ✅
```

---

## 🧠 Key Concepts Summary

| Concept | Simple Explanation |
|---|---|
| DNS | Phone book of internet — name to IP |
| TCP Handshake | Establishing connection — SYN, SYN-ACK, ACK |
| TLS/SSL | Locking the data — encryption |
| HTTP GET | Requesting a file from the server |
| 200 OK | File found and delivered |
| 304 Not Modified | Use cached version, nothing changed |
| DOM | HTML as a tree structure in browser |
| CSSOM | CSS as a tree structure |
| Render Tree | DOM + CSSOM = what you see on screen |
| Memory Cache | Resources stored in RAM (0ms) |
| Disk Cache | Resources stored on HDD (4ms) |

---

## 🔁 The Complete Journey in One View

```
Type URL and press Enter
       ↓
DNS Lookup → IP address found
       ↓
TCP 3-way handshake (connection established)
       ↓
TLS handshake (encrypted channel created)
       ↓
HTTP GET / request sent
       ↓
Server responds → 200 OK or 304 Not Modified
       ↓
Browser builds DOM + CSSOM + executes JavaScript
       ↓
Page fully loaded ✅
```

---

*Notes by Unishka Bisht — BCA 3rd Sem, Amrapali University, Haldwani*
*Real data captured using Chrome DevTools (Network Tab) and Windows CMD (nslookup)*
