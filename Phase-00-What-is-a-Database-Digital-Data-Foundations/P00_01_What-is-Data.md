## What Is This?
Data is the raw material of computation — individual facts, measurements, or symbols with no inherent meaning. Imagine a library’s card catalog: thousands of index cards with numbers and names (raw data). Only when a librarian connects a card to a specific book’s location does that data become *information* (e.g., "Card #42 → *Moby Dick* in Aisle 3"). Data alone is inert; context transforms it into actionable knowledge.

## How It Works Internally
### Layer 1 — Minimum Viable Version
Data exists as isolated values:  
- `42` (a number)  
- `"Alice"` (text)  
- `2024-01-01` (a date)  
These hold no meaning until assigned purpose. Like unlabeled jars in a pantry: flour, salt, and sugar are indistinguishable without context.

### Layer 2 — Why the Simple Version Breaks
Raw data causes ambiguity. If a system logs `42`, is that:  
- A customer ID?  
- Temperature in Celsius?  
- A transaction amount?  
Without context, systems make catastrophic errors (e.g., treating a date as a numeric ID).

### Layer 3 — The Production Version
Data gains meaning through **context**:  
1. **Structure**: Organized into tables (e.g., `customers` table defines `customer_id`, `name`, `join_date`).  
2. **Schema**: Rules defining data types (e.g., `account_number` must be 10 digits).  
3. **Relationships**: Links between data (e.g., `transaction.customer_id` references `customers.id`).  
4. **Metadata**: Descriptions explaining *what* data represents (e.g., "join_date: When account was opened").

### Layer 4 — Edge Cases and Failure Modes
- **Edge Case 1**: Unstructured data overload (e.g., free-text notes in a banking app). *Symptom*: Slow searches. *Fix*: Add tags/categories to create structure.  
- **Edge Case 2**: Binary corruption (e.g., a flipped bit changes `balance: 100` → `balance: 1000`). *Symptom*: Incorrect calculations. *Fix*: Checksums during storage.  
**CORE INSIGHT**: Data without context is noise; structure turns noise into signal.

## Syntax and Structure
```text
# STEP 1: CPU receives raw input "42" from a sensor (e.g., temperature reading)
# STEP 2: Memory reserves a storage slot (like a labeled jar)
# STEP 3: CPU writes the value "42" into the slot
# STEP 4: Schema defines this slot as "temperature_celsius" in a "weather" table
# STEP 5: CPU links this slot to a timestamp slot ("2024-01-01")
# STEP 6: Data persists on disk even after power loss
# → In Phase 1 we will write this in real SQL
```

## Common Mistakes Beginners Make
- **Confusing data and information**: Storing `2024-01-01` without noting *what* it measures (e.g., "account creation date" vs. "last login").  
- **Ignoring persistence**: Assuming data exists only while a program runs (losing all transactions after a crash).  
- **Misinterpreting semi-structure**: Treating JSON `{ "balance": 100 }` as reliable without validating the `balance` field’s existence.  
- **Overlooking binary reality**: Thinking data "lives" in text files, not as 0s/1s on disk.  
- **Interview question**: *"Why can’t we store all bank data in a single spreadsheet?"*  
  Surface answer: "It gets messy." Production answer: "No ACID guarantees, scalability limits, and zero audit trails for money movements."

## Verification Task 1 — Debug This
"Your system shows duplicate customer records with the same name but different IDs. You have 10,000 entries labeled only `customer_data`." Diagnose and fix.

## Solution 1
1. **Missing context**: Raw names (`"Alice"`) lack unique identifiers.  
2. **Fix**: Add structured `customer_id` to all records. Use schema rules to enforce uniqueness.  
3. **Prevent recurrence**: Define metadata (e.g., "customer_id: Unique 8-digit number").

## Verification Task 2 — Design Decision
"Building NexaBank’s transaction ledger. Use structured tables (SQL) or semi-structured JSON documents? Defend using this topic."

## Solution 2
Choose **structured tables**. Transactions require rigid schema enforcement (e.g., `amount DECIMAL(10,2) NOT NULL`) to prevent fractional cents or missing fields. JSON’s flexibility risks invalid data in critical financial operations.

## Verification Task 3 — Code Review
```text
# PSEUDOCODE — Storage attempt
# STEP 1: Receive input "42"
# STEP 2: Write to memory slot "x"
# STEP 3: Program exits → data vanishes
```
*Bug*: Data doesn’t persist. Fix the missing step.

## Solution 3
Add **persistence context**:  
```text
# STEP 4: Copy slot "x" to disk file "transactions.db"
```
Without explicit storage instructions, data dies with the process.

## What Comes Next
The next topic is **File Systems & How Databases Use Disk**. This follows directly because data persistence (taught here) relies on physical storage mechanisms. You’ll learn how databases convert structured data into files, manage disk space, and ensure crash recovery — turning abstract "storage" into hardware reality. The concept of binary representation from this topic will reappear as you explore how 0s/1s map to files.

## Reference Summary
Data is raw, context-free facts (e.g., `42`); information adds meaning through structure. Computers store data persistently to survive program crashes, using schemas to define relationships. Structured data (SQL tables) enforces rules, while semi-structured (JSON) and unstructured (images) data offer flexibility at the cost of rigor. Everything ultimately reduces to binary 0s/1s on disk. At NexaBank, this foundation ensures transaction integrity: a missing schema rule could allow invalid withdrawals. Master this to design systems where `balance: 100` always means exactly one thing.