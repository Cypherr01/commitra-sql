# Phase 0 – Foundations of Data & Databases  
**Project Context – Digital Library**  
*Tagline:* **Building a catalog system for a fictional university library**  
*Stack:* HTML · CSS · JavaScript · MySQL · PostgreSQL  

---

## 1. Phase Overview  
Phase 0 establishes the conceptual and technical groundwork required to build a robust, data‑driven library catalog.  Learners will move from “what is data?” to a working development environment, and will create the first tangible artefacts (HTML catalog page, file‑system layout, and a simple MySQL DBMS) that will be expanded in later phases.

---

## 2. Learning Objectives  

By the end of this phase you will be able to:

| # | Objective |
|---|-----------|
| 2.1 | Define **data**, **information**, and explain why data is the core asset of any software system. |
| 2.2 | Describe how computers store data on disk (bits → bytes → blocks → files) and the role of file systems. |
| 2.3 | Explain how relational DBMSs use disk storage (pages, extents, buffers, WAL). |
| 2.4 | Identify the main responsibilities of a **Database Management System (DBMS)**. |
| 2.5 | Model a simple **relational schema** for books, authors, and genres. |
| 2.6 | Contrast **SQL** and **NoSQL** paradigms and articulate when each is appropriate. |
| 2.7 | List the **core differences** between MySQL and PostgreSQL (licensing, features, extensions, performance). |
| 2.8 | Install and configure a local development environment (code editor, terminal, Git). |
| 2.9 | Connect to a MySQL instance from JavaScript (Node.js or browser‑based client). |
| 2.10| Visualise the **query execution lifecycle** (parsing → planning → execution → result). |

---

## 3. Topic‑to‑Project Connection Map  

| Topic | Core Concept | Mini‑Project / Artefact (Digital Library) |
|-------|--------------|-------------------------------------------|
| **0.1 What is Data?** | Data vs. information, data types, relevance to libraries | Create a static **HTML page** (`catalog.html`) that lists a few sample books – the first “view” of the catalog. |
| **0.2 How Computers Store Data** | Binary representation, file hierarchy, metadata storage | Design a **folder structure** (`/library/assets/`, `/library/data/`) to hold book cover images and CSV/JSON metadata files. |
| **0.3 File Systems & How Databases Use Disk** | Files, directories, blocks, DB page I/O, buffering | Implement a simple **script** that copies the CSV metadata into a MySQL table, demonstrating file‑to‑DB ingestion. |
| **0.4 What is a DBMS?** | ACID, concurrency, catalog, query engine | **Install MySQL** locally (or via Docker) and create the first database `digital_library`. |
| **0.5 Relational Model** | Tables, rows, primary/foreign keys, normalization basics | Design the **ER diagram** and create tables: `books`, `authors`, `genres`, `book_authors`. |
| **0.6 SQL vs NoSQL — When to Use What** | Structured vs. document/graph stores, trade‑offs | Write a **SQL SELECT** and a comparable **MongoDB find** (conceptual) to illustrate differences. |
| **0.7 MySQL vs PostgreSQL — Core Differences** | Engine architecture, extensions, JSON support, GIS, licensing | Produce a **comparison table** (features, syntax quirks, community) and note which will be used for which feature of the library (e.g., PostgreSQL for full‑text search). |
| **0.8 Dev Environment Setup** | IDE/editor, terminal, Git, Docker, environment variables | Set up **VS Code**, install the **MySQL client**, initialise a **Git repo** (`digital-library/`). |
| **0.9 Connecting to Databases** | Connection strings, drivers, async queries | Write a **Node.js script** (`dbConnect.js`) that connects to MySQL and runs a simple `SELECT * FROM books;`. |
| **0.10 How SQL Queries Execute (Conceptual)** | Parser → Optimizer → Executor, indexes, query plans | Use **EXPLAIN** on a sample query and sketch the execution flow on a whiteboard or markdown diagram. |

---

## 4. Deliverables for Phase 0  

