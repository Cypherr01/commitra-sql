## What Is This?
A trigger is a procedure that automatically fires on DML events, such as when a new record is inserted, updated, or deleted from a database table. Think of it like a security guard at a museum who is instructed to take a photo of anyone who enters or leaves a specific room, so they can keep a record of all visitors. In this case, the security guard is like a trigger, and the room is like a database table.

## How It Works Internally
### Trigger Definition
A trigger is defined using the `CREATE TRIGGER` statement, which specifies the trigger name, the timing of the trigger (before or after the event), the event that activates the trigger (insert, update, or delete), and the table that the trigger is associated with.

### Trigger Timing
The timing of a trigger can be either `BEFORE` or `AFTER` the event. For example, a `BEFORE INSERT` trigger would fire before a new record is inserted into the table, while an `AFTER INSERT` trigger would fire after the record has been inserted.

### Trigger Event
A trigger can be activated by one of three events: `INSERT`, `UPDATE`, or `DELETE`. For example, a trigger can be defined to fire whenever a new record is inserted into a table, or whenever an existing record is updated or deleted.

### NEW and OLD Values
In a trigger, you can access the new values of a record being inserted or updated using the `NEW` table, and the old values of a record being updated or deleted using the `OLD` table. For example, in an `AFTER UPDATE` trigger, you can access the new values of the updated record using `NEW.column_name`, and the old values using `OLD.column_name`.

### Modifying NEW Values
In a `BEFORE INSERT` or `BEFORE UPDATE` trigger, you can modify the `NEW` values to change the data that is being inserted or updated. For example, you can use a `BEFORE INSERT` trigger to automatically set the `created_at` timestamp for a new record.

### Signaling an Error
In a `BEFORE` trigger, you can use the `SIGNAL` statement to abort the operation and raise an error if certain conditions are not met. For example, you can use a `BEFORE INSERT` trigger to check if a record already exists in the table, and if so, raise an error to prevent the duplicate record from being inserted.

### Transactions
Triggers cannot use transactions (COMMIT/ROLLBACK) inside MySQL triggers. This means that if a trigger encounters an error, it will not be able to roll back the changes made by the trigger.

### Calling Procedures
Triggers cannot use the `CALL` procedure with OUT parameters in triggers. This means that if you need to call a procedure from a trigger, it must not return any values.

### Trigger Order
`BEFORE` triggers run in the order they were created. This means that if you have multiple `BEFORE` triggers defined for the same table and event, they will be executed in the order they were created.

### Managing Triggers
You can use the `SHOW TRIGGERS` statement to view the triggers defined for a table, and the `DROP TRIGGER` statement to delete a trigger. You can also use the `SHOW CREATE TRIGGER` statement to view the definition of a trigger.

### Common Uses
Triggers are commonly used for audit logging, denormalization, complex validation, and cascade updates. For example, you can use a trigger to log all changes made to a table, or to automatically update related tables when a record is inserted, updated, or deleted.

### Performance Impact
Triggers can have a performance impact, as every DML operation incurs trigger overhead. This means that you should carefully consider the use of triggers and profile your application to ensure that the triggers are not causing performance issues.

### LAYER 1: Minimum Viable Version
A simple trigger can be defined to log all changes made to a table. For example:
```sql
CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (table_name, action, changed_data)
    VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
END;
```
### LAYER 2: Why the Simple Version Breaks
The simple version breaks if we need to log changes made to multiple tables, or if we need to log changes made to specific columns only.

### LAYER 3: Production Version
A production version of the trigger would need to handle multiple tables and columns, and would need to be optimized for performance. For example:
```sql
CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    IF NEW.customer_id IS NOT NULL THEN
        INSERT INTO audit_log (table_name, action, changed_data)
        VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
    END IF;
END;
```
### LAYER 4: Edge Cases
One edge case is if the trigger is defined for a table that has a large number of rows, and the trigger is logging changes to a separate table. In this case, the trigger could cause performance issues if it is logging too many changes.

Another edge case is if the trigger is defined for a table that has a complex schema, with multiple relationships to other tables. In this case, the trigger would need to be carefully designed to handle the complex relationships.

CORE INSIGHT: Triggers are powerful tools for automating tasks and enforcing data integrity, but they can have a performance impact and require careful design and testing.

## Syntax and Structure
```sql
CREATE TRIGGER trigger_name
BEFORE/AFTER INSERT/UPDATE/DELETE ON table
FOR EACH ROW
BEGIN
    -- trigger code
END;
```
This is the basic syntax for creating a trigger in MySQL. The `CREATE TRIGGER` statement is used to define a new trigger, and the `BEFORE` or `AFTER` keyword specifies the timing of the trigger. The `INSERT`, `UPDATE`, or `DELETE` keyword specifies the event that activates the trigger, and the `ON table` clause specifies the table that the trigger is associated with. The `FOR EACH ROW` clause specifies that the trigger should be executed for each row affected by the event.

