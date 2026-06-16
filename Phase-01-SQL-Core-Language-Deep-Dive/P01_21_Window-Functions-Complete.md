## What Is This?
Window functions are a type of SQL function that allows you to perform calculations across a set of rows related to the current row, without collapsing the result into a single row. Think of it like a report that shows the sales performance of each salesperson, where you want to see not only their individual sales but also how they rank compared to their peers.

## How It Works Internally
### Window Function Basics
A window function is used to compute a value across a set of rows that are related to the current row, such as aggregating values or ranking rows. This is different from aggregate functions, which collapse the result into a single row.

### The `OVER()` Clause
The `OVER()` clause is used to define the window over which the function is applied. It specifies the rows that are related to the current row.

### `PARTITION BY`
The `PARTITION BY` clause is used to divide the rows into groups, similar to the `GROUP BY` clause, but it does not collapse the rows into a single row. Instead, it preserves the individual rows and applies the window function to each partition separately.

### `ORDER BY` within `OVER()`
The `ORDER BY` clause within the `OVER()` clause is used to define the order of the rows within the window. This is important for functions that depend on the order of the rows, such as ranking functions.

### `ROWS BETWEEN` / `RANGE BETWEEN`
The `ROWS BETWEEN` and `RANGE BETWEEN` clauses are used to define the frame within the window. The frame specifies the set of rows that are included in the calculation.

### Ranking Functions
There are several ranking functions available, including `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`. These functions assign a unique number to each row within the partition, based on the order of the rows.

### `NTILE(n)`
The `NTILE(n)` function divides the rows into n equal groups, based on the order of the rows.

### `PERCENT_RANK()` and `CUME_DIST()`
The `PERCENT_RANK()` and `CUME_DIST()` functions calculate the relative rank of each row within the partition, as a percentage.

### `LAG()` and `LEAD()`
The `LAG()` and `LEAD()` functions return the value of a column from a previous or next row, respectively.

### `FIRST_VALUE()` and `LAST_VALUE()`
The `FIRST_VALUE()` and `LAST_VALUE()` functions return the first or last value of a column within the window frame.

### `NTH_VALUE()`
The `NTH_VALUE()` function returns the nth value of a column within the window frame.

### Aggregate Functions as Window Functions
Any aggregate function, such as `SUM`, `AVG`, `COUNT`, `MIN`, and `MAX`, can be used as a window function.

### Running Totals and Averages
Window functions can be used to calculate running totals and averages, such as the total sales for each day or the average score for each student.

### Moving Averages
Window functions can be used to calculate moving averages, such as the average sales for the last 7 days.

### Cumulative Sums
Window functions can be used to calculate cumulative sums, such as the total sales for each month.

### Execution Order
Window functions are executed after the `WHERE`, `GROUP BY`, and `HAVING` clauses, but before the `ORDER BY` and `LIMIT` clauses.

## Syntax and Structure
```sql
-- Calculate the running total of sales for each day
SELECT 
  date,
  sales,
  SUM(sales) OVER (ORDER BY date) AS running_total
FROM 
  sales_table;
```

## Practical Example
```sql
-- Create a sample table
CREATE TABLE customers (
  id INT,
  name VARCHAR(255),
  order_value DECIMAL(10, 2)
);

-- Insert sample data
INSERT INTO customers (id, name, order_value)
VALUES
  (1, 'John', 100.00),
  (2, 'Jane', 200.00),
  (3, 'Bob', 50.00),
  (4, 'Alice', 150.00),
  (5, 'Mike', 250.00);

-- Calculate the rank of each customer by order value
SELECT 
  id,
  name,
  order_value,
  RANK() OVER (ORDER BY order_value DESC) AS rank
FROM 
  customers;
```

## How This Connects to the Project
Before using window functions, our project had incomplete data, as we were unable to rank customers by their order value. After applying window functions, we can now see the rank of each customer and calculate the difference in order value between consecutive ranks. The exact file and function name where this concept lives in the project is `customer_ranking.sql`. A real company that uses this exact pattern is Amazon, which uses window functions to rank products by sales and calculate the difference in sales between consecutive ranks.

## Common Mistakes Beginners Make
**Wrong idea:** Thinking that window functions are the same as aggregate functions. 
**Correct idea:** Window functions are used to perform calculations across a set of rows related to the current row, without collapsing the result into a single row.

## Verification Task 1
Debug the following query, which is supposed to calculate the running total of sales for each day: 
```sql
SELECT 
  date,
  sales,
  SUM(sales) AS running_total
FROM 
  sales_table
GROUP BY 
  date;
```
## Solution 1
The query is missing the `OVER` clause, which is necessary for window functions. The correct query should be:
```sql
SELECT 
  date,
  sales,
  SUM(sales) OVER (ORDER BY date) AS running_total
FROM 
  sales_table;
```

## Verification Task 2
Design a query to calculate the average order value for each customer, using either a subquery or a window function. Defend your choice.
## Solution 2
We can use a window function to calculate the average order value for each customer:
```sql
SELECT 
  id,
  name,
  order_value,
  AVG(order_value) OVER (PARTITION BY id) AS average_order_value
FROM 
  customers;
```
This is more efficient than using a subquery, as it avoids the need to repeat the calculation for each row.

## Verification Task 3
Find and fix the bug in the following query, which is supposed to calculate the rank of each customer by order value:
```sql
SELECT 
  id,
  name,
  order_value,
  RANK() OVER (ORDER BY order_value) AS rank
FROM 
  customers;
```
## Solution 3
The query is missing the `DESC` keyword, which is necessary to sort the customers in descending order by order value. The correct query should be:
```sql
SELECT 
  id,
  name,
  order_value,
  RANK() OVER (ORDER BY order_value DESC) AS rank
FROM 
  customers;
```

## What Comes Next
The next topic is Date & Time Functions, which is a prerequisite for working with date and time data in SQL. We will learn how to use date and time functions to extract and manipulate dates and times, and how to use them in combination with window functions to analyze data over time. This matters to you because you will be working with date and time data in your project, and you need to know how to extract and manipulate it correctly.

## Reference Summary
Window functions are a powerful tool in SQL that allow you to perform calculations across a set of rows related to the current row, without collapsing the result into a single row. They are used to rank rows, calculate running totals and averages, and perform other complex calculations. The `OVER` clause is used to define the window over which the function is applied, and the `PARTITION BY` clause is used to divide the rows into groups. Window functions are executed after the `WHERE`, `GROUP BY`, and `HAVING` clauses, but before the `ORDER BY` and `LIMIT` clauses. A common mistake beginners make is thinking that window functions are the same as aggregate functions. This concept is crucial for working with data in SQL, as it allows you to perform complex calculations and analysis.