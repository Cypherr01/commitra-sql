# Subqueries — Complete

## What Is This?

A **subquery** is a query written inside another query, like a Russian nesting doll where one question unpacks another. Imagine you're at a library: you ask the librarian for books by a famous author (outer query), and they check a separate catalog to find all books by that author (inner query). This layered approach lets you solve complex problems step-by-step without writing massive, unreadable code.

## How It Works Internally

### LAYER 1: Minimum Viable Version
```sql
-- Find customers with orders over $100
SELECT customer_name 
FROM customers 
WHERE customer_id IN (
    -- Inner query gets IDs of orders > $100
    SELECT order_customer_id 
    FROM orders 
    WHERE total > 100
)
```
This shows the simplest use: an `IN` clause with a subquery in `WHERE`. The outer query filters customers, and the inner query provides a list of matching IDs.

### LAYER 2: Why the Simple Version Breaks
If the inner query returns multiple rows when a single value is expected:
```sql
-- Will fail if subquery returns >1 row
SELECT customer_name 
FROM customers 
WHERE customer_id = (
    SELECT order_customer_id 
    FROM orders 
    WHERE total > 100
)
```
The `=` operator requires exactly one match. This is a common beginner mistake that causes runtime errors.

### LAYER 3: Production Version
```sql
-- Safe version with correlation
SELECT c.customer_name 
FROM customers c
WHERE c.customer_id = ANY (
    SELECT o.order_customer_id
    FROM orders o
    WHERE o.total > 100
)
```
Using `ANY` handles multiple results gracefully. We also added table aliases (`c`/`o`) to avoid name collisions when queries grow.

### LAYER 4: Edge Cases
1. **Empty results**: If the subquery returns no rows, `IN` returns FALSE but `EXISTS` returns NULL.
2. **Performance trap**: Correlated subqueries (explained next) can cause exponential slowdowns with large datasets.

### CORE INSIGHT
Subqueries are like helper functions in code: they isolate logic, improve readability, and prevent code duplication. The key is choosing the right comparison operator (`IN`, `=`, `ALL`, etc.) for your data shape.

### Full Topic Coverage
1. **Subquery**: A query nested inside another query  
2. **Scalar subquery**: Returns one value (e.g., `SELECT MAX(price) FROM products`)  
3. **Row subquery**: Returns one row with multiple columns (e.g., `(1, 'Alice')`)  
4. **Table subquery**: Returns many rows/columns (used in `FROM`)  
5. **IN (SELECT ...)**: Checks if value exists in subquery results  
6. **= (SELECT ...)**: Requires single-row result (error otherwise)  
7. **ALL/ANY/SOME**: Compare to all or any values in a set  
8. **Correlated subquery**: References outer query variables (re-executed per row)  
9. **Uncorrelated subquery**: Independent execution (faster)  
10. **Subquery in SELECT**: Creates computed columns  
11. **Subquery in FROM**: Creates derived tables  
12. **Subquery in HAVING**: Filters aggregated groups  
13. **EXISTS vs IN**: `EXISTS` stops at first match; `IN` builds full list  
14. **Scalar vs JOIN**: Subqueries are often more readable, but `JOIN` is faster for big datasets  

## Syntax and Structure
```sql
-- Basic subquery in WHERE clause
SELECT column 
FROM table 
WHERE column [operator] (
    -- This is the subquery
    SELECT column 
    FROM other_table 
    WHERE condition
)
```

## Practical Example
```sql
-- Find customers who ordered > $100
SELECT customer_name
FROM customers
WHERE customer_id = ANY (
    SELECT order_customer_id
    FROM orders
    WHERE total > 100
)
```

## How This Connects to the Project

**BEFORE**: Your e-commerce dashboard can't identify high-value customers. Reports show all customers equally.  
**AFTER**: Using subqueries, you filter customers by their order history.  
**File**: `queries/customer_analysis.sql`  
**Company**: Amazon uses subqueries for customer segmentation and purchase pattern analysis.

## Common Mistakes Beginners Make

1. **Using `=` with multiple results**: The symptom is a cryptic "more than one row" error when the subquery returns multiple rows.  
2. **Silent correlated failure**:  
   ```sql
   -- Wrong: Missing reference to outer query
   SELECT customer_name
   FROM customers c
   WHERE c.customer_id = (
       SELECT order_customer_id
       FROM orders o
       WHERE total > 100
   )
   ```
   This will return inconsistent results because the subquery isn't tied to the outer query.  
3. **Ignoring performance**: Correlated subqueries can cause O(n²) runtime, which breaks at scale.  
4. **Missing parentheses**: Forgetting parentheses around subqueries in `FROM` causes syntax errors.  
5. **Interview question**: *When would you use `EXISTS` vs `IN`?*  
   - Surface answer: `EXISTS` checks for existence, `IN` filters values.  
   - Production answer: `EXISTS` is faster for large datasets because it stops after the first match and doesn't materialize the full result set.

## Verification Tasks

### Task 1 — Debug This
Your query returns no results. The subquery is:
```sql
SELECT name FROM users WHERE id = (SELECT user_id FROM logs WHERE action = 'login')
```
**Symptom**: No users returned, but you know logins exist.  
**Evidence**: `SELECT * FROM logs WHERE action = 'login'` shows many rows.  
**Solution**: Change `=` to `IN` because the subquery returns multiple rows.

### Task 2 — Design Decision
You need to find products with prices above all electronics. Use `ALL` or `> (SELECT MAX(...))`?  
**Solution**: Use `> ALL (SELECT price FROM products WHERE category = 'electronics')` for clarity. Both work, but `ALL` makes the intention explicit.

### Task 3 — Code Review
```sql
SELECT customer_name 
FROM customers 
WHERE customer_id NOT IN (
    SELECT order_customer_id
    FROM orders
    WHERE order_date > '2023-01-01'
)
```
**Bug**: Returns incorrect results when `order_customer_id` has NULL values.  
**Fix**: Add `AND order_customer_id IS NOT NULL` to the subquery.

## What Comes Next

The next topic is **Window Functions — Complete**, where you'll learn how to calculate running totals, ranks, and moving averages without collapsing rows. Subqueries are crucial here because window functions often use subqueries to define complex partitions or nested calculations. For example, you'll use subqueries to create custom ranking criteria in `OVER()` clauses.

## Reference Summary

Subqueries solve problems in layers, like peeling an onion. They let you isolate logic, handle complex conditions, and create derived datasets. The most common mistake is using `=` when your subquery returns multiple rows—always start with `IN` when unsure. This concept directly enables your e-commerce project to analyze customer behavior patterns, forming the foundation for window functions where nested logic becomes essential for advanced analytics. Mastering subqueries ensures you can write maintainable, efficient SQL that scales with your data.