## What Is This?
PostgreSQL window functions and advanced queries are a set of powerful tools that allow you to perform complex data analysis and calculations on your data, enabling you to extract valuable insights and statistics from your database. Imagine you're the manager of a large library, and you want to know the most popular books in each genre, as well as the overall most popular books across all genres - window functions would help you achieve this by allowing you to calculate rankings and aggregations over specific subsets of your data.

## How It Works Internally
### Introduction to Window Functions
Window functions are a type of query that allows you to perform calculations across a set of rows that are related to the current row, such as aggregating values or ranking rows. They are similar to aggregate functions, but unlike aggregate functions, which group rows into a single output row, window functions return multiple rows, one for each input row.

### Standard Window Functions
All standard window functions from Phase 1 apply to PostgreSQL, including functions like `ROW_NUMBER()`, `RANK()`, and `NTILE()`. These functions allow you to perform common data analysis tasks, such as assigning a unique number to each row, ranking rows based on a specific column, or dividing rows into a specified number of groups.

### Filter Clause on Aggregates
The `FILTER (WHERE condition)` clause on aggregates allows you to perform partial aggregation, where you can apply an aggregate function to a subset of rows that meet a specific condition. For example, you can use `SUM(column_name) FILTER (WHERE column_name > 0)` to calculate the sum of only the positive values in a column.

### Distinct On
The `DISTINCT ON (col)` clause is a PostgreSQL-specific feature that allows you to return the first row for each distinct value of a column. This can be useful when you want to retrieve a single representative row for each group of duplicate values.

### Returning Clause
The `RETURNING` clause allows you to specify which columns to return after an `INSERT`, `UPDATE`, or `DELETE` operation. This can be useful when you want to retrieve the affected rows after a modification operation.

### Lateral Joins
Lateral joins allow you to reference columns from the outer query in the subquery, enabling you to perform more complex joins and aggregations. The subquery can be thought of as a function that takes the outer query's columns as input and returns a set of rows.

### Tablesample
The `TABLESAMPLE` clause allows you to randomly sample a subset of rows from a table. There are two types of sampling: `SYSTEM` and `BERNOULLI`. `SYSTEM` sampling samples a percentage of pages, while `BERNOULLI` sampling samples a percentage of rows.

### Copy To/From with Functions
The `COPY TO` and `COPY FROM` commands can be used with functions to import and export data from a table. This can be useful when you want to perform data transformations or aggregations on a large dataset.

### Unnest with Ordinality
The `UNNEST` function allows you to expand an array into a set of rows. When used with the `ORDINALITY` keyword, you can also retrieve the position of each element in the array.

### Values Clause as Table
The `VALUES` clause can be used as a table in a query, allowing you to specify a set of rows as a derived table. This can be useful when you want to perform a query on a small set of data that is not stored in a table.

### Generate Series
The `GENERATE_SERIES` function generates a series of numbers over a specified range. This can be useful when you want to create a set of numbers for a query, such as generating a set of dates or IDs.

## Syntax and Structure
```sql
-- Example of a window function
SELECT 
  column1,
  ROW_NUMBER() OVER (ORDER BY column1) AS row_num
FROM 
  table_name;

-- Example of filter clause on aggregates
SELECT 
  SUM(column1) FILTER (WHERE column1 > 0) AS sum_positive
FROM 
  table_name;

-- Example of distinct on
SELECT DISTINCT ON (column1) 
  column1, 
  column2
FROM 
  table_name
ORDER BY 
  column1, 
  column2;

-- Example of returning clause
INSERT INTO table_name (column1, column2)
VALUES ('value1', 'value2')
RETURNING 
  column1, 
  column2;

-- Example of lateral join
SELECT 
  column1, 
  subquery.column2
FROM 
  table_name
CROSS JOIN LATERAL (
  SELECT 
    column2
  FROM 
    another_table
  WHERE 
    another_table.column1 = table_name.column1
) AS subquery;

-- Example of tablesample
SELECT 
  column1
FROM 
  table_name
TABLESAMPLE SYSTEM (10);

-- Example of copy to/from with functions
COPY table_name TO '/path/to/file' WITH CSV;

-- Example of unnest with ordinality
SELECT 
  UNNEST(array['value1', 'value2']) WITH ORDINALITY AS (value, position);

-- Example of values clause as table
SELECT 
  column1
FROM 
  (VALUES ('value1'), ('value2')) AS table_name (column1);

-- Example of generate series
SELECT 
  generate_series(1, 10) AS series;
```

