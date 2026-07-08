# HTML — Complete Notes

HyperText Markup Language ka use webpage ka **structure/skeleton** banane ke liye hota hai. Ye programming language nahi, **markup language** hai — matlab ye content ko *tags* ke through define karti hai ki browser ko kya kaise dikhana hai.

---

## 1. Basic Structure

Har HTML document ka ek fixed skeleton hota hai:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <!-- Visible content yahan aata hai -->
</body>
</html>
```

| Part | Kaam |
|---|---|
| `<!DOCTYPE html>` | Browser ko batata hai ye HTML5 document hai |
| `<html>` | Root element, poora page isi ke andar hota hai |
| `<head>` | Metadata — jo user ko directly dikhta nahi (title, links, meta tags) |
| `<meta charset>` | Character encoding set karta hai (UTF-8 = special characters support) |
| `<meta viewport>` | Mobile responsive banane ke liye zaroori |
| `<body>` | Actual visible content |

---

## 2. Tag kya hota hai?

Tag ek keyword hota hai angle brackets `< >` mein, jo browser ko batata hai ki content ka **type/role** kya hai.

- **Opening tag:** `<p>`
- **Closing tag:** `</p>`
- **Content:** dono ke beech mein
- **Element:** opening + content + closing tag mil ke ek element banta hai

```html
<p>Ye ek paragraph hai</p>
```

**Void/self-closing tags** — inka closing tag nahi hota (content nahi hota inke andar):
```html
<img src="pic.jpg" alt="description">
<br>
<hr>
<input type="text">
```

### Attributes
Tag ko extra info dene ke liye — opening tag ke andar `name="value"` format mein:
```html
<a href="https://example.com" target="_blank">Link</a>
```

---

## 3. Commonly Used Tags

### Text & Headings
```html
<h1>Sabse bada heading</h1>
<h2>...</h2>
...
<h6>Sabse chota heading</h6>

<p>Paragraph text</p>
<span>Inline text ke liye</span>
<strong>Bold + important meaning</strong>
<em>Italic + emphasis</em>
<br>  <!-- line break -->
<hr>  <!-- horizontal line -->
```

> ⚠️ **Rule:** Ek page mein sirf **ek `<h1>`** use karo (main title ke liye). Baaki headings hierarchy follow karein (h2 → h3 → h4).

### Links & Images
```html
<a href="page.html">Internal link</a>
<a href="https://google.com" target="_blank" rel="noopener noreferrer">External link</a>
<img src="photo.jpg" alt="photo description" width="300" height="200">
```

- `alt` attribute **zaroori** hai — accessibility ke liye aur agar image load na ho toh.
- External links pe `target="_blank"` ke saath `rel="noopener noreferrer"` lagao (security best practice).

### Lists
```html
<!-- Unordered (bullets) -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<!-- Ordered (numbers) -->
<ol>
  <li>Step 1</li>
  <li>Step 2</li>
</ol>

<!-- Description list -->
<dl>
  <dt>HTML</dt>
  <dd>Markup language</dd>
</dl>
```

### Div & Span (Generic containers)
```html
<div>Block-level generic container — layout ke liye</div>
<span>Inline generic container — text ke andar styling ke liye</span>
```

---

## 4. Semantic Tags — IMPORTANT ⭐

**Semantic tags** wo tags hote hain jinka naam khud batata hai ki unke andar kaisa content hai — sirf `<div>` use karne ke bajaye, jo meaning nahi batata.

### Kyun important hain?
1. **SEO** — Google/search engines page ko better samajhte hain
2. **Accessibility** — screen readers (blind users ke liye) content ko sahi se navigate kar paate hain
3. **Readability** — code khud-explanatory ban jaata hai, team ko samajhna easy hota hai
4. **Maintainability** — future mein edit karna aasan

### Main Semantic Tags

| Tag | Use |
|---|---|
| `<header>` | Page ya section ka top part — logo, nav, title |
| `<nav>` | Navigation links ka group |
| `<main>` | Page ka main/unique content (ek page mein sirf ek baar) |
| `<section>` | Content ka logical grouping (jaise "About", "Services") |
| `<article>` | Independent, self-contained content (blog post, news article, card) |
| `<aside>` | Side content — sidebar, related links, ads |
| `<footer>` | Page ya section ka bottom part — copyright, contact info |
| `<figure>` + `<figcaption>` | Image/diagram with caption |
| `<time>` | Date/time represent karne ke liye |
| `<mark>` | Highlighted text |

### Semantic Layout Example

```html
<body>
  <header>
    <h1>My Portfolio</h1>
    <nav>
      <a href="#home">Home</a>
      <a href="#projects">Projects</a>
    </nav>
  </header>

  <main>
    <section id="about">
      <h2>About Me</h2>
      <p>...</p>
    </section>

    <section id="projects">
      <h2>Projects</h2>
      <article>
        <h3>ResumeFlow</h3>
        <p>Landing page project...</p>
      </article>
    </section>

    <aside>
      <h3>Quick Links</h3>
      <ul><li><a href="#">GitHub</a></li></ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2026 Yashi. All rights reserved.</p>
  </footer>
