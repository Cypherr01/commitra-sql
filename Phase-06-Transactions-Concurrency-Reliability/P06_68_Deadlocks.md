## What Is This?
A deadlock is a situation that occurs when two or more database transactions are blocked, each waiting for the other to release a resource. Think of it like two people, each holding a door handle, waiting for the other to let go so they can pass through - neither can move forward because they are both waiting for the other.

## How It Works Internally
### LAYER 1: Minimum Viable Version
To understand deadlocks, let's consider a simple scenario where two transactions, A and B, are trying to access two resources, X and Y. 
```text
# Transaction A holds lock X and waits for Y
# Transaction B holds lock Y and waits for X
# This creates a circular wait, resulting in a deadlock
```
This is the simplest form of a deadlock, where two transactions are blocked, each waiting for the other to release a resource.

### LAYER 2: Why the Simple Version Breaks
In a real-world database, deadlocks can occur when multiple transactions are accessing multiple resources. For example, in a banking system, two transactions might be trying to transfer funds between two accounts, but each transaction is waiting for the other to release a lock on one of the accounts. 
```text
# Transaction A: transfer funds from account X to account Y
# Transaction B: transfer funds from account Y to account X
# Both transactions are waiting for each other to release a lock
```
This can lead to a deadlock, where both transactions are blocked, and neither can proceed.

### LAYER 3: Production Version
Both MySQL and PostgreSQL detect deadlocks automatically and abort one transaction to resolve the deadlock. 
```text
# MySQL: the victim is the transaction with the fewest rows changed
# PostgreSQL: rolls back one transaction after a 'deadlock_timeout'
```
In MySQL, the transaction with the fewest rows changed is typically chosen as the victim, while in PostgreSQL, the transaction is rolled back after a specified timeout.

### LAYER 4: Edge Cases
Two specific edge cases to consider are:
1. **ERROR 1213 (MySQL)**: a deadlock is detected, and the transaction is rolled back. The application should retry the transaction with exponential backoff.
2. **ERROR 40P01 (PostgreSQL)**: a deadlock is detected, and the transaction is rolled back. The application should retry the transaction with exponential backoff.

CORE INSIGHT: Deadlocks can occur when multiple transactions are accessing multiple resources, and the database must detect and resolve these deadlocks to prevent transactions from being blocked indefinitely.

## Syntax and Structure
```sql
-- Create two tables for demonstration
CREATE TABLE accounts (
  id INT PRIMARY KEY,
  balance DECIMAL(10, 2)
);

CREATE TABLE transfers (
  id INT PRIMARY KEY,
  from_account_id INT,
  to_account_id INT,
  amount DECIMAL(10, 2)
);

-- Insert some sample data
INSERT INTO accounts (id, balance) VALUES (1, 100.00);
INSERT INTO accounts (id, balance) VALUES (2, 50.00);

-- Start a transaction to transfer funds from account 1 to account 2
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE accounts SET balance = balance + 20.00 WHERE id = 2;
COMMIT;

-- Start another transaction to transfer funds from account 2 to account 1
START TRANSACTION;
UPDATE accounts SET balance = balance - 10.00 WHERE id = 2;
UPDATE accounts SET balance = balance + 10.00 WHERE id = 1;
COMMIT;
```
This example demonstrates how deadlocks can occur when multiple transactions are accessing multiple resources.

## Practical Example
To avoid deadlocks, it's essential to ensure that transactions are accessing resources in a consistent order. For example, always access accounts in ascending order by ID.
```sql
-- Start a transaction to transfer funds from account 1 to account 2
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE accounts SET balance = balance + 20.00 WHERE id = 2;
COMMIT;

-- Start another transaction to transfer funds from account 2 to account 1
START TRANSACTION;
UPDATE accounts SET balance = balance - 10.00 WHERE id = (SELECT id FROM accounts WHERE id < 2 ORDER BY id DESC LIMIT 1);
UPDATE accounts SET balance = balance + 10.00 WHERE id = (SELECT id FROM accounts WHERE id > 1 ORDER BY id ASC LIMIT 1);
COMMIT;
```
This example demonstrates how to avoid deadlocks by accessing resources in a consistent order.

