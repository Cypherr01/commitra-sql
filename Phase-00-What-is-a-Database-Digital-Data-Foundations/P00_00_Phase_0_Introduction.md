## Overview
Phase 0 establishes the essential theoretical and conceptual foundations required before writing any SQL code or designing databases. It demystifies core data principles, storage mechanisms, and database technologies to ensure learners understand *why* and *how* data is structured and managed in the Commerce Insight Hub. This phase bridges abstract concepts with the project's technical requirements, preparing learners to make informed decisions during schema design and implementation.

## Phase Objectives
- Define core data entities (users, products, orders, inventory) and their attributes
- Explain how computers represent and store data at the binary level
- Analyze disk storage strategies for database optimization
- Justify the selection of PostgreSQL as the DBMS for the project
- Model relational databases using primary/foreign keys and normalization
- Compare SQL vs. NoSQL databases and MySQL vs. PostgreSQL
- Set up a local PostgreSQL development environment
- Create scripts to connect applications with PostgreSQL databases
- Conceptually understand SQL query execution for performance optimization

## Topic-to-Project Connection Map
| Topic                          | Description                                                                 | Connection to Commerce Insight Hub                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| 0.1 What is Data?              | Learners define core entities (users, products, orders, inventory) and their attributes. | Establishes foundational data model for the e-commerce platform's key business objects.            |
| 0.2 How Computers Store Data   | Learners map entity attributes to binary storage formats.                   | Ensures proper data type selection (e.g., integers for product IDs) in PostgreSQL tables.          |
| 0.3 File Systems & Databases    | Learners design disk storage strategies for database files.                 | Optimizes storage for high-volume transactional data (orders, inventory updates) in AWS Redshift.  |
| 0.4 What is a DBMS?            | Learners select PostgreSQL based on ACID compliance and features.           | Supports transactional integrity for sales data and complex analytics required by retail analysts. |
| 0.5 Relational Model           | Learners model entity relationships using keys and normalization.           | Creates efficient schema for joining sales, user behavior, and inventory data in dashboards.       |
| 0.6 SQL vs NoSQL               | Learners justify SQL for structured data and complex joins.                 | Enables complex queries for predictive insights vs. NoSQL's flexibility for unstructured data.     |
| 0.7 MySQL vs PostgreSQL        | Learners choose PostgreSQL for JSON/geospatial support.                     | Supports future analytics needs like location-based marketing and semi-structured user data.       |
| 0.8 Dev Environment Setup      | Learners install PostgreSQL locally.                                        | Prepares environment for schema implementation and testing before cloud deployment.                 |
| 0.9 Connecting to Databases    | Learners write connection scripts for application integration.              | Enables data pipeline integration with Python/Airflow for ETL processes.                           |
| 0.10 SQL Query Execution        | Learners optimize structures using query execution concepts.                | Informs indexing strategies for real-time dashboard performance with large datasets.               |

## Phase Outcome
- A normalized entity-relationship diagram for core e-commerce domains
- Local PostgreSQL development environment with verified connectivity
- Connection scripts for integrating PostgreSQL with applications
- Indexing and storage optimization strategies based on query execution understanding
- Justification document comparing PostgreSQL to alternatives for project requirements

## Next Steps
With foundational knowledge and environments established, Phase 1 will shift focus to **database schema design** and **core SQL implementation**. Learners will translate conceptual models into physical PostgreSQL tables, implement constraints, and write foundational queries to ingest and relate sales, user, and inventory data for the Commerce Insight Hub.