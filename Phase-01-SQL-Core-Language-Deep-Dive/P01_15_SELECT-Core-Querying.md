# SELECT — Core Querying

## What Is This?
A `SELECT` query is how you ask a database to show you exactly what you need from its stored information. Think of it like a library card catalog: you specify which books (data) you want, how to sort them, and whether to skip some (for browsing). This is the first tool you use to turn raw data into useful answers.

## How It Works Internally

### LAYER 1: Minimum viable version
```sql
-- Retrieve specific columns from a table (like listing only book titles and authors)
SELECT product_name, price FROM products;
```

### LAYER 2: Why the simple version breaks
```sql
-- SELECT * returns all columns, which might include sensitive data (like ISBN numbers) we shouldn't expose
SELECT * FROM users; -- ❌ Avoid in production
```

### LAYER 3: Production version
```sql
-- Fetch unique customer emails sorted by sign-up date, limited to 100 rows
SELECT DISTINCT email 
FROM customers 
WHERE registration_date > '2023-01-01'
ORDER BY registration_date DESC
LIMIT 100;
```

### LAYER 4: Edge cases
1. **Pagination trap**: `LIMIT 100 OFFSET 10000` becomes slow as `OFFSET` skips more rows. Keyset pagination (filtering by last ID) is faster for large datasets.
2. **NULL confusion**: `SELECT * FROM orders WHERE status = NULL` returns nothing. Use `IS NULL` instead.

**CORE INSIGHT**: Always specify columns instead of `SELECT *` to avoid brittle queries that break when tables change.

---

## Syntax and Structure
```sql
-- Basic query structure with explanations
SELECT 
  product_id,        -- Pick specific columns
  name AS product,   -- Rename column in output
  price * 0.85 AS discounted_price  -- Calculate on the fly
FROM 
  products           -- From this table
WHERE 
  category = 'Electronics'  -- Filter rows first
ORDER BY 
  price DESC NULLS LAST  -- Sort by highest prices
LIMIT 10 OFFSET 0;     -- Get first 10 results
```

---

## Practical Example
```sql
-- Get active products with custom pricing labels
SELECT 
  id, 
  name, 
  price,
  CASE 
    WHEN price < 100 THEN 'Budget' 
    WHEN price < 500 THEN 'Mid-range' 
    ELSE 'Premium' 
  END AS price_category
FROM products
WHERE is_active = TRUE
ORDER BY price ASC
LIMIT 20;
```

---

## How This Connects to the Project

1. **BEFORE**: The e-commerce project shows a blank product catalog because we haven't retrieved any data.
2. **AFTER**: We display products with prices, descriptions, and categories by querying the database.
3. **File Location**: This query lives in `backend/api/product_routes.py` inside the `get_all_products()` function.
4. **Real-World Use**: Shopify uses similar queries to power their product listings, balancing performance with flexibility for filtering/sorting.

---

## Common Mistakes Beginners Make

1. **SELECT * in production**: Returns all columns, which breaks when tables change and leaks data you might not want exposed.
2. **Missing quotes on strings**: 
   ```sql
   -- Wrong idea: No quotes for strings
   SELECT * FROM users WHERE status = premium;
   -- Correct idea: Always quote strings
   SELECT * FROM users WHERE status = 'premium';
   ```
3. **Underestimating OFFSET**: Pagination with large offsets becomes slow as the database counts skipped rows.
4. **NULL comparisons**: Writing `WHERE column = NULL` instead of `WHERE column IS NULL` returns empty results silently.
5. **Interview question**: "What's the difference between `LIMIT 10 OFFSET 0` and `FETCH FIRST 10 ROWS ONLY`?" 
   - Surface answer: They both limit rows.
   - Production answer: `FETCH` is SQL standard with more flexible options like `WITH TIES` for ties in sorting.

---

## Verification Tasks

### Task 1 — Debug This
Your dashboard shows duplicate product names in search results, but you used `SELECT DISTINCT`. The query:
```sql
SELECT DISTINCT name FROM products ORDER BY name;
```
**Symptom**: "I see 'iPhone 15' appearing twice in the search results."
**Evidence**: The products table has entries with identical names but different categories.

### Solution 1
Add category to the DISTINCT clause:
```sql
SELECT DISTINCT name, category FROM products ORDER BY name;
-- Or rename columns:
SELECT DISTINCT name AS product_name, category FROM products ORDER BY name;
```

### Task 2 — Design Decision
You're building a paginated admin panel for order reviews. Should you use `LIMIT/OFFSET` or keyset pagination?
**Decision**: Use keyset pagination (`WHERE id > last_seen_id LIMIT 50`) for large datasets because it avoids counting skipped rows and maintains performance.

### Task 3 — Code Review
```sql
SELECT id, name, price 
FROM products 
WHERE category = 'Toys' 
ORDER BY price DESC NULLS LAST
LIMIT 10 OFFSET 0;
```
**Bug**: The `NULLS LAST` clause works in PostgreSQL but fails in MySQL, which requires `ORDER BY price DESC` with a separate `NULLS LAST` extension.

---

## What Comes Next
After mastering basic queries, you'll learn **Aggregate Functions & GROUP BY**, which lets you summarize data (like total sales per product category). This builds on your ability to filter and sort data, adding tools to calculate totals and averages across groups.

---

## Reference Summary
A `SELECT` query defines what data to retrieve, how to filter and sort it, and how many results to return. The most common mistake is using `SELECT *` in production, which breaks when table structures change and leaks unintended data. Always specify columns and use `LIMIT` with `OFFSET` cautiously for pagination. In your e-commerce project, this enables building product listings with proper sorting and filtering. The next topic will teach you to summarize this data into metrics like average prices and total sales.