## How This Connects to the Project
ELEMENT 1: BEFORE - Without understanding deadlocks, the banking system simulator may experience unexpected errors and crashes when multiple users access the system concurrently.
ELEMENT 2: AFTER - With a solid understanding of deadlocks, the simulator can be designed to handle concurrent access and prevent deadlocks from occurring.
ELEMENT 3: The concept of deadlocks is implemented in the `transfer_funds` function in the `banking_system.py` file.
ELEMENT 4: A real company that uses this pattern is PayPal, which handles millions of concurrent transactions every day and must ensure that its system can prevent and resolve deadlocks efficiently.

## Common Mistakes Beginners Make
**Wrong idea:** Deadlocks only occur in complex systems with many transactions.
**Correct idea:** Deadlocks can occur in any system with multiple transactions accessing multiple resources.
**Most common mistake:** Not considering the order in which resources are accessed, leading to deadlocks.
Looks right but is silently wrong: Using `SELECT FOR UPDATE` without considering the order of resource access.
Seems optional but critical at scale: Implementing retry logic with exponential backoff to handle deadlocks.
Missed config or flag: Not setting the `deadlock_timeout` in PostgreSQL or the `innodb_lock_wait_timeout` in MySQL.
Interview question: How would you design a system to prevent deadlocks in a banking system simulator?

## Verification Task 1
Task 1: Debug This - Your system shows an `ERROR 1213` message when trying to transfer funds between two accounts. You have the following code:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE accounts SET balance = balance + 20.00 WHERE id = 2;
COMMIT;
```
Diagnose and fix the issue.

## Solution 1
The issue is likely due to a deadlock occurring when trying to access the two accounts. To fix this, we need to ensure that the accounts are accessed in a consistent order. We can modify the code to always access accounts in ascending order by ID:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = (SELECT id FROM accounts WHERE id < 2 ORDER BY id DESC LIMIT 1);
UPDATE accounts SET balance = balance + 20.00 WHERE id = (SELECT id FROM accounts WHERE id > 1 ORDER BY id ASC LIMIT 1);
COMMIT;
```

## Verification Task 2
Task 2: Design Decision - You are building a banking system simulator and need to decide how to handle concurrent access to accounts. Should you use pessimistic locking or optimistic locking?

## Solution 2
We should use pessimistic locking to handle concurrent access to accounts. Pessimistic locking ensures that only one transaction can access an account at a time, preventing deadlocks from occurring.

## Verification Task 3
Task 3: Code Review - Find and fix the bug in the following code snippet:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE accounts SET balance = balance + 20.00 WHERE id = 2;
-- missing COMMIT statement
```
The bug is that the `COMMIT` statement is missing, which can cause the transaction to remain open indefinitely.

## Solution 3
To fix the bug, we need to add the `COMMIT` statement at the end of the transaction:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE accounts SET balance = balance + 20.00 WHERE id = 2;
COMMIT;
```

## What Comes Next
The next topic is "Optimistic vs Pessimistic Locking". This topic follows logically from deadlocks because understanding the different locking mechanisms is essential to preventing and resolving deadlocks. The concept of deadlocks is a prerequisite for understanding the trade-offs between optimistic and pessimistic locking. One concrete concept from this topic that will reappear is the importance of considering the order in which resources are accessed to prevent deadlocks.

## Reference Summary
A deadlock is a situation that occurs when two or more database transactions are blocked, each waiting for the other to release a resource. Deadlocks can occur when multiple transactions are accessing multiple resources, and the database must detect and resolve these deadlocks to prevent transactions from being blocked indefinitely. In MySQL, the transaction with the fewest rows changed is typically chosen as the victim, while in PostgreSQL, the transaction is rolled back after a specified timeout. To avoid deadlocks, it's essential to ensure that transactions are accessing resources in a consistent order. The banking system simulator can be designed to handle concurrent access and prevent deadlocks from occurring by implementing retry logic with exponential backoff and using pessimistic locking. Understanding deadlocks is crucial for building a robust and scalable banking system simulator.