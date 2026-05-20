# Topic: What is Data?

## What Is This?
Data are raw facts and figures that have no meaning by themselves.  
Examples:  

- `42` – a number  
- `"Alice"` – a piece of text  
- `2024‑01‑01` – a date  

When we give these facts a context (e.g., “Alice bought 42 books on 2024‑01‑01”), they become **information**.

## How It Works Internally
All data that a computer stores is ultimately represented as a series of **0s and 1s** (binary).  
The computer’s hardware reads and writes these bits, allowing it to keep data even after a program stops running. This persistence is why we need databases, files, and other storage mechanisms.

## Syntax and Structure
At this introductory stage we are only describing concepts, so there is no executable SQL syntax to show.  
Below is a *comment‑only* illustration of how a single piece of data might be thought of:

```sql
-- A single data item (e.g., a book title) is just a value.
-- No SQL command yet; we are only naming the idea of “value”.
```

## Practical Example
Imagine a **digital library** catalog. The catalog stores many separate data items:

- Book title: `"The Great Gatsby"`  
- Author name: `"F. Scott Fitzgerald"`  
- Publication year: `1925`  

Each item alone is just data. When we display them together as a row in a table, users can understand that *the book “The Great Gatsby” was written by F. Scott Fitzgerald and published in 1925*—that is information.

## Common Mistakes Beginners Make
1. **Treating data as if it already has meaning**  
   ```sql
   -- WRONG: Assuming "42" automatically tells us anything useful.
   ```
2. **Ignoring persistence** – thinking data disappears when the program ends.  
   ```sql
   -- WRONG: Believing a value entered today will be gone tomorrow without storage.
   ```
3. **Overlooking the binary nature of storage** – expecting the computer to keep “words” directly.  
   ```sql
   -- WRONG: Expecting the computer to store "Alice" as letters, not as 0/1 patterns.
   ```

## Programming Challenge
*Conceptual task (no code required):*  
Write, in plain English, a short description of three different pieces of data you might store for a **movie** in a library (e.g., title, director, release year). Then explain how putting those three pieces together gives a user useful information about the movie.

## Solution
A possible answer:

- Data items: `"Inception"` (title), `"Christopher Nolan"` (director), `2010` (release year).  
- When shown together, a user instantly knows *the movie “Inception” was directed by Christopher Nolan and released in 2010*, turning raw data into meaningful information.

## What Comes Next
Next we will explore **Information**—how context turns raw data into something useful—and then dive into the three major categories of data storage:

1. **Structured data** – tables with a fixed schema (SQL databases).  
2. **Semi‑structured data** – flexible formats like JSON or XML.  
3. **Unstructured data** – files such as images, videos, and free‑form text.  

Understanding these categories will prepare you to design and query databases effectively.