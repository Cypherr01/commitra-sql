## What Is This?
Common schema patterns refer to the standardized ways of organizing and structuring data in a database to support efficient data retrieval, storage, and manipulation. Imagine a library where books are organized by genre, author, and title, making it easier to find a specific book. Similarly, common schema patterns help in organizing data in a database, making it easier to manage and analyze.

## How It Works Internally
### LAYER 1: Minimum Viable Version
To start with, let's consider the basic elements that are added to every table in a database to track changes and ownership. This includes `created_at`, `updated_at`, `created_by`, and `updated_by` fields. 

### LAYER 2: Why the Simple Version Breaks
The simple version breaks when we need to automatically set the `created_at` field to the current timestamp and update the `updated_at` field whenever a record is modified. 

### LAYER 3: Production Version
In a production environment, we use triggers or application logic to auto-update the `updated_at` field. For MySQL, we can use `ON UPDATE CURRENT_TIMESTAMP` to achieve this. Additionally, we can add a `deleted_at` field to mark records as deleted without actually removing them. We also add a `deleted_by` field to track who deleted the record. 

### LAYER 4: Two Specific Edge Cases
One edge case is when we need to ensure that every query only returns records that are not deleted. We can achieve this by adding a `WHERE is_deleted = FALSE` clause to our queries or by using views to hide the complexity. Another edge case is when we need to optimize queries for active records. We can create a partial index on `is_deleted = FALSE` to improve query performance.

### CORE INSIGHT
The key takeaway here is that common schema patterns provide a standardized way of structuring data to support efficient data retrieval and manipulation. By following these patterns, we can ensure data consistency and scalability.

## Syntax and Structure
```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  created_by INT,
  updated_by INT,
  deleted_at TIMESTAMP NULL DEFAULT NULL,
  deleted_by INT NULL DEFAULT NULL,
  is_deleted BOOLEAN DEFAULT FALSE
);

CREATE INDEX idx_is_deleted ON users (is_deleted);
```

## Practical Example
Let's create a simple example to demonstrate how to use these fields. We'll create a table for orders and insert some data.
```sql
CREATE TABLE orders (
  id INT PRIMARY KEY,
  customer_id INT,
  order_date DATE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  created_by INT,
  updated_by INT,
  deleted_at TIMESTAMP NULL DEFAULT NULL,
  deleted_by INT NULL DEFAULT NULL,
  is_deleted BOOLEAN DEFAULT FALSE
);

INSERT INTO orders (customer_id, order_date, created_by) 
VALUES (1, '2022-01-01', 1);

UPDATE orders SET updated_by = 1 WHERE id = 1;

SELECT * FROM orders WHERE is_deleted = FALSE;
```

## How This Connects to the Project
Before applying common schema patterns, our e-commerce database design was incomplete and lacked standardized data structure. 
After applying these patterns, our database design is more efficient and scalable. 
The exact file and function name where this concept lives in the project is `database_schema.sql` and `create_tables()`. 
One real company that uses this exact pattern is Amazon, which relies heavily on efficient data retrieval and manipulation to support its massive e-commerce platform.

## Common Mistakes Beginners Make
**Most common mistake**: Forgetting to add the `WHERE is_deleted = FALSE` clause to queries, resulting in deleted records being returned.
**Looks right but is silently wrong**: Using `ON UPDATE CURRENT_TIMESTAMP` without specifying the field to update, leading to unexpected behavior.
**Seems optional but critical at scale**: Not creating partial indexes on `is_deleted = FALSE`, resulting in slow query performance.
**Missed config or flag**: Forgetting to set the `DEFAULT` value for `created_at` and `updated_at` fields.
**Interview question**: How would you optimize queries for active records in a database with millions of records?

## Verification Task 1
Debug the following issue: Your system is returning deleted records in queries. You have evidence that the `is_deleted` field is being set correctly. Diagnose and fix the issue.

## Solution 1
The issue is likely due to the missing `WHERE is_deleted = FALSE` clause in the queries. To fix this, add the clause to the queries to ensure only active records are returned.

## Verification Task 2
Design a database schema for a blog platform that uses common schema patterns. Should you use a separate table for comments or include them in the posts table? Defend your decision.

## Solution 2
I would use a separate table for comments. This is because comments are a separate entity from posts and have their own metadata, such as comment author and timestamp. Including comments in the posts table would lead to data redundancy and make it harder to manage comments.

## Verification Task 3
Review the following code snippet and identify the bug:
```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  created_by INT,
  updated_by INT
);

INSERT INTO users (name, created_by) VALUES ('John Doe', 1);
```
Find and fix the bug.

## Solution 3
The bug is that the `updated_by` field is not being set when inserting a new record. To fix this, we need to add the `updated_by` field to the `INSERT` statement:
```sql
INSERT INTO users (name, created_by, updated_by) VALUES ('John Doe', 1, 1);
```

## What Comes Next
The next topic is "How Indexes Work — Deep Dive". This topic follows logically from common schema patterns because understanding how to optimize queries for active records using indexes is crucial for maintaining database performance. The concept of partial indexes on `is_deleted = FALSE` will be revisited in this topic to demonstrate how indexes can be used to improve query performance.

## Reference Summary
Common schema patterns provide a standardized way of structuring data to support efficient data retrieval and manipulation. By adding fields such as `created_at`, `updated_at`, `created_by`, and `updated_by` to every table, we can track changes and ownership. Using triggers or application logic to auto-update the `updated_at` field and adding a `deleted_at` field to mark records as deleted without removing them are also important aspects of common schema patterns. The most common mistake beginners make is forgetting to add the `WHERE is_deleted = FALSE` clause to queries. By applying common schema patterns, we can ensure data consistency and scalability, which is critical for supporting efficient reporting and analysis in e-commerce database design. This concept enables the use of indexes to optimize queries for active records, which will be discussed in the next topic.