# MySQL Learning Notes — Tables, Keys & Joins
*Full-Stack Internship · Database Basics*

---

##  Why We Moved Away From `data.json`

Before this, our resume project was storing all its data inside a simple file called `data.json`. It's just a text file — every user and every resume was written inside it as plain text, and our code opened this file, read it, changed it, and saved it back every time.

This worked fine in class, but it breaks in the real world for two reasons:

> **Analogy — Two People Editing the Same Word File**
> Imagine two people open the same Word file on their own laptops at the same time. Both make changes and save. Whoever saves last "wins" — the other person's changes are silently lost, with no warning. This is called a **race condition**, and a plain file cannot stop it.
> A **database** behaves like a shared Google Doc instead — everyone works on the same live copy, changes don't overwrite each other, and nothing gets silently lost.

The second reason is **speed**. If `data.json` had thousands of resumes in it, our code would have to load the entire file and loop through every single entry just to find one record. A database is built specifically to avoid this — it can find the right record almost instantly, no matter how large the data gets.

So we moved the resume project from a text file to a **real MySQL database**.

---

## 1) Installed MySQL Server and MySQL Workbench

- **MySQL Server** = the actual database engine (runs in the background as a Windows service)
- **MySQL Workbench** = the GUI tool used to write queries, view tables, and manage the database
- Set a root password during installation

### what is mySQL
> MySQL Server is like the secure server room inside a bank where all the actual money (data) is kept — you never touch it directly. MySQL Workbench is like the ATM screen — an interface where you give instructions ("show balance," "deposit money") without ever entering the server room yourself. The root password is like your ATM PIN — forget it, and you can't connect anymore.

---

## 2) The Hierarchy: Server → Database → Table → Row

- **Server** → holds many **Databases**
- **Database** → holds many **Tables**
- **Table** → holds many **Rows** (records)

> **Analogy — Folders Inside Folders on Your Laptop**
> Think of it like nested folders. The **Server** is your whole laptop (runs everything in the background). A **Database** (`resume_db`) is one project folder, like an "Internship" folder. A **Table** (`users`, `resumes`) is a file inside that folder, like a separate Excel sheet. A **Row** is one line inside that sheet.

---

## 3) Created a Database

```sql
CREATE DATABASE resume_db;
USE resume_db;
```

---