| Deliverable | Description | Acceptance Criteria |
|-------------|-------------|----------------------|
| **D0.1** `catalog.html` | Static HTML page displaying at least 5 books (title, author, cover). | Opens in a browser, uses semantic HTML, no broken images. |
| **D0.2** File‑system layout | Directory tree with `assets/` (covers) and `data/` (metadata CSV/JSON). | All files reachable via relative paths; README explains layout. |
| **D0.3** MySQL instance & `digital_library` DB | MySQL (or Docker‑based) running locally, database created. | `SHOW DATABASES;` lists `digital_library`. |
| **D0.4** Relational schema scripts | SQL file (`schema.sql`) that creates tables and constraints. | `source schema.sql;` runs without errors; `DESCRIBE books;` shows expected columns. |
| **D0.5** Connection demo script | JavaScript (`dbConnect.js`) that prints the row count of `books`. | Running `node dbConnect.js` outputs a numeric count. |
| **D0.6** Comparison artefacts | Markdown file (`db-comparison.md`) summarising MySQL vs PostgreSQL. | Contains at least 8 rows of side‑by‑side feature comparison. |
| **D0.7** Git repo | Repository with all above files, a `.gitignore`, and an initial commit. | `git log` shows at least one commit; remote (optional) URL provided. |

---

## 5. Assessment & Checkpoints  

| Checkpoint | Activity | Success Metric |
|------------|----------|----------------|
| **C0.1** (Day 2) | Peer review of `catalog.html` & folder layout. | All reviewers can open the page and locate assets. |
| **C0.2** (Day 4) | Run `schema.sql` and insert sample data. | `SELECT COUNT(*) FROM books;` returns ≥ 5. |
| **C0.3** (Day 6) | Demonstrate DB connection from JavaScript. | Console logs “Rows fetched: X”. |
| **C0.4** (Day 7) | Explain query execution using `EXPLAIN`. | Learner can identify “type”, “possible_keys”, “rows”. |
| **C0.5** (Day 8) | Submit the comparison markdown. | Instructor approves completeness & accuracy. |

---

## 6. Suggested Learning Resources  

| Type | Resource | Link / Reference |
|------|----------|-------------------|
| **Reading** | *Database System Concepts* – Chapter 1 (Data, DBMS) | https://doi.org/10.1016/B978-0-12-374514-1.00001-5 |
| **Video** | “How Computers Store Data” – CrashCourse Computer Science | https://youtu.be/8d6c9UeJ6aM |
| **Interactive** | SQLBolt – Intro to SQL (MySQL syntax) | https://sqlbolt.com |
| **Docs** | MySQL 8.0 Reference Manual – Installation & Basics | https://dev.mysql.com/doc/ |
| **Docs** | PostgreSQL 16 Documentation – Features Overview | https://www.postgresql.org/docs/current/ |
| **Tool** | Docker Hub – MySQL image | https://hub.docker.com/_/mysql |
| **Tool** | VS Code – “SQLTools” extension | https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools |
| **Cheat Sheet** | “SQL vs NoSQL” – DataCamp article | https://www.datacamp.com/tutorial/sql-vs-nosql |

---

## 7. Timeline (Suggested 2‑Week Sprint)

| Week | Day | Milestone |
|------|-----|-----------|
| **1** | 1‑2 | Complete **0.1** & **0.2** – HTML page & file‑system layout. |
|      | 3‑4 | Install MySQL, create DB, run **0.4** & **0.5** (schema). |
|      | 5‑6 | Populate sample data, test **0.9** connection script. |
|      | 7   | Draft **SQL vs NoSQL** and **MySQL vs PostgreSQL** comparison. |
| **2** | 8‑9 | Perform **0.10** query‑execution visualisation (EXPLAIN). |
|      |10‑11| Peer reviews, address feedback, polish README. |
|      |12   | Final commit, submit all deliverables, retrospective. |

---

## 8. Next Steps (Preview of Phase 1)

*Phase 1* will dive into **CRUD operations**, **joins**, and **basic indexing** while building the first dynamic catalog page that pulls data from MySQL.  Learners will also begin implementing **search** functionality and explore **parameterised queries** for security.

---

### Closing Note  

Phase 0 is intentionally lightweight: you are building the **foundation**—the mental model of data, the physical storage layout, and the tooling you’ll rely on for the entire Digital Library project.  Treat each deliverable as a **building block**; later phases will stack on top of them, turning a static page into a fully interactive, data‑driven library system. Happy learning!