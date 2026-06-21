## What Is This?
NULL Functions & Conditional Logic is a fundamental concept in SQL that allows you to handle missing or unknown data, and make decisions based on conditions in your queries. Imagine you're a librarian, and you need to catalog books with missing information, such as unknown authors or publication dates. You would use special markers to indicate the missing data, and then use rules to decide how to handle those markers when searching or sorting the books.

## How It Works Internally
### LAYER 1: Minimum Viable Version
The minimum viable version of NULL Functions & Conditional Logic involves using the `COALESCE` function to replace missing values with a default value. For example, if you have a table with a column for the customer's name, and some rows have a missing name, you can use `COALESCE` to replace the missing name with a default value, such as 'Unknown'.

### LAYER 2: Why the Simple Version Breaks
The simple version breaks when you need to handle more complex conditions, such as checking if a value is NULL before performing an operation. In this case, you would use the `NULLIF` function to return NULL if a condition is met, or the `IFNULL` function to return a default value if a column is NULL.

### LAYER 3: Production Version
The production version of NULL Functions & Conditional Logic involves using a combination of functions, such as `COALESCE`, `NULLIF`, and `IFNULL`, to handle complex conditions and missing data. You can also use the `IF` function to make decisions based on conditions, and the `CASE WHEN` statement to perform more complex conditional logic.

### LAYER 4: Edge Cases
One edge case to consider is when using arithmetic operations with NULL values, which can result in NULL. For example, if you have a column with a NULL value, and you try to add a number to it, the result will be NULL. Another edge case is when using comparisons with NULL values, which can result in NULL. For example, if you compare a column with a NULL value to another column, the result will be NULL.

### NULL Functions
The following NULL functions are available in SQL:
* `COALESCE(a, b, c, ...)`: returns the first non-NULL value
* `NULLIF(a, b)`: returns NULL if a = b
* `IFNULL(a, b)`: returns b if a is NULL
* `NVL(a, b)`: equivalent to `IFNULL(a, b)`

### Conditional Logic
The following conditional logic functions are available in SQL:
* `IF(condition, true_val, false_val)`: returns true_val if condition is true, otherwise returns false_val
* `IIF(condition, true_val, false_val)`: equivalent to `IF(condition, true_val, false_val)`
* `CASE WHEN ... THEN ... ELSE ... END`: performs complex conditional logic

### NULL Arithmetic and Comparisons
Any arithmetic operation with NULL returns NULL. For example, `NULL + 1` returns NULL. Similarly, any comparison with NULL returns NULL. For example, `NULL = 1` returns NULL.

### Three-Valued Logic
SQL uses three-valued logic, which means that a condition can be TRUE, FALSE, or NULL. This is different from two-valued logic, which only allows TRUE or FALSE.

### CASE with NULLs
When using the `CASE WHEN` statement, you can check for NULL values using the `IS NULL` clause. For example, `CASE WHEN col IS NULL THEN ...`.

CORE INSIGHT: NULL Functions & Conditional Logic are essential for handling missing or unknown data in SQL, and can be used to perform complex conditional logic and make decisions based on conditions.

## Syntax and Structure
```sql
-- COALESCE example
SELECT COALESCE(name, 'Unknown') AS name
FROM customers;

-- NULLIF example
SELECT NULLIF(a, b) AS result
FROM table;

-- IFNULL example
SELECT IFNULL(name, 'Unknown') AS name
FROM customers;

-- IF example
SELECT IF(condition, true_val, false_val) AS result
FROM table;

-- CASE WHEN example
SELECT CASE
    WHEN condition THEN true_val
    ELSE false_val
END AS result
FROM table;
```

## Practical Example
```sql
-- Create a table with missing data
CREATE TABLE customers (
    id INT,
    name VARCHAR(255),
    email VARCHAR(255)
);

-- Insert data with missing values
INSERT INTO customers (id, name, email)
VALUES (1, 'John Doe', 'john@example.com'),
       (2, NULL, 'jane@example.com'),
       (3, 'Bob Smith', NULL);

-- Use COALESCE to replace missing values
SELECT COALESCE(name, 'Unknown') AS name,
       COALESCE(email, 'Unknown') AS email
FROM customers;
```