## Practical Example
```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    customer VARCHAR(255),
    total DECIMAL(10, 2)
);

CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (table_name, action, changed_data)
    VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
END;

INSERT INTO orders (id, customer, total) VALUES (1, 'John Doe', 100.00);
```
This example creates a table called `orders` and a trigger called `log_changes` that logs all inserts made to the `orders` table.

## How This Connects to the Project
ELEMENT 1: BEFORE - Without triggers, our database automation toolkit would not be able to automatically log changes made to the database.
ELEMENT 2: AFTER - With triggers, our database automation toolkit can automatically log changes made to the database, and can also enforce data integrity and automate tasks.
ELEMENT 3: The trigger is defined in the `database.sql` file, in the `create_triggers` function.
ELEMENT 4: A real company that uses triggers is Amazon, which uses triggers to enforce data integrity and automate tasks in its databases.

## Common Mistakes Beginners Make
**Most common mistake**: Not understanding the timing of triggers, and defining a trigger that fires at the wrong time.
Wrong idea: Defining a `BEFORE INSERT` trigger to log changes made to a table.
Correct idea: Defining an `AFTER INSERT` trigger to log changes made to a table.
**Looks right but is silently wrong**: Defining a trigger that logs changes made to a table, but not checking for errors.
```sql
CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (table_name, action, changed_data)
    VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
END;
```
This trigger looks right, but it does not check for errors. If an error occurs while logging the change, the trigger will fail silently.
**Seems optional but critical at scale**: Not optimizing triggers for performance.
If a trigger is not optimized for performance, it can cause performance issues when the database is under heavy load.
**Missed config or flag**: Not specifying the `FOR EACH ROW` clause when defining a trigger.
If the `FOR EACH ROW` clause is not specified, the trigger will only fire once for each event, rather than for each row affected by the event.
**Interview question**: What is the difference between a `BEFORE` trigger and an `AFTER` trigger?
Surface answer: A `BEFORE` trigger fires before the event, while an `AFTER` trigger fires after the event.
Production answer: A `BEFORE` trigger fires before the event, and can be used to validate data and enforce data integrity. An `AFTER` trigger fires after the event, and can be used to log changes made to the database and automate tasks.

## Verification Task 1
Your system shows an error message when trying to insert a new record into the `orders` table. You have the following evidence:
* The error message says "Cannot insert duplicate key".
* The `orders` table has a primary key constraint on the `id` column.
Diagnose and fix the issue.
## Solution 1
The issue is that the `id` column is being duplicated. To fix the issue, we need to modify the trigger to check for duplicate keys before inserting the new record.
```sql
CREATE TRIGGER prevent_duplicates
BEFORE INSERT ON orders
FOR EACH ROW
BEGIN
    IF EXISTS (SELECT 1 FROM orders WHERE id = NEW.id) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cannot insert duplicate key';
    END IF;
END;
```
## Verification Task 2
You are building a database for an e-commerce application, and you need to decide whether to use a `BEFORE` trigger or an `AFTER` trigger to log changes made to the `orders` table. Defend your decision using the concepts learned in this topic.
## Solution 2
I would use an `AFTER` trigger to log changes made to the `orders` table. This is because an `AFTER` trigger fires after the event, and can be used to log changes made to the database. A `BEFORE` trigger fires before the event, and is typically used to validate data and enforce data integrity. In this case, we want to log changes made to the `orders` table, so an `AFTER` trigger is the better choice.

## Verification Task 3
You have the following code snippet:
```sql
CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (table_name, action, changed_data)
    VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
END;
```
Find and fix the bug in the code snippet.
## Solution 3
The bug in the code snippet is that it does not check for errors when logging the change. To fix the bug, we need to add error handling to the trigger.
```sql
CREATE TRIGGER log_changes
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        -- handle error
    END;
    INSERT INTO audit_log (table_name, action, changed_data)
    VALUES ('orders', 'INSERT', CONCAT('ID: ', NEW.id, ', Customer: ', NEW.customer));
END;
```
## What Comes Next
The next topic is Scheduled Events — MySQL. This topic is a logical follow-on from Triggers — MySQL because scheduled events can be used to automate tasks and enforce data integrity, just like triggers. One concrete concept from this topic that will reappear in Scheduled Events — MySQL is the use of the `CREATE EVENT` statement to define a new event. This concept will be used to schedule events to occur at specific times or intervals.

## Reference Summary
A trigger is a procedure that automatically fires on DML events, such as when a new record is inserted, updated, or deleted from a database table. Triggers can be used to enforce data integrity, automate tasks, and log changes made to the database. The `CREATE TRIGGER` statement is used to define a new trigger, and the `BEFORE` or `AFTER` keyword specifies the timing of the trigger. Triggers can have a performance impact, and should be carefully designed and tested. The `NEW` and `OLD` tables can be used to access the new and old values of a record being inserted, updated, or deleted. Triggers can be used to log changes made to a table, and can also be used to enforce data integrity and automate tasks. The most common mistake made by beginners is not understanding the timing of triggers, and defining a trigger that fires at the wrong time. This matters to you because if you don't understand how triggers work, you may define a trigger that causes performance issues or data integrity problems in your database.