# Topic: File Systems & How Databases Use Disk

## What Is This?
A file system is a way that computers organize data on disks into files and directories, making it easier for users and programs to find and manage data. Think of a file system like a filing cabinet, where you can store papers (files) in labeled folders (directories) to keep them organized. This concept is crucial for databases, as they need to efficiently store and retrieve large amounts of data.

## How It Works Internally
Here's a step-by-step explanation of how file systems and databases interact:

1. **File System Basics**: A file system divides the disk into smaller sections called files and directories. Files store data, while directories store lists of files and subdirectories.
2. **Database Storage Needs**: Databases require more than just file system storage. They need to ensure data consistency, handle multiple users accessing data simultaneously (concurrency), and recover from crashes or errors (crash recovery). To achieve this, databases use a layer of abstraction between the file system and their internal storage.
3. **Tablespaces**: A tablespace is a logical grouping of physical storage files. Think of it like a container that holds multiple files. Databases use tablespaces to organize their storage and make it easier to manage.
4. **Data Files, Log Files, Temp Files**: 
   - **Data Files**: Store the actual data in a database. 
   - **Log Files**: Record all changes made to the data, allowing the database to recover in case of a crash.
   - **Temp Files**: Store temporary data used during query execution.

5. **Per-Table Data Files (e.g., .ibd files in MySQL InnoDB)**: Some databases, like MySQL's InnoDB, store data in separate files for each table. This approach allows for more efficient storage and retrieval of data.

6. **Database Directory Structure (e.g., pg_data/ in PostgreSQL)**: PostgreSQL stores its data in a directory called `pg_data/`, which contains multiple subdirectories and files. This structure helps organize the database's files and makes it easier to manage.

## Syntax and Structure
```text
# STEP 1: The computer's operating system provides a file system to organize data on disks.
# STEP 2: The file system divides the disk into files and directories for efficient data storage.
# STEP 3: Databases use a tablespace, a logical grouping of physical storage files, to organize their storage.
# STEP 4: The database stores data in data files, records changes in log files, and uses temp files for temporary data.
# STEP 5: Some databases, like MySQL InnoDB, store data in per-table files (e.g., .ibd files).
# STEP 6: Databases like PostgreSQL use a specific directory structure (e.g., pg_data/) to organize their files.
In Phase 1 we will write this in real code.
```

## Practical Example
Imagine you're building a digital library, and you want to store information about books, authors, and borrowers. A database can help you manage this data efficiently. The database will use a file system to store its data files, log files, and temp files. For example, it might store book information in a data file called `books.ibd` (in MySQL InnoDB) or in a `books` table within the `pg_data/` directory (in PostgreSQL).

## Common Mistakes Beginners Make
1. **Storing data directly in files**: 
   Wrong idea: Databases can simply store data in files like regular file systems.
   Correct idea: Databases use a layer of abstraction (tablespaces, data files) to ensure data consistency, concurrency, and crash recovery.

2. **Ignoring log files**: 
   Wrong idea: Log files are unnecessary and can be ignored.
   Correct idea: Log files are crucial for recovering data in case of a crash or error.

3. **Not understanding tablespaces**: 
   Wrong idea: Tablespaces are just directories or folders.
   Correct idea: Tablespaces are logical groupings of physical storage files that help databases manage their storage.

## Programming Challenge
Describe how a database might use a file system to store its data. Think about the types of files a database might need (data files, log files, temp files) and how they might be organized. Draw a simple diagram showing how these files might be structured on disk.

## Solution
```text
# STEP 1: The database uses a file system to store its data.
# STEP 2: It creates a tablespace to group its physical storage files.
# STEP 3: The database stores data in data files (e.g., books.ibd or books table).
# STEP 4: It records changes in log files for crash recovery.
# STEP 5: The database uses temp files for temporary data during query execution.
# STEP 6: The database organizes its files in a structured directory (e.g., pg_data/ in PostgreSQL).
# STEP 7: This organization allows for efficient data retrieval and management.
```

## What Comes Next
The next topic is **SQL Basics: Data Types and Queries**. This topic follows logically from file systems and disk storage, as it deals with how to interact with the stored data using SQL (Structured Query Language). Understanding how databases store data on disk is essential for learning how to retrieve and manipulate that data using SQL.