## How This Connects to the Project
ELEMENT 1: Before using NULL Functions & Conditional Logic, our project's customer database would have missing or unknown data, which would cause errors or incorrect results when querying the data.
ELEMENT 2: After using NULL Functions & Conditional Logic, our project's customer database would have complete and accurate data, which would allow us to perform complex queries and make decisions based on conditions.
ELEMENT 3: The exact file and function name where this concept lives in the project is `customer_database.sql` and `get_customer_data()`.
ELEMENT 4: A real company that uses this exact pattern is Amazon, which uses NULL Functions & Conditional Logic to handle missing or unknown data in their customer database and perform complex queries to personalize customer recommendations.

## Common Mistakes Beginners Make
**Most common mistake**: Not checking for NULL values before performing operations, which can result in NULL or incorrect results.
Wrong idea: Using `= NULL` to check for NULL values.
Correct idea: Using `IS NULL` to check for NULL values.
**Looks right but is silently wrong**: Using `COALESCE` with only one argument, which can cause the function to always return the first argument.
**Seems optional but critical at scale**: Not using `NULLIF` to prevent division by zero, which can cause errors or incorrect results.
**Missed config or flag**: Not setting the `NULL` value for a column, which can cause errors or incorrect results.
**Interview question**: How would you handle missing or unknown data in a SQL database?

## Verification Task 1
Debug This: Your system shows an error message when trying to query the customer database. You have a table with missing values, and you are using `COALESCE` to replace the missing values. However, the error message indicates that there is a NULL value in one of the columns. Diagnose and fix the issue.

## Solution 1
To fix the issue, you need to check for NULL values before performing operations. You can use the `IS NULL` clause to check for NULL values, and then use `COALESCE` to replace the missing values.

## Verification Task 2
Design Decision: You are building a customer database, and you need to decide whether to use `IFNULL` or `COALESCE` to handle missing values. Defend your decision using this topic.

## Solution 2
I would use `COALESCE` to handle missing values because it allows me to specify multiple arguments and returns the first non-NULL value. This is more flexible than `IFNULL`, which only allows two arguments and returns the second argument if the first argument is NULL.

## Verification Task 3
Code Review: The following code snippet is used to query the customer database:
```sql
SELECT name, email
FROM customers
WHERE email IS NOT NULL;
```
However, the code snippet has a subtle bug that causes it to return incorrect results. Find and fix the bug.

## Solution 3
The bug in the code snippet is that it does not check for NULL values in the `name` column. To fix the bug, you can add a check for NULL values in the `name` column using the `IS NOT NULL` clause:
```sql
SELECT name, email
FROM customers
WHERE email IS NOT NULL AND name IS NOT NULL;
```
Alternatively, you can use `COALESCE` to replace missing values in the `name` column:
```sql
SELECT COALESCE(name, 'Unknown') AS name, email
FROM customers
WHERE email IS NOT NULL;
```

## What Comes Next
The next topic in the roadmap is Views. This topic follows logically from NULL Functions & Conditional Logic because Views often involve complex queries that require handling missing or unknown data. One concrete concept from this topic that will reappear in Views is the use of `COALESCE` to replace missing values.

## Reference Summary
NULL Functions & Conditional Logic are essential for handling missing or unknown data in SQL, and can be used to perform complex conditional logic and make decisions based on conditions. The key functions in this topic include `COALESCE`, `NULLIF`, `IFNULL`, and `CASE WHEN`. The most common production mistake is not checking for NULL values before performing operations, which can result in NULL or incorrect results. This topic connects to the project by allowing us to handle missing or unknown data in the customer database and perform complex queries to personalize customer recommendations. A real company that uses this exact pattern is Amazon, which uses NULL Functions & Conditional Logic to handle missing or unknown data in their customer database and perform complex queries to personalize customer recommendations. This matters to you because it allows you to build a robust and scalable customer database that can handle complex queries and provide accurate results.