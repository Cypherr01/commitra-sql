# Phase 4 – Advanced Schema Design & Optimization  
**Project‑Anchored SQL Learning Roadmap (MySQL / PostgreSQL)**  

---

## 1. Project Context  

| Item | Details |
|------|---------|
| **Project** | **E‑Commerce Database Design** |
| **Tagline** | *Design a schema for an e‑commerce platform* |
| **Description** | Learners will design a relational database that supports **orders, products, customers, and inventory**. The work will require applying ER‑modeling, normalization, primary‑key strategies, foreign‑key enforcement, index design, common schema patterns, and the identification & remediation of schema anti‑patterns. |
| **Technology Stack** | SQL (MySQL / PostgreSQL) – ER‑diagram tools (MySQL Workbench, pgModeler, dbdiagram.io, etc.) |

---

## 2. Phase Overview  

Phase 4 moves the learner from a functional schema to a **robust, high‑performance, and maintainable** design. Seven tightly‑coupled topics are covered; each directly contributes to the e‑commerce project.

| Topic | Core Skill | Project‑Level Deliverable |
|-------|------------|---------------------------|
| **4.1 Entity‑Relationship Modeling** | Create a complete ER diagram (entities, attributes, relationships, cardinalities). | ER diagram that includes **Customers, Orders, Order_Items, Products, Inventory, Categories, Payments, Shipping** (and any optional supporting entities). |
| **4.2 Normalization** | Apply 1NF‑3NF (and BCNF where appropriate) to eliminate redundancy. | Normalized logical model with clear primary‑key/foreign‑key placement; justification of each normal form decision. |
| **4.3 Primary‑Key Design Strategies** | Choose surrogate vs. natural keys, composite keys, UUIDs, and auto‑increment strategies. | Primary‑key definitions for every table, with rationale (e.g., `customer_id BIGINT AUTO_INCREMENT`, `order_id UUID`). |
| **4.4 Foreign Keys & Referential Integrity** | Define FK constraints, cascade actions, and deferred constraints (PostgreSQL). | All relationships enforced by FK constraints; scripts for both MySQL and PostgreSQL syntax. |
| **4.5 Indexes in Schema Design** | Identify covering, composite, partial, and expression indexes; understand index selectivity. | Index creation statements that accelerate the most common queries (e.g., order lookup by customer, product search by SKU, inventory stock‑level checks). |
| **4.6 Common Schema Patterns** | Implement star‑schema / snowflake for reporting, bridge tables for many‑to‑many, and audit tables. | A reporting schema (fact + dimension tables) derived from the operational model, ready for OLAP queries. |
| **4.7 Schema Anti‑Patterns** | Detect duplication, “NULL‑filled” tables, over‑indexed tables, and “one‑to‑many as many‑to‑many”. | Refactored DDL that removes identified anti‑patterns, with before/after comparison and performance impact notes. |

---

## 3. Learning Objectives  

By the end of Phase 4 you will be able to:

1. **Model** a complete e‑commerce domain using a professional ER diagram.  
2. **Normalize** the model to at least **3NF**, explaining why each table meets the chosen normal form.  
3. **Select** and justify primary‑key strategies (surrogate vs. natural, UUID vs. auto‑increment).  
4. **Implement** foreign‑key constraints that enforce referential integrity, including appropriate `ON UPDATE/DELETE` actions.  
5. **Design** and apply indexes that materially improve query response times for realistic workloads.  
6. **Apply** common schema patterns (star schema, bridge tables, audit trails) to support analytics and auditability.  
7. **Identify** and **remediate** schema anti‑patterns, documenting the before‑and‑after impact on storage and performance.  

---

## 4. Deliverables for Phase 4  

| Deliverable | Format | Success Criteria |
|-------------|--------|------------------|
| **ER Diagram** | PNG / PDF (or live model in MySQL Workbench/pgModeler) | All required entities & relationships shown; cardinalities correct. |
| **Normalized Logical Model** | Markdown table or spreadsheet | Each table listed with PK, FK, and normal‑form justification. |
| **DDL Scripts** | `.sql` files (MySQL & PostgreSQL) | Scripts run without errors; constraints and indexes present. |
| **Index Rationale Document** | Markdown | For each index: query pattern, selectivity estimate, and expected I/O benefit. |
| **Reporting Schema (Star)** | Diagram + DDL | Fact table (`sales_fact`) and dimension tables (`dim_customer`, `dim_product`, `dim_date`, etc.). |
| **Anti‑Pattern Refactor Report** | Markdown | List of identified anti‑patterns, refactor steps, and before/after performance metrics (e.g., query time, row count). |
| **Reflection Blog Post** | 300‑500 word post | Learner explains the design decisions, challenges faced, and lessons learned. |

---

## 5. Suggested Workflow  

1. **Sketch** the high‑level ER diagram on paper or a digital tool.  
2. **Iterate** with normalization checks: apply 1NF → 2NF → 3NF (and BCNF if needed).  
3. **Choose** primary keys; add surrogate keys where natural keys are volatile or composite.  
4. **Add** foreign‑key constraints; test referential actions with sample data.  
5. **Profile** typical queries (order lookup, product search, inventory audit) and **design** indexes accordingly.  
6. **Create** a star schema for reporting; map operational tables to fact/dimension tables.  
7. **Audit** the schema for anti‑patterns; refactor and re‑run performance tests.  
8. **Document** every step; commit DDL and documentation to a version‑controlled repository.  

---

## 6. Additional Resources  

| Resource | Link |
|----------|------|
| **ER Diagram Tools** | MySQL Workbench, pgModeler, dbdiagram.io, Lucidchart |
| **Normalization Primer** | <https://www.databasejournal.com/features/mysql/normalization-in-mysql.html> |
| **Primary‑Key Strategies** | <https://www.postgresql.org/docs/current/datatype-numeric.html#DATATYPE-INT> |
| **Foreign‑Key & Referential Integrity** | MySQL: <https://dev.mysql.com/doc/refman/8.0/en/create-table-foreign-keys.html>  <br> PostgreSQL: <https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-FK> |
| **Index Design** | MySQL: <https://dev.mysql.com/doc/refman/8.0/en/optimization-indexes.html>  <br> PostgreSQL: <https://www.postgresql.org/docs/current/indexes.html> |
| **Star Schema Overview** | Kimball, *The Data Warehouse Toolkit* (Chapter 2) |
| **Schema Anti‑Patterns** | <https://www.databasestar.com/database-anti-patterns/> |

---

## 7. Assessment & Feedback  

- **Automated Checks** – Run the supplied test suite (`schema_test.sql`) against both MySQL and PostgreSQL instances. All tests must pass.  
- **Peer Review** – Exchange ER diagrams and DDL with a fellow learner; provide at least three constructive comments.  
- **Instructor Review** – Submit all deliverables via the LMS; expect a rubric‑based feedback focusing on correctness, justification, and performance impact.  

---

## 8. Next Steps  

1. **Begin** with Topic 4.1 (Entity‑Relationship Modeling).  
2. **Progress** sequentially through 4.2 → 4.7, ensuring each deliverable is version‑controlled before moving on.  
3. **Iterate**: after completing 4.5 (Indexes), re‑run performance tests on earlier queries; adjust as needed.  
4. **Finalize** the Phase 4 portfolio and prepare for Phase 5 (Advanced Querying & Transaction Management).  

---

**You now have a complete, structured roadmap for Phase 4.** Use it as your checklist, reference, and reporting template as you transform the e‑commerce conceptual model into a production‑ready relational schema. Happy modeling!