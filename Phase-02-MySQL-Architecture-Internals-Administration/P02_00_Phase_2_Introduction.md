# Phase 2 – Building a Scalable E‑commerce Database with MySQL  

---

## 1. Project Context  

| **Item** | **Details** |
|----------|-------------|
| **Project** | **E‑commerce Database** |
| **Tagline** | *Building a scalable e‑commerce database with MySQL* |
| **Description** | Learners will design, implement, and optimise a production‑grade MySQL database for an e‑commerce application. The phase covers MySQL’s internal architecture, storage engine specifics, configuration, security, monitoring, backup/recovery, and JSON handling. By the end of the phase, participants will be able to build a robust, high‑performance data layer that can grow with real‑world traffic. |
| **Technology Stack** | MySQL 8.x, InnoDB storage engine, JSON data type, standard MySQL client tools (mysql, MySQL Workbench, CLI). |

---

## 2. Learning Objectives  

By the end of Phase 2 you will be able to:

1. **Explain** MySQL’s server architecture and the role of the InnoDB engine.  
2. **Provision** a MySQL instance, connect securely, and manage users/privileges.  
3. **Design** normalized tables using appropriate MySQL data types (including JSON).  
4. **Configure** MySQL (my.cnf / my.ini) for performance, security, and reliability.  
5. **Implement** logging, backup, and recovery strategies suitable for an e‑commerce workload.  
6. **Use** the Performance Schema and other monitoring tools to diagnose and tune queries.  
7. **Integrate** JSON columns to store flexible product attributes while preserving queryability.  

---

## 3. Topics & Direct Project Connections  

| **Topic Code** | **Topic Title** | **Project‑Level Activity** |
|----------------|----------------|----------------------------|
| **2.1** | MySQL Architecture | Set up a MySQL server and connect to it using a database client |
| **2.2** | InnoDB Architecture Deep Dive | Design an InnoDB table to store e‑commerce product information |
| **2.3** | MySQL Data Types Deep Dive | Create a table with various MySQL data types to store product reviews |
| **2.4** | MySQL Configuration (my.cnf / my.ini) | Configure MySQL using my.cnf to optimise database performance |
| **2.5** | MySQL Users, Privileges & Security | Create a MySQL user and grant privileges to perform CRUD operations |
| **2.6** | MySQL Databases, Schemas & Metadata | Design and create a database schema to store customer information |
| **2.7** | MySQL Logging | Configure MySQL logging to track database activity |
| **2.8** | MySQL Backup & Recovery | Set up automated backups and recovery procedures for the database |
| **2.9** | MySQL Performance Schema & Monitoring | Use the Performance Schema to monitor database performance and optimise queries |
| **2.10** | MySQL JSON Support | Implement JSON support to store and retrieve product attributes |

---

## 4. Detailed Topic Summaries  

| **Topic** | **Key Concepts** | **Hands‑On Lab** |
|-----------|------------------|------------------|
| **2.1 MySQL Architecture** | Server layers (connection, query parser, optimizer, storage engine), thread handling, buffer pools. | Install MySQL on a VM/Docker, start the service, connect via `mysql` client and MySQL Workbench. |
| **2.2 InnoDB Architecture** | Pages, extents, redo log, undo log, MVCC, row‑level locking, foreign‑key enforcement. | Create `products` table with primary key, indexes, and foreign keys; examine `SHOW ENGINE INNODB STATUS`. |
| **2.3 Data Types Deep Dive** | Numeric, temporal, string, spatial, JSON, ENUM/SET, binary. | Build `product_reviews` table using `TINYINT`, `DECIMAL`, `DATETIME`, `TEXT`, `JSON`; insert sample rows. |
| **2.4 Configuration (my.cnf)** | `innodb_buffer_pool_size`, `query_cache_type`, `max_connections`, `log_bin`, `slow_query_log`. | Edit `my.cnf`, restart MySQL, verify changes with `SHOW VARIABLES`. |
| **2.5 Users, Privileges & Security** | `CREATE USER`, `GRANT`, role‑based access, password policies, SSL/TLS. | Create `ecom_app` user, grant `SELECT, INSERT, UPDATE, DELETE` on the e‑commerce schema, test with a separate client session. |
| **2.6 Databases, Schemas & Metadata** | `CREATE DATABASE`, `USE`, information_schema, `SHOW CREATE TABLE`. | Design `ecom` schema containing `customers`, `orders`, `order_items`; generate ER diagram via Workbench. |
| **2.7 Logging** | Error log, general query log, slow query log, binary log. | Enable the slow‑query log, run a deliberately slow query, inspect the log file. |
| **2.8 Backup & Recovery** | Logical (`mysqldump`), physical (`xtrabackup`), point‑in‑time recovery, `binlog`. | Schedule nightly `mysqldump` backups, simulate a crash, restore from backup. |
| **2.9 Performance Schema & Monitoring** | Enabling the schema, instruments, consumers, `sys` schema, `EXPLAIN ANALYZE`. | Capture query latency stats, identify a bottleneck query, rewrite it using indexes. |
| **2.10 JSON Support** | JSON data type, functions (`JSON_EXTRACT`, `JSON_ARRAYAGG`, `JSON_TABLE`), indexing JSON columns. | Add `attributes` JSON column to `products`, store size/color options, query with `JSON_VALUE`. |

