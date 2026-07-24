## What Is This?
An index is a separate data structure that stores key-value pairs, allowing for faster data retrieval. Think of an index like a phonebook, where you can quickly find a person's phone number by looking up their name, rather than searching through the entire list of numbers. This matters to you because a well-designed index can significantly improve the performance of your database queries.

## How It Works Internally
### Index — Separate Data Structure
An index is a data structure that stores key-value pairs, where the key is a column or set of columns in a table, and the value is a pointer to the location of the corresponding data in the table. This allows for fast lookup, insertion, and deletion of data.

### B-Tree Index (Default)
A B-Tree index is a type of index that uses a balanced tree data structure to store key-value pairs. This allows for efficient lookup, insertion, and deletion of data, with an average time complexity of O(log n). B-Tree indexes are great for queries that use equality, range, and prefix matching conditions, such as `=`, `<`, `>`, `BETWEEN`, `LIKE 'prefix%'`, and `IN`.

### B+ Tree
A B+ Tree is a variant of the B-Tree index, where all data is stored in the leaf nodes, and the leaf nodes are linked together. This allows for efficient range scans and retrieval of data.

### Index Leaf Pages
Index leaf pages point to the location of the corresponding data in the table, which can be either a heap tuple (in PostgreSQL) or a clustered index key (in InnoDB).

### Index Height
The index height refers to the number of levels in the index tree. Typically, the index height is 2-4 levels, which allows for fast lookup and retrieval of data, even for large tables with millions of rows.

### Composite Index
A composite index is an index that is created on multiple columns. The order of the columns in the index matters, as the index is used to speed up queries that filter on the leftmost columns first. This is known as the leftmost prefix rule.

### Index Selectivity
Index selectivity refers to the fraction of distinct values in the indexed column. A higher selectivity means that the index is more effective at narrowing down the search space, resulting in faster query performance.

### Covering Index
A covering index is an index that contains all the columns needed to answer a query. This allows the database to retrieve all the required data from the index, without having to access the underlying table.

## Syntax and Structure
```sql
-- Create a B-Tree index on a single column
CREATE INDEX idx_name ON table_name (column_name);

-- Create a composite index on multiple columns
CREATE INDEX idx_name ON table_name (column1, column2);

-- Create a covering index
CREATE INDEX idx_name ON table_name (column1, column2, column3);
```

## Practical Example
```sql
-- Create a sample table
CREATE TABLE products (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  price DECIMAL(10, 2)
);

-- Create a B-Tree index on the name column
CREATE INDEX idx_name ON products (name);

-- Query the table using the indexed column
SELECT * FROM products WHERE name = 'Product A';
```

## How This Connects to the Project
Before applying indexes, our e-commerce database query performance was slow due to the large amount of data. After creating indexes on the products table, query performance improved significantly. The exact file and function name where this concept lives in the project is `database/indexing.py`. A real company that uses this exact pattern is Amazon, which uses indexes to improve the performance of its product search queries.

## Common Mistakes Beginners Make
**Wrong idea: Indexing every column will always improve performance.**
Correct idea: Indexing only the columns used in queries can improve performance, while indexing every column can lead to slower write performance.
**Looks right but is silently wrong: Creating an index on a column with low selectivity.**
For example, creating an index on a column that contains only two unique values will not improve query performance.
**Seems optional but critical at scale: Not maintaining index statistics.**
Failing to update index statistics can lead to poor query performance and incorrect query plans.
**Missed config or flag: Not using the correct index type for the query.**
Using a B-Tree index for a query that requires a full-text search can lead to poor performance.
**Interview question: How would you optimize the performance of a slow query?**
Surface answer: Use indexes to speed up the query. Production answer: Analyze the query plan, identify the bottlenecks, and apply indexing, partitioning, and other optimization techniques as needed.

## Verification Task 1
Debug the following symptom: "Query performance is slow due to a missing index."
You have the following evidence: A query plan that shows a full table scan.
Diagnose and fix the issue.

## Solution 1
Create an index on the column used in the query filter condition.

## Verification Task 2
Design a decision: Building a database for an e-commerce application. Use a B-Tree index or a hash index for the product name column?
Defend your choice using the concepts learned in this topic.

## Solution 2
Use a B-Tree index for the product name column, as it allows for efficient range scans and retrieval of data, and is suitable for queries that use equality and prefix matching conditions.

## Verification Task 3
Code review: Find and fix the bug in the following code snippet:
```sql
CREATE INDEX idx_name ON products (name);
SELECT * FROM products WHERE name = 'Product A' OR price > 10;
```
The bug is that the index is not being used for the query.

## Solution 3
Create a composite index on the name and price columns:
```sql
CREATE INDEX idx_name_price ON products (name, price);
SELECT * FROM products WHERE name = 'Product A' OR price > 10;
```

## What Comes Next
The next topic is "EXPLAIN — Reading Execution Plans", which logically follows from this topic because understanding how indexes work is crucial to interpreting and optimizing query plans. The concept of index selectivity will reappear in this topic, as it is essential to understanding how the database chooses the most efficient query plan.

## Reference Summary
An index is a data structure that stores key-value pairs, allowing for faster data retrieval. A B-Tree index is a type of index that uses a balanced tree data structure to store key-value pairs, and is suitable for queries that use equality, range, and prefix matching conditions. A composite index is an index that is created on multiple columns, and the order of the columns matters. Index selectivity refers to the fraction of distinct values in the indexed column, and a higher selectivity means that the index is more effective at narrowing down the search space. A covering index is an index that contains all the columns needed to answer a query, allowing the database to retrieve all the required data from the index without having to access the underlying table. The most common production mistake is creating an index on a column with low selectivity, which can lead to slower write performance. This concept is essential to database optimization and is used in real-world applications, such as e-commerce databases.