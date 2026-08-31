## Overview
Phase 0 establishes the foundational knowledge and technical environment required to design and operate NexaBank's core banking database. Learners explore core data principles, storage mechanics, relational modeling, and DBMS selection while setting up their development environment. This phase ensures a shared understanding of how financial transactions demand strict consistency, immutability, and ACID compliance before implementing the schema in subsequent phases.

## Phase Objectives
- Model core banking entities (customers, accounts) and their relationships for an immutable transaction ledger
- Implement binary storage and file system principles for persistent data storage
- Design relational schemas with referential integrity constraints
- Justify SQL/PostgreSQL selection for high-concurrency financial operations
- Configure a PostgreSQL environment and establish secure database connections
- Analyze query execution concepts for future optimization

## Topic-to-Project Connection Map
| Topic                          | Description                                                                 | Connection to NexaBank — Database Engineering Track                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| 0.1 What is Data?              | Model entities by defining critical attributes and relationships            | Define `customers` and `accounts` tables with attributes ensuring accurate transaction attribution                  |
| 0.2 How Computers Store Data   | Implement binary storage for records on disk                                | Design storage for append-only `transactions` ledger requiring sequential write optimization                        |
| 0.3 File Systems & Databases   | Configure file layouts for relational tables and logs                       | Optimize PostgreSQL file structure for high-volume transaction writes and audit log immutability                   |
| 0.4 What is a DBMS?            | Select DBMS enforcing ACID compliance                                       | Choose PostgreSQL to guarantee atomic deposits/withdrawals in `transactions` table                                  |
| 0.5 Relational Model           | Design schemas with primary/foreign keys                                    | Create `customers → accounts → transactions` relationships with cascading integrity constraints                    |
| 0.6 SQL vs NoSQL               | Justify SQL for strict consistency                                          | SQL chosen over NoSQL for serializable isolation in concurrent money movements                                      |
| 0.7 MySQL vs PostgreSQL        | Benchmark DBMS options                                                      | Select PostgreSQL for MVCC (Multi-Version Concurrency Control) and JSON audit logs                                  |
| 0.8 Dev Environment Setup      | Install PostgreSQL, tools, and initialize database                          | Create 'nexabank' database instance hosting core schema tables                                                     |
| 0.9 Connecting to Databases    | Write secure client connection scripts                                      | Implement Python/Node.js connectors for transactional operations with SSL encryption                                |
| 0.10 How SQL Queries Execute   | Analyze query plans for index optimization                                  | Identify indexing needs for balance derivation scans on `accounts` and `transactions`                              |

## Phase Outcome
- Designed a conceptual relational schema for core banking entities
- Configured a PostgreSQL development environment with 'nexabank' database
- Written secure database connection scripts in a modern programming language
- Developed optimized file system and indexing strategies for transaction ledgers
- Created a DBMS selection rationale document for stakeholders

## Next Steps
In Phase 1, learners will apply this foundation to physically design the core schema, implementing normalization rules, data types, and constraints. The focus shifts to ensuring referential integrity, data type precision for financial values, and initial indexing strategies for the immutable transaction ledger.