## What Is This?
Schema anti-patterns refer to common mistakes or inefficient designs in database schemas that can lead to performance issues, data inconsistencies, and scalability problems. Think of it like building a house with a flawed foundation - it may look fine at first, but as time passes, the weaknesses will become apparent, and repairs will be costly. A simple analogy is a filing system where instead of having separate folders for different types of documents, everything is thrown into a single drawer, making it hard to find what you need when you need it.

## How It Works Internally
### Entity-Attribute-Value (EAV)
The Entity-Attribute-Value (EAV) model is a design pattern that allows for flexible and dynamic attribute management. However, it can lead to unindexable data and lacks type safety, making it difficult to maintain and query. 
```text
# Define an entity
# Assign attributes to the entity
# Values are stored separately, linked to the entity and attribute
```
A better approach is to use JSONB data types, which offer more flexibility and query efficiency.

### Comma-separated values in column
Storing comma-separated values in a single column violates the first normal form (1NF) of database design, leading to difficulties in querying and maintaining data integrity. 
```text
# Incorrect way: storing multiple values in one column
# Correct way: use an array type or a junction table
```
Using array types or junction tables can normalize the data and improve query performance.

### Storing derived data
Storing derived data, such as calculated totals, can lead to data inconsistencies if the base data changes. 
```text
# Calculate total on the fly instead of storing it
# Use triggers or views to maintain data consistency
```
Unless performance requirements dictate otherwise, it's generally better to compute derived data at query time.

### Using strings for IDs
Using strings as IDs can lead to join performance issues, charset problems, and difficulties in maintaining referential integrity. 
```text
# Prefer integer or UUID IDs for better performance and simplicity
```
Integer or UUID IDs are more efficient and less prone to errors.

### SELECT * in views and queries
Using `SELECT *` in views and queries can make them fragile and prone to breaking when the schema changes. 
```text
# Specify column names explicitly for better maintainability
```
Explicitly naming columns improves query readability and reduces the risk of errors.

### Magic numbers
Using magic numbers, or undefined constants, can make code difficult to understand and maintain. 
```text
# Define constants or use ENUMs for better readability
```
Defining constants or using ENUMs can improve code clarity and reduce errors.

### Implicit column ordering dependence
Depending on implicit column ordering can lead to unexpected behavior when the schema changes. 
```text
# Always specify column names explicitly to avoid dependencies
```
Explicitly naming columns ensures that queries work as intended, even if the schema changes.

### No NOT NULL constraints
Failing to use NOT NULL constraints can lead to null values in columns that should always have a value. 
```text
# Use NOT NULL constraints to ensure data integrity
```
NOT NULL constraints help maintain data consistency and prevent errors.

### Inconsistent naming
Using inconsistent naming conventions can make the schema difficult to understand and maintain. 
```text
# Choose a naming convention and stick to it for better readability
```
Consistent naming conventions improve schema readability and reduce errors.

### Timestamp without timezone
Using timestamps without timezones can lead to confusion and errors when working with date and time data. 
```text
# Use timestamps with timezones for better accuracy and consistency
```
Timestamps with timezones ensure that date and time data is handled correctly.

## Syntax and Structure
```sql
-- Create a table with a JSONB column
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    attributes JSONB NOT NULL
);

-- Insert data into the table
INSERT INTO products (attributes)
VALUES ('{"color": "red", "size": "large"}');

-- Query the data using JSONB functions
SELECT * FROM products
WHERE attributes @> '{"color": "red"}';
```
This example demonstrates how to create a table with a JSONB column, insert data, and query it using JSONB functions.

## Practical Example
```sql
-- Create a table with an array column
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    items TEXT[]
);

-- Insert data into the table
INSERT INTO orders (items)
VALUES ('{"item1", "item2", "item3"}');

-- Query the data using array functions
SELECT * FROM orders
WHERE items @> '{"item1"}';
```
This example shows how to create a table with an array column, insert data, and query it using array functions.

## How This Connects to the Project
ELEMENT 1: Before applying schema anti-patterns knowledge, our e-commerce database design project may have performance issues, data inconsistencies, and scalability problems.
ELEMENT 2: After refactoring the schema to avoid anti-patterns, the database will be more efficient, scalable, and easier to maintain.
ELEMENT 3: The `products` table in our project will use a JSONB column to store dynamic attributes, and the `orders` table will use an array column to store items.
ELEMENT 4: Companies like Amazon and eBay use well-designed database schemas to handle large amounts of data and traffic, and our project will follow similar principles to ensure scalability and performance.

## Common Mistakes Beginners Make
**Most common mistake**: Not using NOT NULL constraints, leading to null values in columns that should always have a value.
Wrong idea: Using `SELECT *` in views and queries is harmless.
Correct idea: Explicitly naming columns improves query readability and reduces the risk of errors.
**Looks right but is silently wrong**: Using magic numbers or undefined constants, making code difficult to understand and maintain.
**Seems optional but critical at scale**: Not using timestamps with timezones, leading to confusion and errors when working with date and time data.
**Missed config or flag**: Failing to use consistent naming conventions, making the schema difficult to understand and maintain.
**Interview question**: How would you refactor a database schema to avoid common anti-patterns and improve performance?

## Verification Task 1
Debug This: "Your database query is slow and returns incorrect results. You have a table with a comma-separated column. Diagnose and fix."
## Solution 1
To fix this issue, we need to refactor the table to use a separate table for the comma-separated values or use an array column. We also need to update the query to use the new table structure or array functions.

## Verification Task 2
Design Decision: "You are building an e-commerce database and need to store product attributes. Should you use an Entity-Attribute-Value (EAV) model or a JSONB column? Defend your choice."
## Solution 2
We should use a JSONB column to store product attributes. This approach offers more flexibility and query efficiency compared to the EAV model. We can use JSONB functions to query and manipulate the data, making it easier to maintain and scale.

## Verification Task 3
Code Review: 
```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    items TEXT[]
);

INSERT INTO orders (items)
VALUES ('{"item1", "item2", "item3"}');
```
Find and fix the bug: The code is trying to insert an array of items into the `items` column, but the syntax is incorrect.
## Solution 3
The correct syntax for inserting an array of items into the `items` column is:
```sql
INSERT INTO orders (items)
VALUES (ARRAY['item1', 'item2', 'item3']);
```
We need to use the `ARRAY` function to create an array from the list of items.

## What Comes Next
The next topic is "Index Types — Complete", which builds upon the knowledge of schema design and anti-patterns. Understanding schema anti-patterns is crucial for designing efficient indexes, as a well-designed schema is essential for creating effective indexes. The concept of using JSONB columns, which we discussed in this topic, will be directly used in "Index Types — Complete" to create efficient indexes for JSONB data.

## Reference Summary
Schema anti-patterns refer to common mistakes or inefficient designs in database schemas that can lead to performance issues, data inconsistencies, and scalability problems. The Entity-Attribute-Value (EAV) model, comma-separated values in columns, and storing derived data are examples of schema anti-patterns. Using strings for IDs, `SELECT *` in views and queries, magic numbers, implicit column ordering dependence, and inconsistent naming are also common mistakes. NOT NULL constraints, timestamps with timezones, and consistent naming conventions are essential for maintaining data integrity and scalability. By understanding and avoiding these anti-patterns, developers can design more efficient, scalable, and maintainable database schemas. This knowledge is crucial for building large-scale applications, such as e-commerce databases, and will be used in the next topic, "Index Types — Complete", to create efficient indexes for JSONB data.