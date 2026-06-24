## What Is This?
An index is a data structure that improves the speed of data retrieval by providing a quick way to locate specific data. Think of an index like a phonebook: when you want to find a specific person's phone number, you can look up their name in the phonebook and quickly find their number, rather than having to search through the entire list of numbers. This matters to you because a well-designed index can greatly improve the performance of your database queries.

## How It Works Internally
### Index — Separate Data Structure
An index is a separate data structure that is created alongside a table to speed up lookups. It contains a copy of the selected columns from the table, along with a pointer to the location of the corresponding rows in the table.

### Create Index
To create an index, you can use the `CREATE INDEX` statement. For example, to create an index on a column called `name` in a table called `customers`, you would use the following statement:
```text
# Create an index on the name column in the customers table
CREATE INDEX idx_name ON customers (name)
```
This creates a standard index on the `name` column, which can be used to speed up queries that filter on this column.

### Create Unique Index
A unique index is an index that enforces uniqueness on the columns it indexes. This means that no two rows in the table can have the same values in the indexed columns. To create a unique index, you can use the `CREATE UNIQUE INDEX` statement:
```text
# Create a unique index on the email column in the customers table
CREATE UNIQUE INDEX idx_email ON customers (email)
```
This creates a unique index on the `email` column, which ensures that no two customers can have the same email address.

### Composite Index
A composite index is an index that is created on multiple columns. This can be useful when you frequently query on multiple columns together. To create a composite index, you can use the following statement:
```text
# Create a composite index on the name and email columns in the customers table
CREATE INDEX idx_name_email ON customers (name, email)
```
This creates a composite index on the `name` and `email` columns, which can be used to speed up queries that filter on both of these columns.

### Drop Index
To drop an index, you can use the `DROP INDEX` statement. For example:
```text
# Drop the idx_name index
DROP INDEX idx_name
```
This drops the `idx_name` index, which can be useful if you no longer need the index or if you want to recreate it with different settings.

### Automatic Index Creation
Indexes are automatically created on columns that have a `PRIMARY KEY` or `UNIQUE` constraint. This is because these constraints require that the values in the column be unique, and an index is the most efficient way to enforce this constraint.

### B-Tree Index
The default type of index in most databases is a B-tree index. This type of index is great for equality, range, and prefix matching queries, and is the most common type of index used in databases.

### When Indexes Help
Indexes can help speed up queries that filter on specific columns, such as `WHERE` clauses. They can also help speed up queries that join tables on specific columns, such as `JOIN` clauses. Additionally, indexes can help speed up queries that sort or group data, such as `ORDER BY` and `GROUP BY` clauses.

### When Indexes Hurt
Indexes can hurt performance if they are created on columns that are frequently updated, as this can cause the index to become outdated and require frequent rebuilding. Indexes can also hurt performance if they are created on columns with low cardinality, such as boolean columns, as this can cause the index to become very large and slow to query.

### Explain
To verify that an index is being used, you can use the `EXPLAIN` statement. For example:
```text
# Explain the query plan for a query that filters on the name column
EXPLAIN SELECT * FROM customers WHERE name = 'John Doe'
```
This shows the query plan for the query, including which indexes are being used.

### CORE INSIGHT
The core insight to remember is that indexes are a powerful tool for improving query performance, but they require careful consideration of the trade-offs between query speed and update performance.

## Syntax and Structure
```sql
-- Create an index on the name column in the customers table
CREATE INDEX idx_name ON customers (name);

-- Create a unique index on the email column in the customers table
CREATE UNIQUE INDEX idx_email ON customers (email);

-- Create a composite index on the name and email columns in the customers table
CREATE INDEX idx_name_email ON customers (name, email);

-- Drop the idx_name index
DROP INDEX idx_name;
```

## Practical Example
```sql
-- Create a table called customers with columns for name and email
CREATE TABLE customers (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255)
);

-- Insert some data into the customers table
INSERT INTO customers (id, name, email) VALUES
  (1, 'John Doe', 'john.doe@example.com'),
  (2, 'Jane Doe', 'jane.doe@example.com'),
  (3, 'Bob Smith', 'bob.smith@example.com');

-- Create an index on the name column in the customers table
CREATE INDEX idx_name ON customers (name);

-- Query the customers table to find all customers with the name 'John Doe'
SELECT * FROM customers WHERE name = 'John Doe';
```

## How This Connects to the Project
Before learning about indexes, our project's database queries were slow and inefficient. After learning about indexes, we can create indexes on the columns that are frequently queried, which will greatly improve the performance of our database queries. The exact file and function name where this concept lives in the project is `database.py` and `create_indexes()`. One real company that uses this exact pattern is Amazon, which uses indexes to improve the performance of its database queries.

## Common Mistakes Beginners Make
**Most common mistake**: Creating an index on a column that is frequently updated, which can cause the index to become outdated and require frequent rebuilding.
Wrong idea: Creating an index on every column in the table.
Correct idea: Creating an index only on the columns that are frequently queried.
**Looks right but is silently wrong**: Creating a composite index on multiple columns, but not including all of the columns in the query.
**Seems optional but critical at scale**: Not creating an index on a column that is used in a `WHERE` clause, which can cause the query to become very slow.
**Missed config or flag**: Not setting the `INDEX` flag when creating a table, which can cause the index to not be created.
**Interview question**: How would you optimize a slow database query by using indexes?

## Verification Task 1
Your system shows slow query performance. You have a query that filters on a specific column. Diagnose and fix.
## Solution 1
Create an index on the column that is being filtered on.

## Verification Task 2
Building a database schema for an e-commerce application. Use a B-tree index or a hash index on the `product_id` column? Defend using this topic.
## Solution 2
Use a B-tree index on the `product_id` column, as it is the most common type of index used in databases and is well-suited for equality and range queries.

## Verification Task 3
Find and fix the bug in the following code snippet:
```sql
CREATE TABLE customers (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255)
);

CREATE INDEX idx_name ON customers (name);

INSERT INTO customers (id, name, email) VALUES
  (1, 'John Doe', 'john.doe@example.com'),
  (2, 'Jane Doe', 'jane.doe@example.com'),
  (3, 'Bob Smith', 'bob.smith@example.com');

SELECT * FROM customers WHERE name = 'John Doe';
```
## Solution 3
The bug is that the `idx_name` index is not being used in the query. To fix this, we need to add the `INDEX` flag to the `CREATE TABLE` statement:
```sql
CREATE TABLE customers (
  id INT PRIMARY KEY,
  name VARCHAR(255) INDEX,
  email VARCHAR(255)
);
```

## What Comes Next
The next topic is MySQL Architecture. This topic follows logically from this one because understanding how indexes work is crucial to understanding how MySQL architecture works. In particular, the concept of indexes will be used to explain how MySQL stores and retrieves data.

## Reference Summary
An index is a data structure that improves the speed of data retrieval by providing a quick way to locate specific data. Indexes can be created on one or more columns of a table, and can be used to speed up queries that filter on those columns. There are different types of indexes, including B-tree indexes and hash indexes, each with its own strengths and weaknesses. Creating an index can improve query performance, but can also slow down update performance. The `EXPLAIN` statement can be used to verify that an index is being used. This concept is critical to understanding how to optimize database queries and improve the performance of a database.