## Practical Example
To demonstrate the use of window functions, let's consider an example where we have a table of sales data with columns for the date, product, and amount sold. We want to calculate the total sales for each product over time, as well as the ranking of each product by total sales.
```sql
-- Create a sample sales table
CREATE TABLE sales (
  date DATE,
  product VARCHAR(50),
  amount_sold DECIMAL(10, 2)
);

-- Insert some sample data
INSERT INTO sales (date, product, amount_sold)
VALUES 
  ('2022-01-01', 'Product A', 100.00),
  ('2022-01-02', 'Product A', 200.00),
  ('2022-01-03', 'Product B', 50.00),
  ('2022-01-04', 'Product B', 75.00),
  ('2022-01-05', 'Product C', 150.00);

-- Calculate the total sales for each product over time
SELECT 
  product,
  date,
  amount_sold,
  SUM(amount_sold) OVER (PARTITION BY product ORDER BY date) AS total_sales
FROM 
  sales;

-- Calculate the ranking of each product by total sales
SELECT 
  product,
  SUM(amount_sold) AS total_sales,
  RANK() OVER (ORDER BY SUM(amount_sold) DESC) AS sales_rank
FROM 
  sales
GROUP BY 
  product;
```

## How This Connects to the Project
Before learning about window functions, our City Events Tracker project was limited in its ability to analyze and report on event data. With the introduction of window functions, we can now calculate statistics such as the most popular events, the top venues, and the busiest days of the week. The `city_events` table can be used to demonstrate the use of window functions, such as calculating the total attendance for each event over time or ranking the events by attendance.

## Common Mistakes Beginners Make
**Most common mistake**: Not understanding the difference between window functions and aggregate functions. Window functions return multiple rows, one for each input row, while aggregate functions group rows into a single output row.
**Looks right but is silently wrong**: Using the `FILTER` clause on an aggregate function without specifying the correct condition. This can lead to incorrect results or errors.
**Seems optional but critical at scale**: Not using the `DISTINCT ON` clause when retrieving a single representative row for each group of duplicate values. This can lead to performance issues or incorrect results.
**Missed config or flag**: Not specifying the correct sampling method when using the `TABLESAMPLE` clause. This can lead to incorrect results or errors.
**Interview question this topic generates**: How would you calculate the top N products by sales using window functions?

## Verification Task 1
Debug the following query, which is intended to calculate the total sales for each product over time:
```sql
SELECT 
  product,
  date,
  amount_sold,
  SUM(amount_sold) OVER (ORDER BY date) AS total_sales
FROM 
  sales;
```
## Solution 1
The issue with the query is that it is not partitioning the data by product, so the total sales will be calculated across all products. To fix this, we need to add the `PARTITION BY` clause:
```sql
SELECT 
  product,
  date,
  amount_sold,
  SUM(amount_sold) OVER (PARTITION BY product ORDER BY date) AS total_sales
FROM 
  sales;
```

## Verification Task 2
Design a query to calculate the ranking of each event by attendance, using the `city_events` table. Should we use the `RANK()` or `DENSE_RANK()` function?
## Solution 2
We should use the `DENSE_RANK()` function, as it will assign consecutive ranks to events with the same attendance. The `RANK()` function would assign the same rank to events with the same attendance, and then skip a rank for the next event.

## Verification Task 3
Code review: The following query is intended to calculate the top 10 products by sales:
```sql
SELECT 
  product,
  SUM(amount_sold) AS total_sales
FROM 
  sales
GROUP BY 
  product
ORDER BY 
  total_sales DESC
LIMIT 10;
```
However, the query is not using window functions. How can we modify the query to use window functions instead?
## Solution 3
We can modify the query to use the `RANK()` function:
```sql
SELECT 
  product,
  total_sales
FROM (
  SELECT 
    product,
    SUM(amount_sold) AS total_sales,
    RANK() OVER (ORDER BY SUM(amount_sold) DESC) AS sales_rank
  FROM 
    sales
  GROUP BY 
    product
) AS subquery
WHERE 
  sales_rank <= 10;
```

## What Comes Next
The next topic in the roadmap is PostgreSQL Maintenance Commands. This topic is a natural follow-up to PostgreSQL Window Functions & Advanced Queries because it builds on the foundation of querying and analyzing data in PostgreSQL. In order to perform maintenance tasks, such as backing up and restoring databases, optimizing queries, and monitoring performance, it is essential to have a solid understanding of how to query and analyze data in PostgreSQL. One concrete concept from this topic that will reappear in PostgreSQL Maintenance Commands is the use of window functions to analyze and optimize query performance.

## Reference Summary
PostgreSQL window functions and advanced queries are a set of powerful tools that allow you to perform complex data analysis and calculations on your data. The key concepts include standard window functions, filter clause on aggregates, distinct on, returning clause, lateral joins, tablesample, copy to/from with functions, unnest with ordinality, values clause as table, and generate series. Common mistakes beginners make include not understanding the difference between window functions and aggregate functions, and not using the correct sampling method when using the `TABLESAMPLE` clause. The project connection is to the City Events Tracker, where window functions can be used to calculate statistics such as the most popular events and the top venues. This matters to you because it enables you to perform complex data analysis and calculations on your data, which is essential for making informed decisions and optimizing business processes.