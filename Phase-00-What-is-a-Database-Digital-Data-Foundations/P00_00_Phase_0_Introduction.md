## Overview
Phase 0 establishes the essential theoretical and practical foundation for database engineering in NexaBank. It demystifies core concepts like structured data, physical storage, and relational modeling while guiding learners through critical architectural decisions (SQL vs NoSQL, PostgreSQL vs MySQL). This phase ensures learners understand both the "what" and "why" behind NexaBank's database design choices before implementation begins.

## Phase Objectives
- Understand how to model core banking entities (customers, accounts, transactions) as structured data
- Grasp physical storage fundamentals (binary formats, disk blocks) and database file organization
- Compare SQL/NoSQL paradigms and justify PostgreSQL for ACID-compliant banking operations
- Design normalized relational schemas with primary/foreign keys
- Set up a PostgreSQL development environment and establish application connectivity
- Analyze basic SQL query execution concepts for ledger-based balance calculations

## Topic-to-Project Connection Map
| Topic                          | Description                                                                 | Connection to NexaBank                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| 0.1 What is Data?              | Define structured data for banking entities                                 | Model `customers`, `accounts`, and `transactions` as foundational data structures     |
| 0.2 How Computers Store Data   | Binary storage (bytes/blocks) for customer/account records                  | Map physical storage requirements for NexaBank's immutable transaction ledger         |
| 0.3 File Systems & Databases   | Database files (tables/indexes) → file system directories/blocks            | Design on-disk layout for NexaBank's append-only `transactions` table                 |
| 0.4 What is a DBMS?            | Transactional integrity and concurrency control requirements                | Select PostgreSQL to manage atomic transfers and prevent overdrafts                   |
| 0.5 Relational Model           | Design normalized tables with PKs/FKs                                       | Create Phase 0 schema: `customers`, `accounts`, `transactions`                        |
| 0.6 SQL vs NoSQL               | ACID compliance vs flexibility tradeoffs                                    | Justify SQL for double-entry accounting and complex balance joins                      |
| 0.7 MySQL vs PostgreSQL        | Advanced features comparison (concurrency, JSON)                            | Implement PostgreSQL for MVCC and audit trail JSON support                             |
| 0.8 Dev Environment Setup      | PostgreSQL installation and configuration                                   | Prepare local environment for NexaBank schema development                              |
| 0.9 Connecting to Databases    | Application-database linkage (Python/JDBC)                                  | Enable future frontends to interact with NexaBank's core ledger                       |
| 0.10 How SQL Queries Execute  | Conceptual query planning for ledger aggregation                            | Optimize balance calculations from append-only `transactions` table                    |

## Phase Outcome
- Foundational relational schema design for core banking entities
- PostgreSQL DBMS selected and justified with environment configured
- Application-database connectivity established
- Physical storage and query execution concepts applied to NexaBank's ledger pattern
- Clear rationale for SQL/PostgreSQL over alternatives in financial contexts

## Next Steps
Phase 1 shifts from foundation to implementation: learners will deploy the Phase 0 schema, implement atomic transaction mechanics, and introduce concurrency controls to prevent race conditions during money movements.