## 4) Created the `users` Table

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(45) NOT NULL,
    email VARCHAR(45) NOT NULL UNIQUE
);
```

- `id` → Primary Key, auto-increments automatically (don't need to fill it manually)
- `name` → cannot be empty (`NOT NULL`)
- `email` → cannot be empty and must be unique (no two users can have the same email)

> **Analogy — College Roll Numbers**
> The `id` is like a roll number the office assigns automatically (`AUTO_INCREMENT`) — you never pick your own. `email UNIQUE` works like an Aadhaar number: only one person can have a particular Aadhaar number, so no two users can register with the same email.

---

## 5) Inserted Data and Read It Back

Added records using the GUI (Select Rows → Apply) and also learned the SQL way:

```sql
INSERT INTO users (name, email) VALUES ('unishka', 'unishka@gmail.com');
SELECT * FROM users;
SELECT * FROM users WHERE name = 'unishka';
```

> **Analogy — Managing Your Phone Contacts**
> - `INSERT` = saving a new contact
> - `SELECT` = opening your contact list to look at it
> - `WHERE` = typing a name in the search bar so only that contact shows up

**Final `users` table data:**

| id | name    | email               |
|----|---------|---------------------|
| 1  | unishka | unishka@gmail.com   |
| 2  | divyani | divyani@gmail.com   |
| 3  | vijay   | vijay@gmail.com     |
| 4  | manish  | manish@gmail.com    |
| 5  | ishita  | ishita@gmail.com    |


---

## 6) Created a Second Table: `resumes` (with a Foreign Key)

```sql
CREATE TABLE resumes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    userId INT NOT NULL,
    tittle VARCHAR(150) NOT NULL,
    FOREIGN KEY (userId) REFERENCES users(id)
);
```

**Definition — Foreign Key:** A column in one table that points to a row in another table. It ensures the value in that column can only be something that actually exists in the table it references — this stops invalid or "orphan" data from being created.

- `id` → Primary Key of the `resumes` table itself (its own identity)
- `userId` → Foreign Key, points to `users.id` — tells us **which user owns this resume**

**Key concept learned:**
- **Primary Key** = "who am I" (identity of a row in its own table)
- **Foreign Key** = "who do I belong to" (reference to a row in another table)

> **Analogy — Swiggy Order Linked to a Customer ID**
> When you order food on Swiggy, the order has its own Order ID (Primary Key), but it also carries your Customer ID (Foreign Key) — so the system always knows *whose* order it is. `resumes.userId` does the exact same job: it points back to `users.id` to say which user this resume belongs to.

**Final `resumes` table data:**

| id | userId | tittle                 |
|----|--------|------------------------|
| 1  | 1      | software engineer      |
| 2  | 1      | sales manager          |
| 3  | 2      | frontend developer     |
| 4  | 2      | software developer     |
| 5  | 3      | hr                     |
| 6  | 4      | application developer  |
| 7  | 4      | full stack developer   |

*(One user can have multiple resumes — e.g., userId 1 and userId 2 each have two resumes.)*

---

## 7) Learned About ON UPDATE / ON DELETE Rules for Foreign Keys

- **RESTRICT** (default): Prevents deleting/updating a user if related resumes exist — throws an error unless the resumes are removed first
- **CASCADE**: Automatically deletes/updates related resumes when the linked user is deleted/updated

> **Analogy — Deleting a Swiggy Account**
> RESTRICT is like Swiggy refusing to delete your account while you have an active order — it blocks the action until things are cleared up. CASCADE is like deleting your account and Swiggy automatically cancelling every order linked to it, no manual cleanup needed.

---

## 8) JOIN — Reading Two Tables Together

**Definition — Join:** A query that combines rows from two tables by matching a common column between them. Here, `resumes.userId` is matched with `users.id`, so each resume gets paired with the user it belongs to.

```sql
SELECT users.name, users.email, resumes.tittle
FROM resumes
JOIN users ON resumes.userId = users.id;
```

> **Analogy — Matching a Courier Parcel to Its Owner**
> One table only has parcel details (tracking number, item). Another table only has the owner's name and address (also tied to a tracking number). A join means matching both tables **by tracking number** so you can see "this parcel belongs to this person." The data stays safely separate, but a join brings both sides together the moment you need it.

**Result of the JOIN query:**

| name    | email               | tittle                 |
|---------|---------------------|-------------------------|
| unishka | unishka@gmail.com   | software engineer      |
| unishka | unishka@gmail.com   | sales manager          |
| divyani | divyani@gmail.com   | frontend developer     |
| divyani | divyani@gmail.com   | software developer     |
| vijay   | vijay@gmail.com     | hr                     |
| manish  | manish@gmail.com    | application developer  |
| manish  | manish@gmail.com    | full stack developer   |

---

## 9) Normalization — Store Each Fact Only Once

**Definition — Normalization:** Organizing data so that each fact is stored in exactly one place, instead of repeating it across multiple rows or tables.

> **Analogy — Not Photocopying Your Aadhaar Card Onto Every Form**
> Bad design: copy the user's name and email onto every single resume row. If the user ever changes their email, you'd have to **hunt down and update every resume** — miss one, and your data goes out of sync.
> Good design: store the name and email only once, in the `users` table. The `resumes` table just keeps the `userId`. This is like writing only your Aadhaar number on a form instead of photocopying the whole card each time — the original stays safe in one place, and every form just refers back to it.

**One-liner:** Store each fact once, and link to it with an `id`. Use a join to bring it back together whenever you need it.

---

## 10) Indexing — A Shortcut for Faster Search

**Definition — Index:** A data structure MySQL builds on a column so it can find matching rows quickly, instead of scanning the entire table row by row.

> **Analogy — The Index Page at the Back of a Textbook**
> When you look up a topic in a thick textbook, you don't read the whole book — you check the **index page**, which tells you "this topic is on page 214." A MySQL index works the same way — instead of scanning the entire table, MySQL jumps straight to the right row.

```sql
CREATE INDEX idx_email ON users(email);
```

Indexes help the most with: `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY`.

---

## Quick Recap Table

| Term | One-Line Meaning |
|---|---|
| Database | Organized data storage — like a project folder |
| Table | Rows + columns — like an Excel sheet |
| Primary Key | "Who am I" — unique identity of a row |
| Foreign Key | "Who do I belong to" — link to a row in another table |
| Join | Shows data from two tables together — like matching a parcel to its owner by tracking number |
| Normalization | Store each fact only once — like reusing an Aadhaar number instead of copying it everywhere |
| Indexing | A shortcut for faster search — like a textbook's index page |
| RESTRICT | Blocks deletion if related rows exist |
| CASCADE | Auto-deletes/updates related rows |

---

## What Was Actually Run Today

```sql
CREATE DATABASE resume_db;
USE resume_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(45) NOT NULL,
    email VARCHAR(45) NOT NULL UNIQUE
);

INSERT INTO users (name, email) VALUES ('unishka', 'unishka@gmail.com');
SELECT * FROM users;
SELECT * FROM users WHERE name = 'unishka';

CREATE TABLE resumes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    userId INT NOT NULL,
    tittle VARCHAR(150) NOT NULL,
    FOREIGN KEY (userId) REFERENCES users(id)
);

SELECT users.name, users.email, resumes.tittle
FROM resumes
JOIN users ON resumes.userId = users.id;
```

---

## Summary of Today's Learning

- How Server, Database, Table, and Row relate to each other
- Creating databases and tables using SQL
- Difference between Primary Key and Foreign Key
- Inserting and retrieving data (INSERT, SELECT, WHERE, ORDER BY)
- Linking two tables using a Foreign Key relationship
- Using JOIN to combine data from multiple related tables into one result
