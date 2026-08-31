## What Is This?
Data is the raw material of computation — individual facts, measurements, or observations with no inherent meaning. Imagine a recipe's ingredients: "2 eggs," "1 cup flour," and "350°F" are just numbers and words until combined into a cake. Data becomes **information** when given context, like "preheat oven to 350°F for 30 minutes." Computers store data because programs can't function if values disappear when the power turns off — like a bakery needing a saved recipe to bake again tomorrow.

## How It Works Internally
### The Core Layers Explained
1. **Data**: Standalone values like `42`, `"Alice"`, or `2024-01-01`. A single temperature reading from a sensor is data.
2. **Information**: Data + context. "The server room temperature hit 42°C at 2024-01-01 14:30" tells engineers to act.
3. **Persistence**: Computers save data to hardware (disks, chips) so it survives program crashes or reboots. Your banking app relies on this to remember transactions.
4. **Structured data**: Organized in fixed tables with defined types. Like a spreadsheet:

   ```text
   | account_id | balance | owner      |
   |------------+---------+----------------|
   | 1001       | 150.00  | "Alice"     |
   ```

5. **Semi-structured data**: Flexible formats like JSON or XML. No rigid schema:

   ```json
   {"transaction": {"amount": 50, "note": "coffee"}}
   ```

6. **Unstructured data**: Freeform content like emails, images, or audio. A customer support voicemail can't fit into tables.
7. **Binary storage**: All data becomes streams of 0s and 1s. The text `"Alice"` becomes `01000001 01101100 ...` in memory.
8. **Why storage matters**: Every application—from NexaBank's ledgers to social media—depends on reliably saved data. Without persistence, your account balance would reset daily.

### Layer 1 — Minimum Viable Version
A single value stored temporarily:
```text
# STEP 1: Program starts
# STEP 2: CPU creates "x" label in memory
# STEP 3: Value 42 written to memory slot
# STEP 4: Program ends → data vanishes
```

### Layer 2 — Why the Simple Version Breaks
Data disappears when the program stops. Imagine NexaBank's system forgetting all transactions nightly. **Symptom**: Users log in to see zero account history. **Cause**: No persistent storage.

### Layer 3 — The Production Version
Data saved to non-volatile storage (disks):
```text
# STEP 1: Program starts
# STEP 2: Load existing data from disk into memory
# STEP 3: Modify data (e.g., update balance)
# STEP 4: Write changes back to disk periodically
# STEP 5: Handle crashes: Auto-save before shutdown
```

### Layer 4 — Edge Cases and Failure Modes
1. **Corrupted writes**: Power outage during disk save → partial data. **Fix**: Use write-ahead logging (record changes before applying).
2. **Type mismatch**: Storing text in a number field → calculation errors. **Fix**: Enforce strict data types.
CORE INSIGHT: **Data without context is useless; without persistence, it's temporary; without structure, it's chaos.**
## Syntax and Structure
```text
# PHASE 0 PSEUDOCODE: How data storage works conceptually
# STEP 1: User inputs "deposit 100" → raw data "100"
# STEP 2: CPU checks if "100" is valid number (context added)
# STEP 3: Find account record in memory (structured table)
# STEP 4: Update balance field from 50 → 150 (modification)
# STEP 5: Write updated table to disk (persistence)
# STEP 6: Confirm success to user (information created)
# In Phase 1 we will write this in real SQL
```

## Common Mistakes Beginners Make
- **Confusing data and information**: Storing `2024-01-01` without noting it's a "transaction date" makes it meaningless later.
- **Ignoring persistence**: Forgetting to save data before program exit (e.g., unsaved document loss).
- **Misusing types**: Saving dates as text → can't sort chronologically.
- **Overlooking structure**: Dumping all customer data into one JSON blob → impossible to query efficiently.
- **Interview question**: *"Why can't we just store everything as text?"*  
  **Surface answer**: "Text is flexible."  
  **Production answer**: "Numbers enable math; dates enable timelines; structured types enable queries. NexaBank would fail to calculate interest on text balances."

## Verification Task 1 — Debug This
Your system shows **account balances resetting to zero after nightly maintenance**. You have:  
- Evidence: Disk writes succeed but data isn't loaded next day.  
Diagnose and fix.

## Solution 1
**Diagnosis**: The system writes data to a temporary disk cache but never flushes to permanent storage.  
**Fix**: Implement periodic forced writes to persistent storage (e.g., `fsync` system calls) and verify writes complete before shutdown.

## Verification Task 2 — Design Decision
Building a transaction log for NexaBank. Use **structured tables** or **JSON blobs**? Defend using this topic.

## Solution 2
**Choose structured tables**:  
- Transactions require ACID compliance (atomic updates, crash recovery). Structured schemas enforce integrity (e.g., `amount` must be numeric).  
- JSON would hide corruption (e.g., `"amount": "fifty"`) and prevent efficient querying. NexaBank's ledger demands precision.

## Verification Task 3 — Code Review
```text
# Pseudocode snippet with subtle bug
# STEP 1: Read customer data from disk
# STEP 2: Parse into memory as freeform text
# STEP 3: Extract "balance" field via string search
# STEP 4: Add new transaction amount
# STEP 5: Write updated text back to disk
```
Find and fix the bug.

## Solution 3
**Bug**: No type validation. If "balance" is stored as `"$50"` instead of `50`, arithmetic will fail.  
**Fix**: Add schema enforcement during parsing (e.g., convert balance to integer, reject invalid formats).

## What Comes Next
The next topic is **File Systems & How Databases Use Disk**. This follows logically because understanding *what* data is (raw facts needing persistence) leads directly to *where* and *how* it's physically stored on hardware. The binary representation and persistence concepts from this topic explain why file systems organize data into blocks and directories.

## Reference Summary
Data is raw, context-free facts (e.g., `42`) that computers store persistently in binary form (0s/1s) to survive program restarts. It becomes information when given meaning (e.g., "server temperature alert"). Structured data (tables), semi-structured (JSON), and unstructured (images) formats serve different needs. Storage matters because every application—like NexaBank's transaction ledger—relies on durable, organized data. The most common mistake is neglecting structure or persistence, leading to data loss or corruption. This foundation enables databases to manage the complex relationships in banking systems.