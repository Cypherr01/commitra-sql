## What Is This?
Distributed transactions refer to a sequence of operations that span multiple databases or services, ensuring that either all or none of the operations are executed to maintain data consistency. Think of it like a bank transfer between two accounts in different banks: the money is deducted from one account and added to the other, but if either step fails, the entire transaction is cancelled to avoid inconsistent balances.

## How It Works Internally
### Distributed Transaction — Transaction Spanning Multiple Databases or Services
A distributed transaction is a complex process that involves multiple parties, each responsible for a portion of the transaction. It's like a supply chain where each supplier must deliver their part for the final product to be complete. If any supplier fails, the entire chain is broken.

### Two-Phase Commit (2PC) — Coordinator Prepares All Participants → All Commit or All Rollback
The Two-Phase Commit protocol is a method used to ensure that all parties in a distributed transaction agree on the outcome. It's like a group decision-making process where everyone must agree before the decision is finalized. If anyone disagrees, the decision is rolled back.

### Saga Pattern — Sequence of Local Transactions with Compensating Transactions for Failures
The Saga pattern is a design approach that breaks down a distributed transaction into smaller, local transactions. Each local transaction has a corresponding compensating transaction that reverses its effects if something goes wrong. It's like a series of smaller decisions, each with a backup plan in case something fails.

### Eventual Consistency — Accept Temporary Inconsistency; Reconcile Later
Eventual consistency is a strategy that allows for temporary inconsistencies in the data, as long as they are eventually reconciled. It's like a temporary detour on a road trip: you might take a longer route, but you'll eventually reach your destination.

### Change Data Capture (CDC) — Stream Database Changes via Debezium/binlog
Change Data Capture is a technique that captures changes made to a database and streams them to other systems. It's like a news feed that broadcasts updates to all interested parties.

## Syntax and Structure
```sql
-- Start a distributed transaction
BEGIN;

-- Perform operations on multiple databases or services
INSERT INTO database1.table1 (column1) VALUES ('value1');
INSERT INTO database2.table2 (column2) VALUES ('value2');

-- Commit the transaction if all operations are successful
COMMIT;

-- Roll back the transaction if any operation fails
ROLLBACK;
```

## Practical Example
To demonstrate a distributed transaction, let's consider a banking system where we need to transfer money from one account to another. We'll use a simplified example with two databases: `database1` for the sender's account and `database2` for the recipient's account.
```sql
-- Create tables in both databases
CREATE TABLE database1.accounts (id INT, balance DECIMAL(10, 2));
CREATE TABLE database2.accounts (id INT, balance DECIMAL(10, 2));

-- Insert initial balances
INSERT INTO database1.accounts (id, balance) VALUES (1, 100.00);
INSERT INTO database2.accounts (id, balance) VALUES (2, 50.00);

-- Start a distributed transaction
BEGIN;

-- Debit the sender's account
UPDATE database1.accounts SET balance = balance - 20.00 WHERE id = 1;

-- Credit the recipient's account
UPDATE database2.accounts SET balance = balance + 20.00 WHERE id = 2;

-- Commit the transaction
COMMIT;
```

## How This Connects to the Project
**BEFORE:** Without distributed transactions, our banking system would be prone to inconsistencies and errors when transferring money between accounts.
**AFTER:** With distributed transactions, our system ensures that either both accounts are updated correctly or neither is, maintaining data consistency.
The `transfer_money` function in the `banking_system` module uses distributed transactions to update account balances.
A real company that uses distributed transactions is PayPal, which needs to ensure that transactions between different accounts and systems are executed reliably and consistently.

## Common Mistakes Beginners Make
**Most common mistake:** Forgetting to commit or roll back a distributed transaction, leading to inconsistent data.
**Looks right but is silently wrong:** Using a local transaction instead of a distributed transaction, which can cause data inconsistencies.
**Seems optional but critical at scale:** Not using Change Data Capture to stream database changes, which can lead to data inconsistencies and errors.
**Missed config or flag:** Forgetting to set the `distributed_transaction` flag when starting a transaction, which can cause the transaction to fail.
**Interview question:** How would you handle a distributed transaction that fails due to a network error?

## Verification Task 1
Debug This: "Your system shows inconsistent account balances after a transfer. You have the transfer code and the database logs. Diagnose and fix the issue."

## Solution 1
The issue is likely due to a missing commit or rollback statement in the transfer code. To fix this, we need to review the code and ensure that the transaction is properly committed or rolled back.

## Verification Task 2
Design Decision: "Building a distributed transaction system. Use the Two-Phase Commit protocol or the Saga pattern? Defend your choice."

## Solution 2
We should use the Saga pattern because it provides a more flexible and resilient approach to distributed transactions. The Saga pattern allows for compensating transactions to be executed in case of failures, which ensures that the system remains in a consistent state.

## Verification Task 3
Code Review: The following code snippet is used to transfer money between accounts:
```sql
BEGIN;
UPDATE database1.accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE database2.accounts SET balance = balance + 20.00 WHERE id = 2;
-- missing commit or rollback statement
```
Find and fix the bug.

## Solution 3
The bug is the missing commit or rollback statement. To fix this, we need to add a commit or rollback statement after the updates:
```sql
BEGIN;
UPDATE database1.accounts SET balance = balance - 20.00 WHERE id = 1;
UPDATE database2.accounts SET balance = balance + 20.00 WHERE id = 2;
COMMIT;
```

## What Comes Next
The next topic is "Stored Functions — MySQL", which builds on the concepts learned in this topic. We will learn how to create stored functions in MySQL, which can be used to encapsulate complex logic and improve the performance of our database queries.

## Reference Summary
Distributed transactions refer to a sequence of operations that span multiple databases or services, ensuring that either all or none of the operations are executed to maintain data consistency. The Two-Phase Commit protocol and the Saga pattern are two approaches to implementing distributed transactions. Change Data Capture is a technique used to stream database changes to other systems. Distributed transactions are critical in ensuring data consistency and reliability in distributed systems. A common mistake beginners make is forgetting to commit or roll back a distributed transaction, leading to inconsistent data. The concept of distributed transactions is essential in building reliable and scalable systems, and it connects to the project by ensuring that account balances are updated consistently.