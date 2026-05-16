# Topic: File Systems & How Databases Use Disk  
## What Is This?  
A **file system** is how computers organize and store data on disks. It arranges data into **files** (individual data units) and **directories** (folders that group files). Databases use file systems to store their data persistently, meaning the data remains even after the computer restarts.  

Databases map their data (like tables, indexes, and settings) to files on disk. For example, a database named `library` might create a folder containing multiple files for its data.  

---

## How It Works Internally  
When a database is created, it interacts with the operating system to:  
1. Reserve space on the disk.  
2. Create files to store raw data (e.g., `library_data.ibd` for MySQL or `library.db` for SQLite).  
3. Use the file system’s structure to manage relationships between files (e.g., directories for different databases).  

The database software handles reading/writing to these files transparently, ensuring data is stored efficiently and retrieved quickly.  

---

## Syntax and Structure  
```sql
-- Create a database named "library"
CREATE DATABASE library;
```  
This command tells the database system to:  
1. Allocate space on the disk.  
2. Create a directory (e.g., `/var/lib/mysql/library/` in MySQL).  
3. Generate files like `library.ibd` (InnoDB storage engine) to store data.  

---

## Practical Example  
After running `CREATE DATABASE library;`, check your file system:  
- **MySQL**: Look in `/var/lib/mysql/` (Linux) or `C:\ProgramData\MySQL\` (Windows).  
- **PostgreSQL**: Look in `/var/lib/postgresql/` (Linux) or `C:\Program Files\PostgreSQL\` (Windows).  

You’ll find a folder named `library` containing files the database uses to store data.  

---

## Common Mistakes Beginners Make  
1. **Editing database files manually**  
   ❌ *Example*: Trying to open `library.ibd` in a text editor.  
   *Why it’s wrong*: Database files are binary and not human-readable. Manual edits corrupt data.  

2. **Ignoring disk space limits**  
   ❌ *Example*: Not monitoring disk usage while inserting large files into a database.  
   *Why it’s wrong*: Databases require free disk space to write new data.  

3. **Mixing file systems and databases naively**  
   ❌ *Example*: Storing images directly in a database without understanding storage limits.  
   *Why it’s wrong*: Databases are optimized for structured data, not large binary files.  

---

## Programming Challenge  
Create a database named `digital_library` and verify its corresponding file/directory exists on the disk.  

---

## Solution  
1. Run the SQL command:  
   ```sql  
   CREATE DATABASE digital_library;  
   ```  
2. Check the file system for the database’s folder (location depends on your DBMS). For example:  
   - **MySQL**: `C:\ProgramData\MySQL\MySQL Server 8.0\Data\digital_library\`  
   - **PostgreSQL**: `/var/lib/postgresql/14/main/base/` (use `pg_ls_dir` to list databases).  

---

## What Comes Next  
After understanding how databases interact with disk storage, the next topic is **Tables and Structured Data**, where we’ll explore how databases organize data into rows and columns.