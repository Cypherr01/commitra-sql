## What Is This?
Normalization is the process of organizing data in a database to minimize redundancy and improve data integrity. Think of it like a librarian organizing books on shelves - just as a librarian wants to avoid having multiple copies of the same book, a database designer wants to avoid having multiple copies of the same data.

## How It Works Internally
### Goal of Normalization
The goal of normalization is to reduce redundancy, prevent anomalies, and improve data integrity. This is achieved by dividing large tables into smaller ones, linked through relationships.

### Update Anomaly
An update anomaly occurs when changing one piece of data requires updating many rows. For example, if a customer's address is stored in multiple rows, updating the address would require updating all those rows.

### Insert Anomaly
An insert anomaly occurs when you cannot insert data without other unrelated data. For instance, if a table requires a customer's address to insert a new order, you cannot insert a new order without having a customer's address.

### Delete Anomaly
A delete anomaly occurs when deleting data accidentally removes other unrelated data. If a customer's address is deleted, all orders associated with that customer would also be deleted.

### Functional Dependency
A functional dependency is a relationship between two attributes where one attribute determines the value of the other. This is denoted as A → B, meaning A determines B.

### Partial Dependency
A partial dependency occurs when a non-key column depends on only part of a composite key. This can lead to data redundancy and inconsistencies.

### Transitive Dependency
A transitive dependency occurs when A → B → C, meaning A determines B, and B determines C. This can also lead to data redundancy and inconsistencies.

### Normal Forms
#### 1NF (First Normal Form)
A table is in 1NF if each cell contains a single value. This eliminates repeating groups and arrays.

#### 2NF (Second Normal Form)
A table is in 2NF if it is in 1NF and all non-key columns depend on the entire primary key.

#### 3NF (Third Normal Form)
A table is in 3NF if it is in 2NF and there are no transitive dependencies.

#### BCNF (Boyce-Codd Normal Form)
A table is in BCNF if it is in 3NF and there are no transitive dependencies, and a composite key depends on the entire primary key.

#### 4NF and 5NF
4NF and 5NF are higher levels of normalization that deal with multi-valued dependencies and join dependencies, respectively.

### Denormalization
Denormalization is the process of intentionally introducing redundancy into a database for performance reasons. This is often done in reporting tables, pre-aggregated summaries, and read-heavy workloads.

### LAYER 1: Minimum Viable Version
Normalization starts with identifying the minimum viable version of a table, which meets the basic requirements of data storage.

### LAYER 2: Why the Simple Version Breaks
The simple version breaks when data redundancy and inconsistencies arise due to poor design.

### LAYER 3: Production Version
The production version of a normalized table is designed to eliminate data redundancy and inconsistencies, ensuring data integrity.

### LAYER 4: Edge Cases
Two specific edge cases to consider are handling null values and dealing with composite keys.

CORE INSIGHT: Normalization is essential for maintaining data integrity and preventing anomalies in a database.

## Syntax and Structure
```sql
-- Create a table in 1NF
CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(50),
  address VARCHAR(100)
);

-- Create a table in 2NF
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  order_date DATE,
  FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Create a table in 3NF
CREATE TABLE order_items (
  order_id INT,
  product_id INT,
  quantity INT,
  PRIMARY KEY (order_id, product_id),
  FOREIGN KEY (order_id) REFERENCES orders(order_id)
);
```

## Practical Example
To demonstrate normalization, consider a simple e-commerce database with customers, orders, and products. The initial table design might look like this:
```sql
CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(50),
  address VARCHAR(100),
  order_id INT,
  order_date DATE,
  product_id INT,
  quantity INT
);
```
However, this design is not normalized, as it contains repeating groups and transitive dependencies. A normalized design would split this into separate tables for customers, orders, and order items.

## How This Connects to the Project
Before normalization, the e-commerce database design was incomplete and prone to data inconsistencies. After normalization, the design is more robust and efficient. The exact file and function name where this concept lives in the project is `database_design.sql`. A real company that uses this exact pattern is Amazon, which relies on a highly normalized database to manage its massive e-commerce platform.

## Common Mistakes Beginners Make
**Wrong idea:** Normalization is only for large databases.
**Correct idea:** Normalization is essential for any database, regardless of size.
**Most common mistake:** Failing to eliminate transitive dependencies.
**Looks right but is silently wrong:** Using a composite key without considering partial dependencies.
**Seems optional but critical at scale:** Denormalization for performance.
**Missed config or flag:** Forgetting to establish foreign key relationships.
**Interview question:** How would you design a normalized database for an e-commerce platform?

## Verification Task 1
Debug This: Your system shows inconsistent data for customer orders. You have a table with customer information, order dates, and product details. Diagnose and fix the issue.

## Solution 1
The issue is likely due to a lack of normalization. To fix this, split the table into separate tables for customers, orders, and order items, and establish foreign key relationships to ensure data consistency.

## Verification Task 2
Design Decision: You are building a database for a new e-commerce platform. Should you use a normalized or denormalized design? Defend your choice.

## Solution 2
I would choose a normalized design to ensure data integrity and prevent anomalies. While denormalization can improve performance, it can also lead to data inconsistencies and make maintenance more difficult.

## Verification Task 3
Code Review: The following code snippet is used to insert data into a customers table:
```sql
INSERT INTO customers (customer_id, name, address, order_id, order_date)
VALUES (1, 'John Doe', '123 Main St', 1, '2022-01-01');
```
Find and fix the bug.

## Solution 3
The bug is that the order_id and order_date columns are not necessary in the customers table. To fix this, remove these columns from the customers table and create a separate orders table with the relevant columns.

## What Comes Next
The next topic is Foreign Keys & Referential Integrity, which builds on the concept of normalization by establishing relationships between tables to maintain data consistency. This topic is a natural next step because it provides a mechanism to enforce the relationships established during normalization.

## Reference Summary
Normalization is the process of organizing data in a database to minimize redundancy and improve data integrity. It involves dividing large tables into smaller ones, linked through relationships, to eliminate data redundancy and inconsistencies. The goal of normalization is to reduce redundancy, prevent anomalies, and improve data integrity. A common mistake beginners make is failing to eliminate transitive dependencies. Normalization is essential for any database, regardless of size, and is used by companies like Amazon to manage their e-commerce platforms. By understanding normalization, developers can design more robust and efficient databases that maintain data integrity and prevent anomalies.