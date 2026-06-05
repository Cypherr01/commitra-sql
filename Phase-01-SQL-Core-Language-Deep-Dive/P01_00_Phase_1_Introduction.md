# **Phase 1 Introduction: SQL E-Commerce Database**  
**Project Context**: SQL E-commerce Database  
**Tagline**: Building a functional e-commerce database using SQL  
**Duration**: 4 Weeks  
**Target Stack**: SQLite (local DBMS)  

---

## **Overview**  
Phase 1 introduces learners to foundational SQL concepts required to design, populate, and query a functional e-commerce database. This phase focuses on **database schema design**, **data manipulation**, and **basic query writing** to establish a robust foundation for managing an e-commerce platform. By the end of this phase, learners will have created a database schema for products, customers, orders, and payment methods, populated it with sample data, and written queries to retrieve and analyze core business data.  

Key topics include:  
- Designing tables with appropriate data types and constraints.  
- Inserting, updating, and deleting data.  
- Writing `SELECT` queries with filtering, aggregation, and joins.  

This phase aligns with the project’s goal of teaching SQL through hands-on practice, ensuring learners can apply concepts to real-world e-commerce scenarios.  

---

## **Learning Objectives**  
By the end of Phase 1, learners will be able to:  
1. **Design a relational database schema** for an e-commerce platform using DDL (Data Definition Language).  
2. **Define data types and constraints** to ensure data integrity.  
3. **Insert, update, and delete data** using DML (Data Manipulation Language).  
4. **Write core SQL queries** (`SELECT`, `WHERE`, `GROUP BY`, `JOIN`) to retrieve and analyze data.  
5. **Apply filtering and aggregation** to generate insights like total revenue and customer statistics.  

---

## **Phase Structure and Timeline**  

| **Week** | **Modules** | **Key Topics** | **Deliverables** |  
|----------|-------------|----------------|------------------|  
| **Week 1** | 1.1, 1.2, 1.3 | - Database schema design<br>- Data types (e.g., `VARCHAR`, `DECIMAL`, `DATE`)<br>- Constraints (`PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`) | Create tables for `products`, `customers`, `orders`, and `payment_methods` |  
| **Week 2** | 1.4, 1.5, 1.6 | - Inserting sample data<br>- Core `SELECT` queries<br>- Filtering with `WHERE` and `BETWEEN` | Insert 100+ rows of sample data and write queries to retrieve product data |  
| **Week 3** | 1.7, 1.8 | - Aggregation (`SUM`, `AVG`, `COUNT`)<br>- `JOIN` operations (inner, left) | Calculate total revenue and join `products` with `orders` to retrieve order details |  
| **Week 4** | 1.9–1.10 (Intro) | - Subqueries<br>- Common Table Expressions (CTEs) | Write subqueries/CTEs to identify high-value customers |  

---

## **Tools and Technologies**  
- **Database**: SQLite (local DBMS, compatible with MySQL/PostgreSQL syntax).  
- **Utilities**: SQLite Browser, `sqlite3` CLI, or extensions like VS Code’s SQLite plugin.  
- **Sample Data**: Predefined datasets for products, customers, and orders (provided in project materials).  

---

## **Assessment and Deliverables**  
1. **Database Schema**: Submit DDL scripts for all tables with constraints.  
2. **Sample Data**: Provide SQL scripts to insert, update, and delete records.  
3. **Core Queries**: Submit queries to:  
   - Retrieve all products with prices and categories.  
   - Filter products by price range/category.  
   - Calculate total revenue and average order value.  
   - Join `products`, `orders`, and `customers` tables.  
4. **Checkpoint Review**: A peer or mentor review of your SQLite database and queries.  

---

## **Additional Resources**  
- **SQLite Documentation**: [https://www.sqlite.org/docs.html](https://www.sqlite.org/docs.html)  
- **SQLZoo Tutorials**: Interactive SQL practice for schema design and queries.  
- **Sample E-Commerce Datasets**: Use provided `.sql` files or generate synthetic data.  

---

## **Closing Note**  
Phase 1 builds the cornerstone of your e-commerce database. By mastering schema design, data manipulation, and basic querying, you’ll be equipped to tackle advanced SQL concepts in later phases. Stay curious, practice daily, and leverage the provided resources to reinforce your learning!  

---  
**Next Phase**: Phase 2 will explore advanced SQL techniques like window functions, transactions, and performance optimization.