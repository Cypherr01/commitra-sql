## What Is This?
Data is the raw building material of facts and figures — numbers, text, dates, or media — that holds no inherent meaning on its own. Imagine ingredients in a kitchen: flour, sugar, eggs. Alone, they're just items. Only when combined with a recipe (context) do they become a cake. Data becomes **information** when we add meaning through structure and relationships. This distinction is fundamental: without context, data is useless noise.

## How It Works Internally
### The 8 Layers of Data Reality
1. **Raw Data**: Unprocessed facts like `42`, `"Alice"`, or `2024-01-01`. A sensor reading, a keystroke, or a photo pixel. No meaning yet.
2. **Information**: Data + context. `"Alice"` becomes meaningful when linked to "customer name" in a transaction.
3. **Persistence**: Computers store data in memory/disk so it survives program crashes or reboots. Your saved documents rely on this.
4. **Structured Data**: Organized in tables with strict schemas (e.g., SQL databases). Like a spreadsheet: predictable columns (data types) and rows (records).
5. **Semi-Structured Data**: Flexible formats like JSON/XML. Think nested dictionaries: `{"user": "Alice", "orders": [101, 105]}`. No rigid schema.
6. **Unstructured Data**: Free-form content: emails, images, videos. A photo of a product review can't be directly queried like text.
7. **Binary Storage**: All data ultimately becomes 0s/1s. The text `"Hello"` becomes `01001000 01000101...` in memory/disk.
8. **Foundation of Apps**: Every app—from e-commerce to social media—relies on stored data. Without persistence, systems reset to zero on shutdown.

### Layer 1 — Minimum Viable Version
```text
# Raw data example:
# 1. Store the number 42 (no context)
# 2. Store the string "Alice" (no context)
# → This is data: just values with no relationships or meaning
```

### Layer 2 — Why the Simple Version Breaks
**Naive misunderstanding**: Treating all data as unstructured text. Example: Storing user profiles as free-form notes instead of structured fields. Result? Impossible to query "users over 18" or calculate averages.

### Layer 3 — The Production Version
Structured schema design:
```text
# 1. Define schema: "users" table with columns (id INT, name VARCHAR, age INT)
# 2. Enforce data types: Reject "age: 'twenty'"
# 3. Add relationships: Link to "orders" table via user_id
# → Now data has context and enables queries like "average age of customers"
```

### Layer 4 — Edge Cases and Failure Modes
1. **Data Corruption**:  
   - *Trigger*: Power outage during write → partial binary save.  
   - *Symptom*: Garbled text like "Al°¥ce" in user profiles.  
   - *Fix*: Checksums + backups.  
2. **Type Mismatch**:  
   - *Trigger*: Storing date as string `"30-Feb-2025"`.  
   - *Symptom*: Queries fail silently; invalid dates in reports.  
   - *Fix*: Strict schema validation.  
**CORE INSIGHT**: Structure transforms worthless bits into actionable information.

## Syntax and Structure
```text
# PHASE 0 PSEUDOCODE: How data storage works conceptually
# STEP 1: Application requests to save "user: Alice, age: 30"
# STEP 2: Database engine validates against schema (checks data types)
# STEP 3: Data is converted to binary: "Alice" → 01000001... (ASCII)
# STEP 4: Binary written to disk in allocated storage block
# STEP 5: Metadata (block location) saved in index for retrieval
# STEP 6: Confirmation returned: "Data persisted successfully"
# In Phase 1 we will write this in real SQL
```

## Common Mistakes Beginners Make
- **Confusing data and information**: Storing raw sensor readings without timestamps/units → unusable later.  
- **Ignoring structure**: Using JSON blobs for frequently queried data → slow searches.  
- **Forgetting persistence**: Assuming in-memory data survives crashes → losing unsaved work.  
- **Misunderstanding types**: Storing dates as strings → `"10-11-2025"` (ambiguous format).  
- **Interview question**:  
  *"Why not store everything as JSON?"*  
  **Surface answer**: "Flexibility for unstructured data."  
  **Production answer**: "But structured data enables fast queries, validation, and joins—critical for analytics."

## Verification Task 1 — Debug This
*Symptom*: User reports their profile data disappears after server restart.  
*Evidence*: Application uses in-memory dictionaries; no disk writes implemented. Diagnose and fix.

## Solution 1
**Diagnosis**: Missing persistence layer. In-memory data vanishes when the process dies.  
**Fix**: Implement structured storage (e.g., SQL database) to write data to disk. Add schema validation to ensure data integrity.

## Verification Task 2 — Design Decision
Building a product catalog. Use **structured tables** (SQL) or **semi-structured documents** (JSON)? Defend your choice using this topic.

## Solution 2
**Choose structured tables** for:  
- Products with fixed attributes (ID, price, inventory).  
- Enables efficient queries (e.g., "items under $50 in stock").  
**Choose semi-structured** only for variable attributes (e.g., user-generated tags). Structured data wins for predictable, relational commerce data.

## Verification Task 3 — Code Review
```text
# PSEUDOCODE SNIPPET (CONCEPTUAL BUG)
# STEP 1: Read user input as string: "age: 30"
# STEP 2: Split into parts: ["age:", "30"]
# STEP 3: Store second part as string in "age" column
# STEP 4: Later query: "SELECT users WHERE age > 25" → returns nothing
```
*Find the subtle bug that breaks queries.*

## Solution 3
**Bug**: Storing numeric age as a string (e.g., `"30"` vs 30).  
**Fix**: Convert input to integer before storage. Structured schemas require correct data types for comparisons.

## What Comes Next
**File Systems & How Databases Use Disk** is next because it explains *how* persistent data is physically organized. This topic established *why* persistence matters; the next reveals the mechanical implementation—converting binary data into files, blocks, and directories that databases rely on.

## Reference Summary
Data is raw, context-free facts (e.g., `42`, `"Alice"`) that only become useful information when structured with meaning. Computers persist data to survive shutdowns, organizing it as structured tables (SQL), flexible JSON, or unstructured media. Everything ultimately stores as 0s/1s. This foundation enables applications to retain state. The critical mistake? Ignoring structure, leading to unqueryable chaos. In your Commerce Insight Hub project, defining structured entities (users, products) with validated data types ensures reliable analytics. Master this, and you'll understand why file systems—the next topic—are databases' physical backbone.