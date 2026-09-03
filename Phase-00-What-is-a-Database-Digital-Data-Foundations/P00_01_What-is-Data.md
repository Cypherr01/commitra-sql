## What Is This?
Data is the foundational raw material of computing — individual facts and figures like `42`, `"Alice"`, or `2024-01-01` that hold no inherent meaning on their own. Think of it like bricks: a single brick (data point) is just a shaped object. Only when you see a wall (information) do you understand its purpose. Computers rely on data as their universal building block.

## How It Works Internally
### Layer 1 — Minimum Viable Version
- **Data**: Standalone values (numbers, text, dates) with zero context.  
  Example: `3.14`, `"2025-03-15"`, `true`.  
- **Information**: Data + context. Adding meaning: "3.14 is today's temperature in Celsius."  
- **Persistence**: Computers save data to hardware (e.g., disks) so it survives power loss.  
- **Structured**: Tables with fixed columns (e.g., `customers: [id, name, email]`).  
- **Semi-structured**: Flexible formats like JSON: `{"name": "Alice", "age": 30}`.  
- **Unstructured**: Raw media (photos, videos) or free-text documents.  
- **Binary**: All data becomes `0`s and `1`s for machine storage.  
- **Foundation**: Applications exist to collect, process, and deliver data.

### Layer 2 — Why the Simple Version Breaks
Ignoring structure turns data into chaos. Example: Storing user details as unstructured text:  
`"Alice, 30, alice@email.com"`  
Fails when parsing: Is "30" an age or ID? Missing context causes errors.

### Layer 3 — The Production Version
Add schema/context:  
- **Structured**: Define `users(id INT, name TEXT, email TEXT)`.  
- **Semi-structured**: Use JSON schemas to validate key-value pairs.  
- **Unstructured**: Tag media with metadata (e.g., "2024-01-01_wedding.jpg").  
- **Binary**: Convert all formats to bytes via encoding (e.g., UTF-8 for text).

### Layer 4 — Edge Cases and Failure Modes
1. **Edge Case 1**: Unstructured data overload.  
   *Trigger*: Storing 1TB of unlabeled sensor readings.  
   *Symptom*: Impossible to query meaningful patterns.  
   *Fix*: Add structured metadata (timestamps, device IDs).  
2. **Edge Case 2**: Binary corruption.  
   *Trigger*: Power failure during write.  
   *Symptom*: File opens as gibberish.  
   *Fix*: Use error-checking codes during storage.  
CORE INSIGHT: Data without context is useless noise.

## Syntax and Structure
```text
# STEP 1: Collect raw input (e.g., user types "Alice" and clicks "Submit")
# STEP 2: Validate format (is "Alice" text? Does it match expected patterns?)
# STEP 3: Attach meaning (label "Alice" as a customer name)
# STEP 4: Convert to binary (ASCII: 'A'=65, 'l'=108, etc. → 01000001 01101100...)
# STEP 5: Save to storage (write binary 0s/1s to disk sectors)
# STEP 6: Retrieve when needed (read binary → convert back to "Alice")
In Phase 1 we will write this in real code.
```

## Common Mistakes Beginners Make
- **Confusing data and information**: Storing `42` without noting it’s "user age" makes it meaningless later.  
- **Wrong idea**: Freeform text is easiest.  

```text
  # BAD: Unstructured user entry
  "Alice, 30, alice@email.com"
```
  **Correct idea**: Use structured fields: `name: "Alice"`, `age: 30`.  
- **Ignoring persistence**: Assuming data lives in RAM forever (crashes erase it).  
- **Missing binary conversion**: Forgetting all data becomes 0s/1s (e.g., emojis need UTF-8 encoding).  
- **Interview question**: "Why not store everything as text?"  
  *Surface answer*: "Text is flexible."  
  *Production answer*: "Numbers/dates need math/sorting; text can’t handle that efficiently."

## Verification Task 1 — Debug This
Your system shows: User profiles disappear after restarting the app. You have: Data stored only in memory (RAM). Diagnose and fix.

## Solution 1
**Diagnosis**: RAM is volatile (loses data on power off).  
**Fix**: Implement persistence by saving profiles to disk/database. This converts in-memory data to permanent storage.

## Verification Task 2 — Design Decision
Building a recipe app. Use **structured tables** (ingredients: [name, quantity, unit]) or **free-text notes**? Defend using this topic.

## Solution 2
**Choose structured tables**. Why:  
- Enables precise queries (e.g., "find recipes with < 10g salt").  
- Free-text fails at calculations/filtering (e.g., parsing "a pinch of salt" as a measurable unit).  
- Structured data is the foundation for reliable applications.

## Verification Task 3 — Code Review
```text
# STEP 1: Read user input as raw text
# STEP 2: Save directly to file without validation
# STEP 3: Later, split text by commas to extract data
# → Fails if input contains commas (e.g., "Doe, John")
```
Find and fix the bug.

## Solution 3
**Bug**: No schema enforcement.  
**Fix**: Define structured fields (e.g., `[firstName, lastName, age]`) and reject invalid inputs. Never assume raw text aligns with expectations.

## What Comes Next
The next topic is **How Computers Store Data**. This follows logically because understanding data’s binary nature (0s/1s) and persistence is useless without knowing *how* hardware physically stores these bits. You’ll see how disks, memory, and filesystems turn abstract data into tangible reality.

## Reference Summary
Data is raw, context-free facts (e.g., `42`) that become information when meaningful (e.g., "user age"). Computers persist data beyond runtime using structured (tables), semi-structured (JSON), or unstructured (media) formats, all stored as binary 0s/1s. Storage matters because every application—from banks to games—relies on data as its foundation. The most common mistake is ignoring structure, leading to unqueryable chaos. For NexaBank, structured data models customers/transactions as tables, enabling precise calculations and reporting. This topic unlocks understanding hardware storage next.