# Phase 0 – Foundations of Data & Databases  
**Project:** *Digital Library* – *“Building a catalog system for a fictional university library”*  

---

## 1. Phase Overview  

Phase 0 establishes the conceptual and technical groundwork required to design, build, and query a relational database for the Digital Library.  Learners will move from “what is data?” to a working development environment that can connect to MySQL and PostgreSQL.  All activities are tied directly to small, concrete deliverables that will later become components of the full‑stack catalog system.

---

## 2. Learning Objectives  

By the end of this phase you will be able to:

| # | Objective |
|---|-----------|
| 2.1 | Define **data**, **metadata**, and explain why structured data matters for a library catalog. |
| 2.2 | Describe how computers store data on disk (bits, bytes, blocks, files). |
| 2.3 | Explain the role of a **file system** and how a DBMS leverages disk storage. |
| 2.4 | Identify the core responsibilities of a **Database Management System (DBMS)**. |
| 2.5 | Model library entities (books, authors, genres) using the **relational model** (tables, rows, primary/foreign keys). |
| 2.6 | Contrast **SQL** vs **NoSQL** and articulate scenarios where each is appropriate. |
| 2.7 | List the **key differences** between MySQL and PostgreSQL (data types, extensions, licensing, performance characteristics). |
| 2.8 | Install and configure a **local development environment** (code editor, terminal, Git). |
| 2.9 | Connect to a MySQL (and optionally PostgreSQL) instance from JavaScript/Node.js or a client GUI. |
| 2.10| Visualize the **query execution lifecycle** (parsing → planning → execution) and recognise basic optimisation concepts. |

---

## 3. Topics & Mini‑Projects  

| Topic (Map ID) | Brief Description | Project‑Level Activity |
|----------------|-------------------|------------------------|
| **0.1 What is Data?** | Data as raw facts; metadata as descriptive information; why libraries need structured data. | Create a simple **HTML page** (`catalog.html`) that lists a few hard‑coded books to illustrate “catalog data”. |
| **0.2 How Computers Store Data** | Binary representation, storage media, file allocation tables. | Sketch a **folder hierarchy** for the library (e.g., `/books/`, `/covers/`, `/metadata/`). |
| **0.3 File Systems & How Databases Use Disk** | Files vs pages, buffering, write‑ahead logging. | Build a **mock file‑system** (plain folders) and write a script that copies a JSON book record into a file – later we’ll replace this with DB storage. |
| **0.4 What is a DBMS?** | DBMS services: CRUD, concurrency, recovery, security. | Install **MySQL Community Server** locally and create a test database `digital_library`. |
| **0.5 Relational Model** | Tables, rows, primary keys, foreign keys, normalization basics. | Design an **ER diagram** (books ↔ authors ↔ genres) and translate it into `CREATE TABLE` statements. |
| **0.6 SQL vs NoSQL — When to Use What** | Structured vs document/graph stores, ACID vs BASE, query patterns. | Write two simple queries: one in **SQL** (`SELECT * FROM books WHERE title LIKE '%SQL%';`) and one in a NoSQL‑style pseudo‑code (e.g., MongoDB find). |
| **0.7 MySQL vs PostgreSQL — Core Differences** | Engine architecture, data‑type richness, extensions (PostGIS, JSONB), replication, licensing. | Populate a **comparison matrix** and discuss which engine fits the Digital Library’s needs (e.g., complex reporting → PostgreSQL). |
| **0.8 Dev Environment Setup** | VS Code, terminal, Git, Docker (optional). | Clone the starter repo, initialise a Git repo, and verify `mysql -u root -p` works. |
| **0.9 Connecting to Databases** | Connection strings, drivers (Node‑MySQL, pg), handling credentials. | Write a **JavaScript snippet** that connects to MySQL, runs a `SELECT` and logs results to the console. |
| **0.10 How SQL Queries Execute (Conceptual)** | Parser → Optimizer → Executor, indexes, query plans. | Use `EXPLAIN` on a sample query and interpret the output; sketch the execution flow diagram. |

---

## 4. Deliverables for Phase 0  

1. **`catalog.html`** – static page displaying a mock book list.  
2. **Folder structure diagram** (markdown or image) showing where book files and metadata will live.  
3. **ER diagram** (draw.io, Lucidchart, or hand‑drawn) for the relational model.  
4. **SQL schema file** (`schema.sql`) containing `CREATE TABLE` statements for books, authors, genres, and linking tables.  
5. **Git repository** initialized with a `README.md` that documents the environment setup steps.  
6. **Connection demo script** (`db-connect.js` or `db-connect.py`) that prints a row from the `books` table.  
7. **Comparison matrix** (markdown table) of MySQL vs PostgreSQL features.  
8. **`EXPLAIN` analysis** screenshot or text for a sample query.  

All deliverables should be committed to the repository with clear commit messages (e.g., “Add initial HTML catalog page”, “Create relational schema”).  

---

## 5. Suggested Resources  

| Type | Title / Link |
|------|--------------|
| **Reading** | *Database System Concepts* – Chapter 1 “Data, Information, and Databases”. |
| **Video** | “How Computers Store Data” – Khan Academy (YouTube). |
| **Docs** | MySQL 8.0 Reference Manual – *Getting Started*. |
| **Docs** | PostgreSQL 16 Documentation – *Introduction*. |
| **Tool** | VS Code – *SQLTools* extension for query editing. |
| **Cheat Sheet** | “SQL vs NoSQL – Quick Reference” (downloadable PDF). |

---

## 6. Assessment & Checkpoints  

| Checkpoint | What to Submit | Success Criteria |
|------------|----------------|------------------|
| **0.1 – Data & HTML** | `catalog.html` + screenshot in README | Page loads locally, displays at least 3 books. |
| **0.4 – DBMS Install** | `mysql --version` output in README | MySQL 8+ is installed and reachable. |
| **0.5 – Schema** | `schema.sql` + ER diagram | Schema creates without errors; foreign keys correctly defined. |
| **0.9 – Connection** | `db-connect.js` output log | Script connects, runs a SELECT, and prints a row. |
| **0.10 – Explain** | `EXPLAIN` output + brief interpretation | Shows use of index (if created) and logical plan steps. |

A **peer review** session (optional) can be scheduled after all deliverables are pushed, where teammates comment on each other’s README and code quality.

---

## 7. Next Steps (Preview of Phase 1)

*Write your first SELECT/INSERT/UPDATE/DELETE statements.*  
*Begin populating the `books` table with real sample data.*  
*Introduce basic indexing and query optimisation.*  

Phase 1 will turn the static schema into a functional data store that powers the dynamic catalog UI.

---

### Quick Recap  

| Goal | How We Achieve It |
|------|-------------------|
| Understand data fundamentals | 0.1, 0.2, 0.3 |
| Grasp DBMS purpose & relational theory | 0.4, 0.5 |
| Choose the right SQL engine | 0.6, 0.7 |
| Set up a reproducible dev environment | 0.8 |
| Connect code to the database | 0.9 |
| Visualise query execution | 0.10 |

With these foundations in place, you’ll be ready to start building the **Digital Library** back‑end in the next phase. Happy learning!