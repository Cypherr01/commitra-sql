## What Is This?
Filtering in SQL is the process of selecting a subset of data from a larger dataset based on specific conditions. Think of it like searching for a specific book in a library - you want to find all the books that match certain criteria, such as author, title, or genre. In SQL, this is achieved using the `WHERE` clause, which allows you to specify conditions that the data must meet in order to be included in the results.

## How It Works Internally
### Introduction to Filtering
Filtering is a fundamental concept in SQL that enables you to narrow down your search results to only the data that is relevant to your query. This is done by adding a `WHERE` clause to your `SELECT` statement, which specifies the conditions that the data must meet.

### Comparison Operators
The most basic way to filter data is by using comparison operators, such as `=`, `!=` / `<>`, `>`, `<`, `>=`, and `<=`. These operators allow you to compare values in your dataset and select only the rows that meet the specified condition.
```text
# Example of using comparison operators
# SELECT * FROM table WHERE column = 'value'
# SELECT * FROM table WHERE column != 'value'
# SELECT * FROM table WHERE column > 'value'
```
### BETWEEN Operator
The `BETWEEN` operator is used to select values within a specific range. It is inclusive, meaning that it includes the values at the start and end of the range.
```text
# Example of using BETWEEN operator
# SELECT * FROM table WHERE column BETWEEN 'val1' AND 'val2'
```
### IN Operator
The `IN` operator is used to select values that match any value in a list. It is often used in conjunction with a subquery to select values that meet certain conditions.
```text
# Example of using IN operator
# SELECT * FROM table WHERE column IN ('val1', 'val2', 'val3')
```
### NOT IN Operator
The `NOT IN` operator is used to select values that do not match any value in a list. However, be careful when using this operator, as it can return no rows if the list contains a `NULL` value.
```text
# Example of using NOT IN operator
# SELECT * FROM table WHERE column NOT IN ('val1', 'val2', 'val3')
```
### LIKE Operator
The `LIKE` operator is used to select values that match a specific pattern. It uses two special characters: `%` (zero or more characters) and `_` (exactly one character).
```text
# Example of using LIKE operator
# SELECT * FROM table WHERE column LIKE '%pattern%'
```
### ILIKE Operator
The `ILIKE` operator is similar to the `LIKE` operator, but it is case-insensitive.
```text
# Example of using ILIKE operator
# SELECT * FROM table WHERE column ILIKE '%pattern%'
```
### REGEXP Operator
The `REGEXP` operator is used to select values that match a regular expression pattern.
```text
# Example of using REGEXP operator
# SELECT * FROM table WHERE column REGEXP 'pattern'
```
### IS NULL and IS NOT NULL Operators
The `IS NULL` and `IS NOT NULL` operators are used to select values that are either `NULL` or not `NULL`.
```text
# Example of using IS NULL and IS NOT NULL operators
# SELECT * FROM table WHERE column IS NULL
# SELECT * FROM table WHERE column IS NOT NULL
```
### EXISTS and NOT EXISTS Operators
The `EXISTS` and `NOT EXISTS` operators are used to select values that exist or do not exist in a subquery.
```text
# Example of using EXISTS and NOT EXISTS operators
# SELECT * FROM table WHERE EXISTS (subquery)
# SELECT * FROM table WHERE NOT EXISTS (subquery)
```
### Logical Operators
The `AND`, `OR`, and `NOT` operators are used to combine conditions in a `WHERE` clause.
```text
# Example of using logical operators
# SELECT * FROM table WHERE condition1 AND condition2
# SELECT * FROM table WHERE condition1 OR condition2
# SELECT * FROM table WHERE NOT condition
```
### Operator Precedence
The operator precedence in SQL is as follows: `NOT` > `AND` > `OR`. It is a good practice to use parentheses to clarify the order of operations.
```text
# Example of using operator precedence
# SELECT * FROM table WHERE NOT (condition1 AND condition2)
```
### Short-Circuit Evaluation
SQL uses short-circuit evaluation, which means that the `AND` operator stops evaluating conditions as soon as it encounters a `FALSE` condition, and the `OR` operator stops evaluating conditions as soon as it encounters a `TRUE` condition.
```text
# Example of using short-circuit evaluation
# SELECT * FROM table WHERE condition1 AND condition2
```
### NULL Logic
In SQL, `NULL` values can be tricky to work with. The `AND` operator will return `NULL` if one of the conditions is `NULL`, and the `OR` operator will return `TRUE` if one of the conditions is `TRUE`.
```text
# Example of using NULL logic
# SELECT * FROM table WHERE condition1 AND NULL
# SELECT * FROM table WHERE condition1 OR TRUE
```
CORE INSIGHT: The key to mastering filtering in SQL is to understand the different operators and how they interact with each other. This matters to you because if you don't use the correct operators, you may end up with incorrect or incomplete results, which can have serious consequences in a real-world application.

