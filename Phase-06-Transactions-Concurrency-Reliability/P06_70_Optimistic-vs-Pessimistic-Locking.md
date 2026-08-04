## What Is This?
Optimistic vs pessimistic locking refers to two different strategies used to manage concurrent access to shared resources in a database, ensuring data consistency and preventing conflicts. A real-world analogy for this concept is a library where multiple people want to borrow the same book. In a pessimistic approach, the library locks the book as soon as someone expresses interest in borrowing it, preventing others from accessing it until the first person returns the book. In contrast, an optimistic approach allows multiple people to borrow the book simultaneously, checking for conflicts only when someone tries to return the book, and resolving any issues that arise at that point.

## How It Works Internally
### Assume Conflicts Will Happen; Lock Data Before Reading It
In pessimistic locking, the system assumes that conflicts will happen and locks the data before reading it to prevent other transactions from accessing the same data. This approach ensures that only one transaction can modify the data at a time, preventing conflicts and inconsistencies.

### Select ... For Update — Lock Row for Update
The `SELECT ... FOR UPDATE` statement is used to lock a row for update, preventing other transactions from accessing the same row until the lock is released. This statement is typically used in high-contention environments where multiple transactions are competing for the same resources.

### Good for: High-Contention Resources, Short Operations
Pessimistic locking is well-suited for high-contention resources and short operations, where the lock is held for a short duration. This approach ensures that the transaction can complete quickly and efficiently, without conflicts or inconsistencies.

### Bad for: Long-Running Operations (Holds Locks a Long Time)
However, pessimistic locking can be problematic for long-running operations, as it holds locks for an extended period, preventing other transactions from accessing the same resources. This can lead to decreased concurrency and increased contention, resulting in performance issues.

### Assume Conflicts Are Rare; Don't Lock; Check for Conflicts at Update Time
In optimistic locking, the system assumes that conflicts are rare and doesn't lock the data before reading it. Instead, it checks for conflicts at update time, and resolves any issues that arise.

### Version Column: `version INTEGER DEFAULT 0` or `updated_at TIMESTAMP`
A version column, such as `version INTEGER DEFAULT 0` or `updated_at TIMESTAMP`, is used to track changes to the data. When a transaction updates the data, it checks the version column to ensure that the data hasn't been modified by another transaction.

### Read Row + Version → Update Row → Check Version Hasn't Changed → Commit or Retry
The optimistic locking process involves reading the row and version, updating the row, checking that the version hasn't changed, and committing or retrying the transaction if a conflict is detected.

### Update Table Set Col=Val, Version=Version+1 Where Id=? and Version=?
The `UPDATE` statement is used to update the row, incrementing the version column and checking that the version hasn't changed. If the version has changed, the update fails, and the transaction is retried or rolled back.

### If `rows_affected = 0` — Conflict; Retry or Report Error
If the `UPDATE` statement affects zero rows, it indicates a conflict, and the transaction is retried or an error is reported.

### Good for: Low-Contention, Long Operations, Distributed Systems
Optimistic locking is well-suited for low-contention environments, long operations, and distributed systems, where conflicts are rare and the overhead of locking is high.

### ETag-Based Optimistic Locking in REST APIs
ETag-based optimistic locking is a technique used in REST APIs to implement optimistic locking. An ETag (Entity Tag) is a unique identifier assigned to a resource, which is used to track changes to the resource. When a client updates a resource, it includes the ETag in the request, and the server checks that the ETag matches the current ETag of the resource. If the ETags don't match, it indicates a conflict, and the update fails.

### CORE INSIGHT
The core insight of optimistic vs pessimistic locking is that the choice of locking strategy depends on the specific use case and requirements of the system. Pessimistic locking is suitable for high-contention environments and short operations, while optimistic locking is suitable for low-contention environments and long operations.