---

## 5. Prerequisites  

- Completion of **Phase 1** (basic SQL syntax, simple SELECT/INSERT/UPDATE/DELETE, primary‑key design).  
- Local development environment with Docker or a VM capable of running MySQL 8.x.  
- Familiarity with a command‑line interface and a graphical client (e.g., MySQL Workbench).  

---

## 6. Expected Deliverables  

1. **MySQL Server Setup** – documented `my.cnf`, connection instructions, and a screenshot of a successful client connection.  
2. **InnoDB‑Based Product Table** – DDL script (`CREATE TABLE products …`) and sample data load.  
3. **Product Reviews Table** – DDL using a variety of data types, plus sample inserts.  
4. **Security Configuration** – SQL script creating the `ecom_app` user with least‑privilege grants.  
5. **Schema Diagram** – ER diagram (PDF/PNG) showing all tables and relationships.  
6. **Logging & Backup Scripts** – configuration snippets and a backup‑restore demonstration video or log.  
7. **Performance Report** – screenshots/queries from Performance Schema showing before/after optimisation.  
8. **JSON Attribute Implementation** – DDL, sample JSON payloads, and query examples.  

All deliverables are to be stored in a Git repository under the `phase‑2/` folder, with a `README.md` that explains how to reproduce the environment.

---

## 7. Assessment & Success Criteria  

| **Criterion** | **How It Is Measured** |
|---------------|------------------------|
| Server installation & connectivity | Ability to start MySQL and connect from two different clients. |
| Correct InnoDB table design | Table passes `SHOW CREATE TABLE` verification and enforces foreign‑key constraints. |
| Appropriate data‑type usage | No warnings/errors on `INSERT` of sample data; data types match use‑case. |
| Configuration optimisation | `my.cnf` reflects at least three performance‑related settings; `SHOW VARIABLES` confirms them. |
| Security & privileges | `ecom_app` can only perform CRUD on its schema; attempts to access other schemas are denied. |
| Backup & recovery | Successful restoration of a dropped table from the most recent backup. |
| Performance tuning | Identified slow query is reduced by ≥30 % after optimisation. |
| JSON handling | JSON column stores valid documents; queries retrieve specific attributes correctly. |

A **graded rubric** (0‑100 pts) will be applied, with each deliverable weighted equally.

---

## 8. Suggested Learning Resources  

| **Resource** | **Link** | **Why It Helps** |
|--------------|----------|------------------|
| MySQL 8.0 Reference Manual – Architecture | https://dev.mysql.com/doc/refman/8.0/en/architecture.html | Authoritative description of server components. |
| InnoDB Storage Engine Documentation | https://dev.mysql.com/doc/refman/8.0/en/innodb-storage-engine.html | Deep dive into pages, logs, and MVCC. |
| MySQL Performance Schema Guide | https://dev.mysql.com/doc/refman/8.0/en/performance-schema.html | Practical examples of monitoring. |
| “High Performance MySQL” (3rd ed.) – O'Reilly | ISBN 978‑1492052509 | Covers configuration, indexing, and JSON. |
| MySQL Workbench Manual – Modeling | https://dev.mysql.com/doc/workbench/en/ | Step‑by‑step schema design and ER diagram generation. |
| Percona XtraBackup Documentation | https://www.percona.com/doc/percona-xtrabackup/LATEST/ | Alternative physical backup method. |
| Official MySQL JSON Functions | https://dev.mysql.com/doc/refman/8.0/en/json-functions.html | Syntax and examples for JSON manipulation. |

---

## 9. Timeline (Suggested)  

| **Week** | **Focus** |
|----------|-----------|
| 1 | Install MySQL, explore architecture, connect with clients. |
| 2 | InnoDB deep dive, create product table, review storage details. |
| 3 | Data‑type exploration, build product_reviews table. |
| 4 | Server configuration (`my.cnf`) and performance tuning basics. |
| 5 | Users, roles, and security hardening. |
| 6 | Schema design for customers & orders; generate ER diagram. |
| 7 | Enable and test logging (general, slow, binary). |
| 8 | Backup strategy: logical & physical, recovery drills. |
| 9 | Performance Schema monitoring, query optimisation. |
| 10 | JSON column design, queries, indexing, final integration. |
| 11‑12 | Consolidate deliverables, peer review, final assessment. |

---

## 10. Closing Note  

Phase 2 is the **engine room** of the e‑commerce database project. Mastery of MySQL’s internals, configuration knobs, and operational best practices will give you the confidence to run a production‑grade data platform. Treat each lab as a building block; the artifacts you produce here will be the foundation for the advanced analytics and scaling topics that follow in later phases.  

Happy coding, and may your queries always be fast!