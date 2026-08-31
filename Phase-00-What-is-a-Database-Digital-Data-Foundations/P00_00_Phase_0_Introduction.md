## Overview
Phase 0 establishes the foundational knowledge and technical setup required to design and operate a database for NexaBank, a high-stakes financial system. This phase demystifies core database concepts, storage mechanisms, and relational principles while setting up the development environment. By grounding learners in the unique demands of banking data—such as transactional integrity, auditability, and concurrency control—it prepares them to tackle the engineering challenges of subsequent phases. The goal is to ensure learners understand *why* databases work the way they do before building or optimizing them.

## Phase Objectives
- Define atomic data units and model foundational entities (customers, accounts) using the core schema.
- Simulate binary storage and file-based transaction logs to grasp durability and recovery mechanisms.
- Install and configure PostgreSQL as the DBMS, justified for its ACID compliance and advanced concurrency features.
- Design relational tables with primary/foreign keys to enforce data integrity in financial operations.
- Compare SQL/NoSQL and MySQL/PostgreSQL to contextualize PostgreSQL’s suitability for NexaBank’s audit and transactional needs.
- Set up a local development environment and programmatically connect to the database using Python.
- Analyze basic SQL query execution plans to introduce indexing and join strategies.

## Topic-to-Project Connection Map
| Topic                     | Description                                                                 | Connection to NexaBank — Database Engineering Track                                                                 |
|---------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| 0.1 What is Data?         | Define atomic data units (e.g., `customer_id`, `account_number`).          | Establishes precise data modeling for entities like `customers` and `accounts`, ensuring unambiguous identifiers in financial transactions. |
| 0.2 How Computers Store Data | Simulate binary storage of records.                                        | Builds intuition for persistent storage of sensitive data (e.g., encrypted account details) and ledger immutability. |
| 0.3 File Systems & How Databases Use Disk | Implement file-based transaction logs.                                     | Directly mirrors NexaBank’s append-only `transactions` ledger and `audit_log`, critical for recovery and compliance. |
| 0.4 What is a DBMS?       | Install PostgreSQL for ACID-compliant operations.                          | Ensures atomicity in money transfers and loan disbursements, preventing partial transactions.                        |
| 0.5 Relational Model      | Design tables with primary/foreign keys.                                   | Enforces referential integrity between `customers` → `accounts` → `transactions`, eliminating orphaned records.     |
| 0.6 SQL vs NoSQL          | Justify SQL for transactional consistency.                                 | Guarantees serializable isolation for concurrent deposits/withdrawals, avoiding race conditions.                     |
| 0.7 MySQL vs PostgreSQL   | Select PostgreSQL for MVCC and JSON support.                               | Enables non-blocking reads during EMI debits and flexible audit logging of complex loan workflows.                  |
| 0.8 Dev Environment Setup | Configure local PostgreSQL instance and `nexabank` database.               | Creates a sandbox for prototyping the core schema and testing financial operations.                                  |
| 0.9 Connecting to Databases | Write Python script with `psycopg2` for schema creation.                   | Automates deployment of tables like `loans` and `cheque_book_requests`, ensuring reproducibility.                    |
| 0.10 How SQL Queries Execute | Diagram execution plans for transaction queries.                          | Optimizes indexing strategies for high-volume `transactions` table joins, essential for real-time balance calculations. |

## Phase Outcome
By completing Phase 0, learners will have:
- Modeled the `customers` and `accounts` tables with proper relational constraints.
- Implemented a file-based transaction log simulation to understand durability.
- Installed PostgreSQL and created the `nexabank` database with the core schema.
- Written a Python script to connect to the database and execute schema-creation SQL.
- Justified PostgreSQL’s selection over alternatives for NexaBank’s requirements.
- Analyzed a basic query execution plan to identify indexing and join opportunities.

## Next Steps
Phase 1 shifts focus to advanced schema design, normalization, and transaction management, leveraging the foundation built here. Learners will extend the core schema to handle complex banking workflows like loan origination and cheque processing while ensuring atomicity and isolation. The environment and conceptual clarity from Phase 0 enable tackling these real-world engineering challenges.