## Syntax and Structure
```sql
-- Pessimistic locking example
BEGIN TRANSACTION;
SELECT * FROM table_name FOR UPDATE;
UPDATE table_name SET column_name = 'new_value' WHERE id = 1;
COMMIT;

-- Optimistic locking example
BEGIN TRANSACTION;
SELECT * FROM table_name;
UPDATE table_name SET column_name = 'new_value', version = version + 1 WHERE id = 1 AND version = 1;
COMMIT;
```
In the above example, the pessimistic locking approach uses the `SELECT ... FOR UPDATE` statement to lock the row, while the optimistic locking approach uses a version column to track changes to the data.

## Practical Example
To demonstrate the concept of optimistic vs pessimistic locking, consider a banking system where multiple transactions are competing for the same account. In a pessimistic locking approach, the system would lock the account as soon as a transaction is initiated, preventing other transactions from accessing the same account until the lock is released. In an optimistic locking approach, the system would check for conflicts at update time, and resolve any issues that arise.

## How This Connects to the Project
Before implementing optimistic vs pessimistic locking, the banking system simulator would be prone to conflicts and inconsistencies, resulting in incorrect account balances and potentially causing financial losses. After implementing optimistic vs pessimistic locking, the system would ensure that transactions are processed correctly and consistently, preventing conflicts and inconsistencies. The exact file and function name where this concept lives in the project is `transaction_manager.py`, and the function name is `process_transaction`. A real company that uses this exact pattern is PayPal, which uses optimistic locking to manage concurrent access to user accounts.

## Common Mistakes Beginners Make
**Most common mistake**: Not considering the trade-offs between pessimistic and optimistic locking, and choosing the wrong approach for the specific use case.
Wrong idea: Using pessimistic locking for all transactions, regardless of the use case.
Correct idea: Choosing the locking strategy based on the specific requirements of the system.
**Looks right but is silently wrong**: Using optimistic locking without properly handling conflicts, resulting in inconsistent data.
**Seems optional but critical at scale**: Not implementing locking mechanisms at all, resulting in conflicts and inconsistencies as the system scales.
**Missed config or flag**: Not configuring the locking mechanism properly, resulting in incorrect behavior.
**Interview question this topic generates**: How would you implement optimistic locking in a distributed system, and what are the trade-offs between pessimistic and optimistic locking?

## Verification Task 1
Debug the following symptom: "The banking system simulator is producing incorrect account balances." Given the evidence that multiple transactions are competing for the same account, diagnose and fix the issue.
## Solution 1
The issue is likely due to the lack of locking mechanisms, resulting in conflicts and inconsistencies. To fix the issue, implement optimistic locking using a version column to track changes to the account data.

## Verification Task 2
Design a decision: "Should we use pessimistic or optimistic locking for the banking system simulator?" Defend your answer using the concepts learned in this topic.
## Solution 2
We should use optimistic locking for the banking system simulator, as it is well-suited for low-contention environments and long operations. Pessimistic locking would be more suitable for high-contention environments and short operations.

## Verification Task 3
Code review: The following code snippet is used to update an account balance:
```sql
UPDATE accounts SET balance = balance + 100 WHERE id = 1;
```
Find and fix the bug that causes the code to fail under a specific condition.
## Solution 3
The bug is that the code does not handle conflicts properly, resulting in inconsistent data. To fix the bug, add a version column to track changes to the account data, and use optimistic locking to check for conflicts at update time.

## What Comes Next
The next topic is **Stored Procedures — MySQL**, which follows logically from this topic because stored procedures are used to encapsulate complex database operations, including locking mechanisms. Understanding optimistic vs pessimistic locking is a prerequisite for designing and implementing stored procedures that manage concurrent access to shared resources.

## Reference Summary
Optimistic vs pessimistic locking refers to two different strategies used to manage concurrent access to shared resources in a database. Pessimistic locking assumes conflicts will happen and locks the data before reading it, while optimistic locking assumes conflicts are rare and checks for conflicts at update time. The choice of locking strategy depends on the specific use case and requirements of the system. Pessimistic locking is suitable for high-contention environments and short operations, while optimistic locking is suitable for low-contention environments and long operations. A common production mistake is not considering the trade-offs between pessimistic and optimistic locking, and choosing the wrong approach for the specific use case. This concept is critical for designing and implementing database systems that ensure data consistency and prevent conflicts.