</body>
```

### `<div>` vs Semantic tag — kab kya use karein?
- Agar content ka koi specific **meaning/role** hai (navigation, article, footer) → **semantic tag** use karo
- Agar sirf **styling/layout** purpose se grouping chahiye, koi meaning nahi hai → `<div>` use karo

---

## 5. Forms

Form user se input lene ke liye use hota hai.

```html
<form action="/submit" method="POST">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required placeholder="Enter your name">

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>

  <label for="password">Password:</label>
  <input type="password" id="password" name="password">

  <label for="age">Age:</label>
  <input type="number" id="age" name="age" min="1" max="100">

  <label for="bio">Bio:</label>
  <textarea id="bio" name="bio" rows="4"></textarea>

  <label for="country">Country:</label>
  <select id="country" name="country">
    <option value="india">India</option>
    <option value="usa">USA</option>
  </select>

  <input type="checkbox" id="terms" name="terms">
  <label for="terms">I agree to terms</label>

  <input type="radio" id="male" name="gender" value="male">
  <label for="male">Male</label>
  <input type="radio" id="female" name="gender" value="female">
  <label for="female">Female</label>

  <button type="submit">Submit</button>
</form>
```

### Important Form Concepts
- **`<label for="id">`** hamesha input ke `id` se match hona chahiye — accessibility ke liye zaroori (click on label = focus input)
- **`name` attribute** — server ko data submit karte waqt field identify karne ke liye
- **`required`** — HTML-level validation
- **Input types:** `text`, `email`, `password`, `number`, `date`, `tel`, `url`, `file`, `checkbox`, `radio`, `submit`

---

## 6. Tables

```html
<table>
  <caption>Student Marks</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Subject</th>
      <th>Marks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Yashi</td>
      <td>Web Tech</td>
      <td>95</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Average</td>
      <td>95</td>
    </tr>
  </tfoot>
</table>
```

| Tag | Kaam |
|---|---|
| `<table>` | Poori table ka wrapper |
| `<thead>` | Header row(s) |
| `<tbody>` | Main data rows |
| `<tfoot>` | Footer row (totals etc.) |
| `<tr>` | Table row |
| `<th>` | Header cell (bold, centered by default) |
| `<td>` | Normal data cell |
| `colspan` / `rowspan` | Cells ko merge karne ke liye |

> Tables sirf **tabular data** ke liye use karo, layout banane ke liye nahi (purana practice tha, ab CSS Grid/Flexbox use hota hai).

---

## 7. Accessibility Basics (a11y)

- Har `<img>` mein meaningful `alt` text do
- Semantic tags use karo (`<nav>`, `<button>` — na ki `<div onclick>`)
- Form inputs ko hamesha `<label>` do
- Heading hierarchy break mat karo (h1 → h2 → h3, skip mat karo)
- `<button>` use karo clickable actions ke liye, `<a>` sirf navigation ke liye
- Color ke alawa bhi info convey karo (sirf red/green pe depend mat karo)
- `tabindex` aur keyboard navigation test karo

---

## 8. Best Practices

1. **Semantic HTML likho** — meaning-based tags use karo, sirf div-soup mat banao
2. **Indentation consistent rakho** — nested tags clearly dikhne chahiye
3. **Lowercase tags/attributes** likho (`<div>` not `<DIV>`)
4. **Attributes double quotes mein** rakho — `class="box"`
5. **Alt text kabhi mat bhoolo** images pe
6. **Ek hi `<h1>`** per page
7. **External CSS/JS files** use karo — inline styles/scripts avoid karo (separation of concerns)
8. **Validate karo** — [W3C Validator](https://validator.w3.org/) se check kar sakte ho
9. **Comments** likho complex sections ke upar: `<!-- Navigation section -->`
10. **Mobile-first** socho — viewport meta tag zaroor daalo

---

## 9. Quick Reference — Block vs Inline Elements

| Block-level (naya line, full width) | Inline (line ke andar hi, sirf content jitni width) |
|---|---|
| `<div>`, `<p>`, `<h1>-<h6>` | `<span>`, `<a>`, `<strong>`, `<em>` |
| `<section>`, `<article>` | `<img>`, `<button>`, `<label>` |
| `<ul>`, `<ol>`, `<table>` | `<input>` |

---

## Summary

- HTML = structure/skeleton of webpage
- Tags define content ka type; attributes extra info dete hain
- **Semantic tags** SEO + accessibility + readability ke liye use karo, sirf `<div>` nahi
- Forms user input lete hain — labels aur proper `name`/`id` zaroori
- Tables sirf tabular data ke liye
- Accessibility aur best practices follow karke likha HTML professional dikhta hai
