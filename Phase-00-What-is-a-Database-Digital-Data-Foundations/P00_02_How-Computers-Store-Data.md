# Topic: How Computers Store Data

## What Is This?
Computers store data in a hierarchical manner, using a combination of temporary and permanent storage. 
Imagine a library where books are stored on shelves (permanent storage) and a librarian's desk (temporary storage) where books are temporarily placed while being checked out or processed.

## How It Works Internally
Here's a step-by-step explanation of how computers store data internally:

1. **RAM (Temporary Fast Memory)**: RAM (Random Access Memory) is a type of computer storage that temporarily holds data and applications while the computer is running. It's like a librarian's desk where books are temporarily placed.
2. **Disk (Persistent Storage)**: Disks, such as Hard Disk Drives (HDD) or Solid-State Drives (SSD), provide permanent storage for data. This is like the library's bookshelves where books are stored long-term.
3. **Pages**: Computers store data in fixed-size blocks called pages, typically 4KB, 8KB, or 16KB. Think of pages like individual bookshelves that can hold a specific number of books.
4. **Why Databases Read/Write in Pages**: Databases read and write data in pages because it allows for more efficient storage and retrieval. Imagine checking out multiple books from the same bookshelf at once.
5. **Sequential vs Random I/O**: Sequential I/O (Input/Output) accesses data in a continuous sequence, like reading a book from start to finish. Random I/O accesses data in a non-sequential manner, like looking up a specific page in a book. Sequential I/O is generally faster.
6. **Buffer Pool**: A buffer pool is a cache of disk pages stored in RAM, which improves database performance by reducing the need for disk accesses. Think of it like a librarian's cart that holds frequently used books.
7. **WAL (Write-Ahead Log)**: The Write-Ahead Log is a durability mechanism that writes changes to a log before writing them to the main data files. This ensures that data can be recovered in case of a crash or power failure.
8. **Crash Recovery**: Crash recovery refers to the process of restoring a database to a consistent state after a crash or power failure. This is achieved through the WAL and buffer pool.

## Syntax and Structure
```text
# STEP 1: CPU receives instruction to store data
# STEP 2: RAM allocates space for the data
# STEP 3: Data is written to RAM (temporary storage)
# STEP 4: Data is written to disk (permanent storage) in pages
# STEP 5: Buffer pool caches frequently accessed disk pages in RAM
# STEP 6: WAL logs changes before writing to data files
# STEP 7: Crash recovery uses WAL and buffer pool to restore consistency
In Phase 1 we will write this in real code.
```

## Practical Example
Consider a digital library that stores book metadata and images. When a user searches for a book, the database retrieves the relevant metadata from the disk (permanent storage) and stores it in RAM (temporary storage) for faster access. The buffer pool ensures that frequently accessed book metadata remains in RAM.

## Common Mistakes Beginners Make
1. **Mistake: Confusing RAM and Disk Storage**
   Wrong idea: RAM and disk storage are the same thing.
   Correct idea: RAM is temporary fast memory, while disk storage is permanent.

2. **Mistake: Not Understanding Pages**
   Wrong idea: Computers store data in individual bytes.
   Correct idea: Computers store data in fixed-size blocks called pages.

3. **Mistake: Ignoring the Importance of Buffer Pool**
   Wrong idea: The buffer pool is not necessary for database performance.
   Correct idea: The buffer pool significantly improves database performance by reducing disk accesses.

## Programming Challenge
Describe how a computer would store a single book's metadata (title, author, publication date) in RAM and on disk. Explain the steps involved in reading and writing this data.

## Solution
```text
# Step 1: CPU receives instruction to store book metadata
# Step 2: RAM allocates space for the metadata
# Step 3: Metadata is written to RAM (temporary storage)
# Step 4: Metadata is written to disk (permanent storage) in pages
# Step 5: Buffer pool caches frequently accessed metadata in RAM
# Step 6: WAL logs changes before writing to data files
# Step 7: Metadata is retrieved from RAM or disk when needed
```

## What Comes Next
The next topic is **SQL Basics**, which will introduce the fundamental concepts of SQL (Structured Query Language) and how it is used to interact with databases. This topic follows logically from "How Computers Store Data" because SQL is used to manage and manipulate data stored in databases.