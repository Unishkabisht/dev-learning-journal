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

**Also learned:** without `ORDER BY`, MySQL does **not guarantee** any particular row order. Use `ORDER BY id` (or any column) to control the order explicitly.

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

---
---

# Day 2: Database Fundamentals & MySQL

---

## Table of Contents
1. [Core Concepts](#core-concepts)
2. [DBMS vs RDBMS](#dbms-vs-rdbms)
3. [SQL vs NoSQL](#sql-vs-nosql)
4. [Data Types in MySQL](#data-types-in-mysql)
5. [ORM & Sequelize](#orm--sequelize)
6. [Structured vs Unstructured Data](#structured-vs-unstructured-data)
7. [Why ORM When We Have SQL](#why-orm-when-we-have-sql)

---

## Core Concepts

### 1. What is a Database?

**Definition:** A database is an **organized collection of structured data** stored in a way that allows efficient retrieval, modification, and management.

**Key Points:**
- Data is stored in an organized manner for easy access
- Data doesn't manage itself—it needs a DBMS to maintain, protect, and query it
- Enables multi-user access with data consistency and security

**Real-World Analogy:** Think of a database as a well-organized library where books (data) are arranged in a system, indexed, and managed by a librarian (DBMS).

---

### 2. What is a DBMS?

**DBMS** stands for **Database Management System**.

**Definition:** The software application that stores, manages, retrieves, and protects data in a database.

**Responsibilities:**
- **Storing** data safely and efficiently
- **Retrieving** data when requested
- **Protecting** data from unauthorized access
- **Managing** concurrent user access
- **Maintaining** data integrity and consistency

**Examples of DBMS:**
- MySQL
- PostgreSQL
- Oracle Database
- MongoDB (NoSQL DBMS)
- Microsoft SQL Server

**What You're Actually Installing:**  
When you "install MySQL," you're installing a DBMS—the software that manages databases for you.

---

## DBMS vs RDBMS

### DBMS (Database Management System)

**What it is:** A general-purpose software system for managing any kind of database.

| Feature | Details |
|---------|---------|
| **Data Structure** | Can organize data in various ways (hierarchical, network, relational, document-based) |
| **Relationships** | Minimal or no built-in relationship management |
| **Data Integrity** | Basic data integrity constraints |
| **Query Language** | Varies by system; not standardized |
| **Scalability** | Limited horizontal scalability in traditional DBMS |
| **Example Systems** | File systems, flat-file databases, simple data stores |

**Use Cases:**
- Simple data storage needs
- Unstructured or semi-structured data
- Applications with minimal relationship requirements

---

### RDBMS (Relational Database Management System)

**What it is:** A specialized type of DBMS that organizes data into **structured tables with predefined relationships**.

| Feature | Details |
|---------|---------|
| **Data Structure** | Organizes data into **tables (rows and columns)** with relationships |
| **Relationships** | Strong support for relationships via **foreign keys** and **normalization** |
| **Data Integrity** | Enforces **ACID properties** (Atomicity, Consistency, Isolation, Durability) |
| **Query Language** | Uses **SQL** (Structured Query Language)—a standardized language |
| **Schema** | Requires **fixed schema** defined before data insertion |
| **Example Systems** | MySQL, PostgreSQL, Oracle, SQL Server, MariaDB |

**Benefits of RDBMS:**
- Data consistency and reliability
- Efficient querying with SQL
- Strong support for complex queries involving multiple tables
- ACID compliance ensures reliable transactions

---

### Quick Comparison

```
┌─────────────────────────────────────────────────────────────┐
│ DBMS (Generic)          │ RDBMS (Structured)              │
├─────────────────────────────────────────────────────────────┤
│ Loose data structure     │ Strict table-based structure    │
│ Limited relationships    │ Strong relationships (FK)       │
│ No standard query lang   │ Standard SQL language           │
│ Basic integrity          │ ACID compliance                 │
│ Lower overhead           │ Higher overhead but safer       │
│ Example: File database   │ Example: MySQL, PostgreSQL     │
└─────────────────────────────────────────────────────────────┘
```

---

## SQL vs NoSQL

### SQL Databases (Structured/Relational)

**Definition:** SQL (Structured Query Language) databases are **relational databases** that store data in structured tables with predefined schemas.

**Characteristics:**
- **Table-based:** Data organized in rows and columns
- **Predefined Schema:** Structure defined before data entry
- **Relationships:** Uses foreign keys to link tables
- **ACID Compliant:** Guarantees data reliability
- **Vertical Scaling:** Scale by adding more power (CPU, RAM) to existing server

**When to Use SQL:**
- ✅ Structured, relational data (users, orders, products)
- ✅ Need strict data consistency
- ✅ Complex queries across multiple tables
- ✅ Financial or mission-critical systems
- ✅ Data with clear relationships (e.g., orders belong to users)

**Examples:**
- MySQL
- PostgreSQL
- Oracle
- SQL Server
- MariaDB

---

### NoSQL Databases (Unstructured/Non-Relational)

**Definition:** NoSQL databases store data in **flexible, unstructured or semi-structured formats** without requiring a predefined schema.

**Characteristics:**
- **Flexible Structure:** No strict schema; documents can have different fields
- **Document/Key-Value Based:** Stores data as JSON documents, key-value pairs, etc.
- **Horizontal Scaling:** Easily scale by adding more servers
- **Eventually Consistent:** May not guarantee immediate consistency across all nodes
- **High Performance:** Optimized for high-speed read/write operations

**When to Use NoSQL:**
- ✅ Unstructured or semi-structured data (logs, user-generated content)
- ✅ Rapidly changing data models
- ✅ Need massive horizontal scalability
- ✅ Real-time big data applications
- ✅ Flexible schema requirements (e.g., different user profiles with varying fields)

**Examples:**
- MongoDB (Document)
- Redis (Key-Value)
- Cassandra (Column-family)
- DynamoDB (Key-Value)
- Elasticsearch (Search/Logging)

---

### SQL vs NoSQL: Detailed Comparison

| Aspect | SQL | NoSQL |
|--------|-----|-------|
| **Data Model** | Tables (Rows & Columns) | Documents, Key-Value, Graphs |
| **Schema** | Fixed, predefined | Flexible, dynamic |
| **Query Language** | SQL (standardized) | Query language varies |
| **Relationships** | Foreign Keys, Joins | References (less structured) |
| **ACID** | ✅ Guaranteed | ⚠️ Eventual Consistency |
| **Scaling** | Vertical (add resources to server) | Horizontal (add more servers) |
| **Performance** | Excellent for complex queries | Excellent for simple, fast queries |
| **Data Integrity** | Strong constraints | Flexible constraints |
| **Learning Curve** | Moderate | Varies by system |
| **Best For** | Structured, relational data | Large-scale, unstructured data |

---

## Data Types in MySQL

### Text Data Types

#### STRING vs VARCHAR

**Why two layers?**
- `STRING` is the **JavaScript/Sequelize name**
- `VARCHAR` is the **actual MySQL column type**
- When you define `DataTypes.STRING` in Sequelize, it transforms into `VARCHAR(255)` in MySQL

```javascript
// Sequelize (JavaScript layer)
const User = sequelize.define('User', {
  name: DataTypes.STRING,  // JavaScript name
});
// Becomes this in MySQL:
// name VARCHAR(255)
```

---

#### CHAR(size)

**Definition:** Fixed-length text column. Always reserves the exact number of cells regardless of actual data length.

**Storage Example for "Deepesh" (7 letters) in CHAR(10):**
```
D | e | e | p | e | s | h | · | · | ·
= 10 cells always reserved
(3 blank spaces added as padding)
```

**Pros:**
- Fast lookups (fixed size known in advance)
- Good for columns with consistent lengths (ZIP codes, phone numbers)

**Cons:**
- Wastes space for shorter values
- Padding added unnecessarily

---

#### VARCHAR(size)

**Definition:** Variable-length text column. Stores only the data you provide, up to the specified size limit.

**Storage Example for "Deepesh" (7 letters) in VARCHAR(10):**
```
D | e | e | p | e | s | h
= 7 cells used (no padding)
```

**Pros:**
- Space-efficient
- Better for text with varying lengths
- Saves memory (especially with millions of records)

**Cons:**
- Slightly slower lookup (variable size)

---

#### Rule of Thumb

```
📌 Use CHAR when: All values are exactly the same length
   Example: Country codes (always 2 letters), SKU codes

📌 Use VARCHAR when: Text length varies
   Example: Names, emails, addresses
   
⚠️ Storage Impact:
   1 million names stored in CHAR(10) vs VARCHAR(10)
   = Massive wasted space with CHAR
```

---

### Specialized MySQL Data Types

#### ENUM

**Definition:** A column that can hold **only one value from a predefined list**.

**Syntax:**
```sql
ENUM('value1', 'value2', 'value3')
```

**Example:**
```sql
CREATE TABLE posts (
  id INT PRIMARY KEY,
  title VARCHAR(255),
  status ENUM('active', 'pending', 'deleted')
);
```

**Use Cases:**
- ✅ Status fields (active, inactive, pending, archived)
- ✅ Category fields with fixed options
- ✅ Role fields (admin, user, guest)

**Advantages:**
- Prevents invalid data entry
- Keeps data consistent
- MySQL will reject any value not in the list
- Space-efficient (stored as integer internally)

**Example in Sequelize:**
```javascript
const Post = sequelize.define('Post', {
  title: DataTypes.STRING,
  status: DataTypes.ENUM('active', 'pending', 'deleted'),
});
```

---

#### BOOLEAN

**Definition:** A true/false column for yes-or-no questions.

**Typical Usage Examples:**
- `isVerified` — Is the user email verified?
- `termsAccepted` — Did the user accept terms?
- `isActive` — Is the account active?
- `isPremium` — Is the user a premium subscriber?

**In Sequelize:**
```javascript
const User = sequelize.define('User', {
  email: DataTypes.STRING,
  isVerified: DataTypes.BOOLEAN,      // false by default
  termsAccepted: DataTypes.BOOLEAN,   // false by default
  isActive: DataTypes.BOOLEAN,         // true by default
});
```

**Storage:**
- MySQL stores BOOLEAN as TINYINT(1)
- `true` = 1
- `false` = 0

---

#### TINYINT

**Definition:** A very small integer column (takes up minimal space).

**Range:**
- Signed: -128 to 127
- Unsigned: 0 to 255

**Use Cases:**
- User ratings (1-5 stars)
- Small counts
- Flags (0 or 1)
- Small age ranges

**Example:**
```sql
CREATE TABLE ratings (
  id INT PRIMARY KEY,
  stars TINYINT,  -- Stores 1-5
  helpful TINYINT  -- Stores 0 or 1 (like BOOLEAN)
);
```

**Storage Benefit:**
- TINYINT uses only 1 byte
- INT uses 4 bytes
- Important when storing millions of records

---

### Data Type Quick Reference

```javascript
// Sequelize → MySQL Mapping

// Text
DataTypes.STRING        → VARCHAR(255)
DataTypes.STRING(50)    → VARCHAR(50)
DataTypes.TEXT          → TEXT (longer text)

// Numbers
DataTypes.INTEGER       → INT
DataTypes.BIGINT        → BIGINT
DataTypes.FLOAT         → FLOAT
DataTypes.DECIMAL(8,2)  → DECIMAL(8,2) [for prices]

// Boolean
DataTypes.BOOLEAN       → TINYINT(1)

// Specialized
DataTypes.ENUM(...)     → ENUM(...)
DataTypes.DATE          → DATETIME
DataTypes.JSON          → JSON (MySQL 5.7+)

// Example Model
const Product = sequelize.define('Product', {
  name: DataTypes.STRING(255),           // VARCHAR(255)
  description: DataTypes.TEXT,           // TEXT
  price: DataTypes.DECIMAL(10, 2),       // DECIMAL(10,2)
  stock: DataTypes.TINYINT,              // TINYINT
  inStock: DataTypes.BOOLEAN,            // TINYINT(1)
  category: DataTypes.ENUM('electronics', 'clothing', 'books'),
  rating: DataTypes.FLOAT,               // FLOAT
});
```

---

## ORM & Sequelize

### What is an ORM?

**ORM** stands for **Object-Relational Mapping**.

**Definition:** A programming technique that lets you interact with a database using **objects in your programming language** instead of writing raw SQL queries.

**The Problem It Solves:**
- SQL and JavaScript are different languages
- Converting between JavaScript objects and SQL queries is repetitive
- Easy to make mistakes with raw SQL
- SQL queries are strings (hard to validate at development time)

**The Solution:**
- ORM acts as a **bridge** between your JavaScript code and the database
- You work with JavaScript objects
- ORM automatically converts them to SQL queries

---

### ORM Architecture

```
┌──────────────────────────────────────────────────────┐
│         Your JavaScript Application                  │
│  (Objects, functions, business logic)                │
└──────────────────────────┬───────────────────────────┘
                           │
                    Uses objects/models
                           │
┌──────────────────────────▼───────────────────────────┐
│            ORM (Sequelize)                           │
│  Translates JS objects → SQL queries                 │
│  Translates SQL results → JS objects                 │
└──────────────────────────┬───────────────────────────┘
                           │
                  Executes SQL queries
                           │
┌──────────────────────────▼───────────────────────────┐
│         Database (MySQL, PostgreSQL, etc.)           │
│  Stores data in tables                               │
└──────────────────────────────────────────────────────┘
```

---

### What is Sequelize?

**Sequelize** is a **popular ORM for Node.js** that makes working with SQL databases easier.

**Key Features:**
- Works with multiple databases (MySQL, PostgreSQL, SQLite, MSSQL)
- Write database models in JavaScript
- Automatic SQL query generation
- Data validation and constraints
- Associations (relationships between models)
- Migrations (version control for database structure)

---

### Sequelize in Action

#### Without ORM (Raw SQL)

```javascript
// You have to write SQL strings manually
const result = await connection.query(
  "SELECT * FROM users WHERE id = ? AND email = ?",
  [userId, userEmail]
);

// Converting results to JavaScript objects manually
const user = {
  id: result[0].id,
  name: result[0].name,
  email: result[0].email,
  created_at: result[0].created_at
};
```

**Problems:**
- 🔴 Writing SQL strings by hand (error-prone)
- 🔴 Manual result conversion
- 🔴 Hard to validate SQL at development time
- 🔴 Repetitive code
- 🔴 SQL injection risks if not careful

---

#### With Sequelize ORM

```javascript
// Define your model (JavaScript object)
const User = sequelize.define('User', {
  id: {
    type: DataTypes.INTEGER,
    primaryKey: true,
    autoIncrement: true,
  },
  name: DataTypes.STRING,
  email: DataTypes.STRING,
  createdAt: DataTypes.DATE,
});

// Query using JavaScript methods (not SQL strings!)
const user = await User.findByPk(userId);
// Sequelize automatically generates: SELECT * FROM users WHERE id = ?

// Or with conditions
const user = await User.findOne({
  where: { id: userId, email: userEmail }
});
// Sequelize generates: SELECT * FROM users WHERE id = ? AND email = ?

// Result is automatically a JavaScript object
console.log(user.name);     // Direct property access
console.log(user.email);    // Type-safe
```

**Advantages:**
- ✅ Write JavaScript, not SQL strings
- ✅ Automatic type safety
- ✅ Query validation at development time
- ✅ Less repetitive code
- ✅ Built-in security against SQL injection
- ✅ Results are JavaScript objects automatically

---

### Sequelize Key Concepts

#### 1. Models

A **model** is a JavaScript representation of a database table.

```javascript
const User = sequelize.define('User', {
  // Column definitions
  id: {
    type: DataTypes.INTEGER,
    primaryKey: true,
    autoIncrement: true,
  },
  email: {
    type: DataTypes.STRING,
    allowNull: false,
    unique: true,
  },
  name: DataTypes.STRING,
  isActive: {
    type: DataTypes.BOOLEAN,
    defaultValue: true,
  },
  role: DataTypes.ENUM('admin', 'user', 'guest'),
});

// Now you can use User to query the database
```

---

#### 2. Associations (Relationships)

Define relationships between models.

```javascript
// One-to-Many: One user has many posts
User.hasMany(Post);
Post.belongsTo(User);

// Many-to-Many: Users and projects
User.belongsToMany(Project, { through: 'UserProject' });
Project.belongsToMany(User, { through: 'UserProject' });

// Usage in queries
const userWithPosts = await User.findOne({
  where: { id: userId },
  include: [Post]  // Automatically joins the posts table
});
```

**Sequelize generates the complex SQL JOIN automatically!**

---

#### 3. Queries

```javascript
// CREATE
const newUser = await User.create({
  email: 'john@example.com',
  name: 'John Doe',
  role: 'user'
});

// READ - Single record
const user = await User.findByPk(1);

// READ - Multiple records
const allUsers = await User.findAll({
  where: { isActive: true }
});

// UPDATE
await user.update({ name: 'Jane Doe' });

// DELETE
await user.destroy();
```

**All of this is translated to SQL by Sequelize!**

---

## Structured vs Unstructured Data

### Structured Data

**Definition:** Data organized in a **predefined format** with a clear structure.

**Characteristics:**
- Organized in tables, rows, and columns
- Follows a fixed schema
- Every record has the same fields
- Easily queryable and searchable
- Predictable format

**Examples:**
- Employee database (consistent columns: name, email, salary, department)
- Customer orders (order ID, customer ID, amount, date)
- Product catalog (product name, price, description, stock)
- Bank transactions (account ID, amount, date, type)

**Storage:**
```sql
-- Example: Employee table (Structured)
CREATE TABLE employees (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100),
  salary DECIMAL(10, 2),
  department VARCHAR(50),
  hireDate DATE
);

-- Every record has exactly these 6 fields
-- All data follows the same structure
```

**Advantages:**
- ✅ Efficient querying and indexing
- ✅ Data consistency guaranteed
- ✅ Easier to validate and constrain
- ✅ Optimal for relationships (joins)
- ✅ Better for reporting and analytics

**Best Used With:** SQL Databases (MySQL, PostgreSQL, Oracle)

---

### Unstructured Data

**Definition:** Data that **doesn't follow a predefined structure** or schema.

**Characteristics:**
- No fixed format or organization
- Flexible schema (or no schema)
- Different records can have different fields
- Text, images, videos, audio
- Harder to search and query
- High volume, variety

**Examples:**
- Social media posts (different users, different content types)
- Log files (varying formats and fields)
- User-generated content (reviews, comments, articles)
- Images and videos
- Email messages
- Customer feedback and surveys

**Storage:**
```javascript
// Example: Social media posts (Unstructured)
// Post 1
{
  userId: 123,
  content: "Just had coffee!",
  timestamp: "2024-01-15T10:30:00Z",
  likes: 45
}

// Post 2 (different structure)
{
  userId: 456,
  content: "Check out this photo",
  image: "https://...",
  timestamp: "2024-01-15T11:00:00Z",
  likes: 200,
  comments: [{ userId: 789, text: "Nice!" }],
  hashtags: ["photography", "nature"]
}

// Post 3 (yet another structure)
{
  userId: 789,
  videoUrl: "https://...",
  duration: 120,
  caption: "Video tutorial",
  views: 1000,
  shares: 50
}

// Each post can have different fields!
```

**Advantages:**
- ✅ Flexible and adaptable to changing requirements
- ✅ Can handle diverse data types
- ✅ Scalable for massive data volumes
- ✅ Fast writes (no schema validation overhead)
- ✅ Good for rapid development (iterate quickly)

**Disadvantages:**
- ❌ Harder to query and search
- ❌ No guaranteed data consistency
- ❌ More complex to analyze
- ❌ Storage overhead (stores field names with every record)

**Best Used With:** NoSQL Databases (MongoDB, DynamoDB, Cassandra)

---

### Structured vs Unstructured: Comparison

| Aspect | Structured | Unstructured |
|--------|-----------|--------------|
| **Format** | Fixed, predefined | Flexible, varying |
| **Schema** | Strict schema required | No fixed schema |
---
---
# Day 18 · Day 3 notes — Storing Data, Step by Step.

**Topic:** Full-Stack Internship · Module 4 · Database
**Instructor:** Dinesh Rawat

---

## What this class is about

In the last class, you created a database and a `users` table by hand in MySQL Workbench, and wrote INSERT/SELECT queries yourself. Today you do the same work from JavaScript — meaning the code talks to the database now, one operation at a time. For each step, you'll see three things:

1. What JavaScript you write
2. What SQL Sequelize (the ORM) turns it into
3. What result comes back

By the end of this class, a real user will be saved in the database, along with their resumes. You'll then read them back and update one of them — and you'll understand exactly what each line does to the database.

---

## Step 0: The setup before any step

Three model files describe the tables, and one connection file talks to MySQL. You already wrote versions of these before — here they're shown together so every step below has a solid foundation.

### `config/database.js` — the MySQL connection

This file tells Sequelize where the database is and how to connect to it.

```javascript
const { Sequelize } = require('sequelize');

const sequelize = new Sequelize(
  'resume_db',        // the database name (already created in MySQL Workbench)
  'root',             // your MySQL username
  'your_password',    // your MySQL password (set during installation)
  {
    host: 'localhost', // MySQL runs on your own machine
    dialect: 'mysql',  // tells Sequelize to speak MySQL
    logging: false,    // set to console.log to see every SQL query it sends
  }
);

module.exports = sequelize;
```

In simple terms: this file creates just one connection object, and every other file talks to the database through this same object. That's why it acts as the single source of truth for the connection.

### `models/user.js` — the structure of the User table

```javascript
const { DataTypes } = require('sequelize');
const bcrypt = require('bcryptjs');
const sequelize = require('../config/database');

const User = sequelize.define('User', {
  name: { type: DataTypes.STRING, allowNull: false },
  email: { type: DataTypes.STRING, allowNull: false, unique: true,
    validate: { isEmail: true } },
  password: { type: DataTypes.STRING, allowNull: false },
});

// hash the password before it gets saved
User.beforeCreate(async (user) => {
  const salt = await bcrypt.genSalt(10);
  user.password = await bcrypt.hash(user.password, salt);
});

User.prototype.checkPassword = function (plainText) {
  return bcrypt.compare(plainText, this.password);
};

// ---- this model's relationship lives in this file ----
// This function receives all the models, so it never needs to
// require Resume itself. That's what avoids the circular require.
// It's called once, after all models have been loaded
// (see models/index.js).
User.associate = (models) => {
  User.hasMany(models.Resume, { foreignKey: 'userId', onDelete: 'CASCADE' });
};

module.exports = User;
```

The important thing here: the password is never saved as plain text. The `beforeCreate` hook automatically hashes it with bcrypt right before it's saved.

### `models/resume.js` — the structure of the Resume table

```javascript
const { DataTypes } = require('sequelize');
const sequelize = require('../config/database');

const Resume = sequelize.define('Resume', {
  title: { type: DataTypes.STRING, allowNull: false },
  summary: { type: DataTypes.TEXT },
});

// ---- this model's relationship lives in this file ----
Resume.associate = (models) => {
  Resume.belongsTo(models.User, { foreignKey: 'userId' });
};

module.exports = Resume;
```

### `models/index.js` — the file that connects all models

```javascript
const sequelize = require('../config/database');
const User = require('./user');
const Resume = require('./resume');

const models = { User, Resume };

// now that all models are loaded, wire up each one's relationships
Object.values(models).forEach((model) => {
  if (model.associate) model.associate(models);
});

module.exports = { sequelize, ...models };
```

**Important pattern to understand:** earlier, the job of defining `associate` used to sit in one single file (all relationships written there together). Now, each model defines its own relationship inside its own file (`User.associate`, `Resume.associate`), and `index.js` simply loads all the models and then calls each model's `associate()` once. This keeps the code cleaner and avoids circular require issues (like the User file needing to directly require Resume).

---

## Step 1: Syncing the database

```javascript
const { sequelize, User, Resume } = require('./models');
await sequelize.sync(); // no force, so existing data is kept
```

`sync()` means — Sequelize creates tables in the database based on the models, if they don't already exist. Here, `force: true` was NOT passed, so if the `users` or `resumes` tables already exist, their data stays safe. If `force: true` were passed, every time `sync()` runs the tables would be dropped and recreated fresh — meaning all existing data would be wiped out.

---

## Step 2: Creating a new User

```javascript
const user = await User.create({
  name: 'Himanshu',
  email: 'himanshu@example.com',
  password: 'secret123',
});

console.log('Saved user #' + user.id);
```

**Sequelize sends this SQL:**

```sql
INSERT INTO `Users`
(`name`, `email`, `password`, `createdAt`, `updatedAt`)
VALUES ('Himanshu', 'himanshu@example.com', ..., NOW(), NOW());
```

**Result:**
```
Saved user #1
```

The key thing to notice here: as soon as `User.create` is called, Sequelize builds the INSERT query. The `createdAt` and `updatedAt` columns get added automatically — you never have to write them manually. And as soon as the row is inserted, the database assigns it an `id` (here, `1`), which comes back right away through `user.id`. That's why you can immediately use this new user's id in the next step.

---

## Step 3: Creating resumes for that user

```javascript
await Resume.create({
  title: 'Full Stack Intern',
  summary: 'Built REST APIs with Node, Express and MySQL.',
  userId: user.id,
});

await Resume.create({
  title: 'QA Intern',
  summary: 'Manual test cases and API tests with Postman.',
  userId: user.id,
});

console.log('Saved 2 resumes');
```

**Sequelize sends this SQL:**

```sql
INSERT INTO `Resumes`
(`title`, `summary`, `userId`, `createdAt`, `updatedAt`)
VALUES ('Full Stack Intern', '...', 1, NOW(), NOW());
```

**Result:**
```
Saved 2 resumes
```

Here, `userId: user.id` is exactly what links this Resume to the User. Since `user.id` from the previous step was `1`, this resume gets saved with `userId: 1` — meaning it belongs to that specific user.

---

## Step 4: Reading all resumes belonging to that user

```javascript
const resumes = await Resume.findAll({ where: { userId: user.id } });
console.log('This user has', resumes.length, 'resumes:');
resumes.forEach(r => console.log(' -', r.title));
```

**Sequelize sends this SQL:**

```sql
SELECT id, title, summary, userId, createdAt, updatedAt
FROM `Resumes`
WHERE `userId` = 1;
```

**Result:**
```
This user has 2 resumes:
 - Full Stack Intern
 - QA Intern
```

`findAll` means fetching multiple rows, and `where: { userId: ... }` acts as a filter — just like SQL's `WHERE` clause. Only the resumes belonging to that matching user id will come back.

(If only a single row were needed, you'd use `findByPk` or `findOne` instead of `findAll`.)

---

## Step 5: Fetching a Resume together with its User (JOIN)

```javascript
const first = await Resume.findByPk(resumes[0].id, { include: User });
console.log('Resume "' + first.title + '" belongs to ' + first.User.name);
```

**Sequelize sends this SQL:**

```sql
SELECT Resume.*, User.name, User.email
FROM `Resumes` AS `Resume`
LEFT OUTER JOIN `Users` AS `User`
ON `Resume`.`userId` = `User`.`id`
WHERE `Resume`.`id` = 1;
```

**Result:**
```
Resume "Full Stack Intern" belongs to Himanshu
```

Here, passing `include: User` tells Sequelize to automatically build a `LEFT OUTER JOIN` — meaning the related User comes back together with the Resume in a single query (matching `Resume.userId` to `User.id`).

**Important thing to remember:** the joined User data will be available as `first.User` (capital U), not the lowercase `first.user`. This is Sequelize's default naming based on the model's name.

---

## Step 6: Updating a resume

```javascript
first.title = 'Senior Full Stack Intern';
await first.save();
console.log('Updated title:', first.title);
```

**Sequelize sends this SQL:**

```sql
UPDATE `Resumes`
SET `title` = 'Senior Full Stack Intern', `updatedAt` = NOW()
WHERE `id` = 1;
```

**Result:**
```
Updated title: Senior Full Stack Intern
```

The pattern here: first, change the property directly on the JS object (`first.title = ...`), then call `.save()`. Sequelize automatically figures out which row to update (based on the `id`), and also automatically sets `updatedAt` to the current time. The `WHERE id = 1` is there because that's exactly what identifies this particular resume.

---

## Final check — looking directly at the database

```sql
SELECT * FROM resumes;
```

```
+----+---------------------------+---------+--------+
| id | title                     | summary | userId |
+----+---------------------------+---------+--------+
| 1  | Senior Full Stack Intern  | ...     | 1      |
| 2  | QA Intern                 | ...     | 1      |
+----+---------------------------+---------+--------+
```

This confirms that everything done through JS code — create, read, and update — is reflected in the actual MySQL table.

---

## The most important takeaway

Every JavaScript line (`create`, `findAll`, `findByPk`, `save`) is actually sending a real SQL query to MySQL behind the scenes. Sequelize just makes this easier so you don't have to write raw SQL yourself, but ultimately every operation converts into an INSERT, SELECT, or UPDATE query. Understanding what SQL is happening behind each JS command is exactly what makes debugging easier when something goes wrong.

