## What Is This?
Data storage is how computers **persistently remember information** — keeping data intact even when powered off. Imagine a library:  
- **Books** (data) live on **shelves** (storage devices like disks).  
- A **catalog system** (file system) helps find books by title/author.  
- **Librarians** (storage controllers) fetch books when requested.  
Without this system, books would scatter, and knowledge would vanish when the library closes. Computers use similar principles to retain your bank transactions, photos, and code.

## How It Works Internally
### Layer 1 — Minimum Viable Version
Two core components:  
1. **RAM (Random Access Memory)**:  
   - Temporary, lightning-fast workspace.  
   - Like your desk: holds tools/papers you’re actively using.  
   - *Volatile*: Loses everything when power cuts.  

2. **Disk (HDD/SSD)**:  
   - Permanent storage; slower than RAM.  
   - Like a filing cabinet: holds documents long-term.  
   - *Non-volatile*: Data survives shutdowns.  

### Layer 2 — Why the Simple Version Breaks
Relying solely on RAM or disk causes failures:  
- **RAM alone**: A power outage wipes all unsaved work (e.g., losing an hour-long unsaved essay).  
- **Disk alone**: Constantly reading/writing to disk would be glacially slow (like mailing every pencil stroke to a remote office).  

### Layer 3 — The Production Version
Real systems add these optimizations:  
3. **Pages (4KB/8KB/16KB blocks)**:  
   - Data moves between RAM/disk in fixed-size "chunks."  
   - *Why?* Disks can’t read single bytes efficiently; pages batch operations.  
   - Like delivering 10 letters in one trip instead of 10 trips for one letter.  

4. **Buffer Pool**:  
   - A RAM cache holding frequently used disk pages.  
   - Avoids redundant disk trips (e.g., reusing a customer’s account data across transactions).  

5. **Sequential vs. Random I/O**:  
   - **Sequential**: Reading/writing contiguous pages (e.g., a book chapter). *Faster* because disk heads move linearly.  
   - **Random**: Jumping between scattered pages (e.g., 10 random book pages). *Slower* due to mechanical seeking.  

6. **Write-Ahead Log (WAL)**:  
   - A durability safeguard: Changes are written to a log *before* data files.  
   - Ensures crash recovery (e.g., replaying logged transactions after a power failure).  

7. **Crash Recovery**:  
   - On startup, databases replay WAL entries to restore consistency.  
   - Undoes incomplete transactions (e.g., a half-written transfer in NexaBank).  

### Layer 4 — Edge Cases and Failure Modes
1. **Power failure during a write**:  
   - *Symptom*: Corrupted data file.  
   - *Fix*: Replay WAL to restore the last consistent state.  
   - *Detection*: Checksum mismatches in data pages.  

2. **Buffer pool starvation**:  
   - *Symptom*: Queries slow to a crawl as RAM runs out.  
   - *Fix*: Evict old pages or increase buffer pool size.  
   - *Detection*: High "buffer pool wait" metrics.  

**CORE INSIGHT**: Data must be written **safely** (WAL) and accessed **efficiently** (pages/buffer pool) to balance speed and reliability.

## Syntax and Structure
```text
# STEP 1: CPU requests to store data (e.g., "customer_id=12345")
# STEP 2: RAM checks buffer pool for free space; finds a page slot
# STEP 3: Data is written to RAM page (temporary storage)
# STEP 4: WAL logs the change to disk (ensures durability)
# STEP 5: Buffer pool schedules page write to disk (e.g., every 1 second)
# STEP 6: Disk controller writes full page (4KB) sequentially
# STEP 7: On crash, recovery process replays WAL to fix incomplete writes
# STEP 8: Buffer pool reloads critical pages from disk at startup
# In Phase 1 we will write this in real code.
```

## Common Mistakes Beginners Make
- **Ignoring volatility**: Assuming RAM persists data → loses all work on shutdown.  
- **Wrong idea**: Writing every byte to disk immediately.  

```text
# Pseudocode example (inefficient):
# WRITE byte TO disk  # Slow! Causes 10,000 disk trips for 10,000 bytes
```

- **Correct idea**: Batch writes into 4KB pages.  
- **Underestimating random I/O**: Designing systems that jump between pages → disk thrashing.  
- **Skipping WAL**: Omitting write-ahead logging → data corruption after crashes.  
- **Interview question**: "Why not store all data in RAM?"  
  *Surface answer*: RAM is faster.  
  *Production answer*: Volatility risk + cost; disk provides durable, affordable scaling.
## Verification Task 1 — Debug This  
**Symptom**: After a server crash, recent transactions vanished.  
**Evidence**: WAL log exists but wasn’t replayed during recovery. Diagnose and fix.

## Solution 1  
**Diagnosis**: The database wasn’t configured to enable WAL.  
**Fix**:  
1. Set `wal_enabled = on` in configuration.  
2. Ensure WAL directory has write permissions.  
3. Restart the database to initialize logging.  
*Why it matters*: NexaBank transactions would disappear after crashes without WAL.

## Verification Task 2 — Design Decision  
**Building**: A logging system.  
**Use**: Single-byte writes (Option A) or 4KB pages (Option B)? Defend your choice.

## Solution 2  
**Choose B (4KB pages)**.  
- **Efficiency**: Writing 4KB in one operation is 4,000× faster than 1,000 single-byte writes.  
- **Atomicity**: Page writes complete fully or not at all, preventing partial logs.  
- **Recovery**: Pages simplify crash recovery by replaying whole blocks.  

## Verification Task 3 — Code Review  
```text
# Pseudocode snippet (conceptual bug):
# STEP 1: UPDATE account_balance IN RAM
# STEP 2: WRITE change DIRECTLY to disk  # Skips WAL!
# STEP 3: COMMIT transaction
```  
Find and fix the bug that risks data loss.

## Solution 3  
**Bug**: The update writes directly to disk *without* logging to WAL first.  
**Fix**: Insert WAL logging between Steps 1 and 2:  
```text
# STEP 1: UPDATE account_balance IN RAM
# STEP 1.5: WRITE change TO WAL  # Critical for durability
# STEP 2: WRITE change TO disk
```  
*Consequence*: A crash after Step 2 but before commit would corrupt the balance.

## What Comes Next  
The next topic is **File Systems & How Databases Use Disk**. This follows logically because we’ve learned how data moves between RAM and disk in pages. Now we’ll explore how disks organize these pages into files and directories — the foundation for database storage engines. The concept of **pages** from this topic will directly explain why databases structure data files in fixed-size chunks.

## Reference Summary  
Data storage balances speed (RAM) and durability (disk) through pages, buffer pools, and WAL. Computers use 4KB/8KB/16KB pages for efficient I/O, with sequential access outperforming random jumps. The buffer pool caches hot data in RAM, while WAL guarantees crash recovery by logging changes first. For NexaBank, this ensures transactions survive outages and account balances remain consistent. The most common mistake is neglecting WAL, risking silent corruption. This foundation enables understanding how databases physically organize data on disk in the next topic.