## Syntax and Structure
```sql
-- Example of using WHERE clause with comparison operators
SELECT * FROM products
WHERE price > 10 AND category = 'electronics';

-- Example of using BETWEEN operator
SELECT * FROM products
WHERE price BETWEEN 10 AND 20;

-- Example of using IN operator
SELECT * FROM products
WHERE category IN ('electronics', 'clothing', 'home goods');

-- Example of using NOT IN operator
SELECT * FROM products
WHERE category NOT IN ('electronics', 'clothing', 'home goods');

-- Example of using LIKE operator
SELECT * FROM products
WHERE name LIKE '%apple%';

-- Example of using ILIKE operator
SELECT * FROM products
WHERE name ILIKE '%apple%';

-- Example of using REGEXP operator
SELECT * FROM products
WHERE name REGEXP 'apple';

-- Example of using IS NULL and IS NOT NULL operators
SELECT * FROM products
WHERE description IS NULL;

SELECT * FROM products
WHERE description IS NOT NULL;

-- Example of using EXISTS and NOT EXISTS operators
SELECT * FROM products
WHERE EXISTS (SELECT * FROM orders WHERE orders.product_id = products.id);

SELECT * FROM products
WHERE NOT EXISTS (SELECT * FROM orders WHERE orders.product_id = products.id);

-- Example of using logical operators
SELECT * FROM products
WHERE price > 10 AND category = 'electronics';

SELECT * FROM products
WHERE price > 10 OR category = 'electronics';

SELECT * FROM products
WHERE NOT price > 10;
```
This matters to you because understanding the syntax and structure of SQL queries is essential for writing effective and efficient queries.

## Practical Example
Let's say we have a table called `products` with columns `id`, `name`, `price`, and `category`. We want to find all the products that are in the `electronics` category and have a price greater than $10.
```sql
SELECT * FROM products
WHERE category = 'electronics' AND price > 10;
```
This will return all the rows in the `products` table that match the specified conditions.

## How This Connects to the Project
BEFORE: Our e-commerce database has a `products` table with columns `id`, `name`, `price`, and `category`, but we don't have a way to filter products by category and price.
AFTER: We can now use the `WHERE` clause to filter products by category and price, making it easier to find specific products.
Exact file and function name: `database.sql`, `get_products_by_category_and_price` function.
One real company that uses this exact pattern: Amazon, which uses SQL to filter products by category, price, and other criteria.

## Common Mistakes Beginners Make
**Wrong idea:** Using the `=` operator to compare values with `NULL`.
**Correct idea:** Using the `IS NULL` operator to compare values with `NULL`.
Wrong idea: Not using parentheses to clarify the order of operations in a `WHERE` clause.
Correct idea: Using parentheses to ensure that the conditions are evaluated in the correct order.
Looks right but is silently wrong: Using the `NOT IN` operator with a list that contains `NULL` values.
Seems optional but critical at scale: Not indexing columns used in `WHERE` clauses, which can lead to slow query performance.
Missed config or flag: Not setting the correct database connection parameters, which can lead to errors when running queries.
Interview question: How would you optimize a slow-running query that uses a `WHERE` clause with multiple conditions?

## Verification Task 1
Your system shows an error message when trying to filter products by category and price. You have a `products` table with columns `id`, `name`, `price`, and `category`. Diagnose and fix the issue.
## Solution 1
The issue is likely due to a syntax error in the `WHERE` clause. Check the query and make sure that the conditions are correctly formatted and that the column names are spelled correctly.

## Verification Task 2
You are building a new feature that allows users to filter products by category and price. You have two options: use a single `WHERE` clause with multiple conditions or use separate `WHERE` clauses for each condition. Defend your choice.
## Solution 2
I would choose to use a single `WHERE` clause with multiple conditions. This approach is more efficient and easier to maintain than using separate `WHERE` clauses for each condition.

## Verification Task 3
You are reviewing a code snippet that filters products by category and price. The snippet uses a `WHERE` clause with multiple conditions, but it does not use parentheses to clarify the order of operations. Find and fix the bug.
## Solution 3
The bug is that the conditions in the `WHERE` clause are not properly ordered. To fix this, add parentheses to clarify the order of operations. For example:
```sql
SELECT * FROM products
WHERE (category = 'electronics' AND price > 10) OR (category = 'clothing' AND price < 20);
```
This ensures that the conditions are evaluated in the correct order.

## What Comes Next
The next topic is **JOINs — Complete**, which builds on the concepts learned in this topic. In **JOINs — Complete**, we will learn how to combine data from multiple tables using various types of joins. This topic is a natural next step because it requires a solid understanding of filtering and querying data, which is the focus of this topic.

## Reference Summary
Filtering in SQL is the process of selecting a subset of data from a larger dataset based on specific conditions. The `WHERE` clause is used to specify these conditions, which can include comparison operators, logical operators, and other functions. Understanding the syntax and structure of SQL queries is essential for writing effective and efficient queries. Common mistakes beginners make include using the `=` operator to compare values with `NULL` and not using parentheses to clarify the order of operations. This topic connects to the project by providing a way to filter products by category and price, and it is used by companies like Amazon to filter products by various criteria. The key takeaways from this topic are the importance of using the correct operators and understanding the order of operations in a `WHERE` clause.