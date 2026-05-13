# Topic: What is Data?
## What Is This?
Data are the raw facts and values that we store in a computer.  
In a database, each **piece of data** is a single value such as a number, a word, a date, or a piece of text.  
When many pieces of data are grouped together they form a **record** (think of one row in a table), and many records together make up a **dataset** (think of the whole table).

## How It Works Internally
- **Bits and Bytes** – At the lowest level the computer represents everything as 0s and 1s (bits).  
- **Data Types** – The database knows how to interpret those bits: a group of bits can be treated as an integer, a string, a date, etc.  
- **Storage** – The database engine writes those bytes to disk in pages so they can be retrieved later.

## Syntax and Structure
Below is a *purely illustrative* SQL comment that shows what a single piece of data looks like.  
No executable statement is used because we have not yet introduced table creation or data‑manipulation commands.

```sql
-- A single data value: the title of a book
-- Example value:  'Pride and Prejudice'

-- A second data value: the year the book was published
-- Example value:  1813
```

The comments describe two separate data items (a text value and a numeric value).  
When we later learn about tables, each row will hold many such values together.

## Practical Example
Imagine we are building a **Digital Library**.  
The *data* we need for each book might include:

1. **Title** – text, e.g., `The Great Gatsby`  
2. **Author** – text, e.g., `F. Scott Fitzgerald`  
3. **Publication Year** – integer, e.g., `1925`

Each of those three items is a piece of data.  
When we later create a table, one row will contain the three data values for a single book.

## Common Mistakes Beginners Make
| Mistake | What It Looks Like (What NOT to Do) |
|---------|--------------------------------------|
| 1. Treating data as “information” | Thinking that writing `The Great Gatsby` *already* tells the system the author – it is only a raw value, not processed information. |
| 2. Mixing data types in the same place | Storing the year as text: `‘1925’` instead of a numeric value `1925`. This can cause sorting or calculation problems later. |
| 3. Inconsistent formatting | Writing dates in different styles, e.g., `1925-04-10` **and** `04/10/1925`. The database would see them as different kinds of data. |

## Programming Challenge
Write down, in plain English, **three separate pieces of data** you would need to describe a book in your digital library. List each piece on its own line.

## Solution
```
1. Title – the name of the book (text)
2. Author – the person who wrote the book (text)
3. Publication Year – the year the book was first published (integer)
```

These three items are the **data** that will later become columns in a table.

## What Comes Next
Now that you understand what *data* is, the next step is to learn how to **organize data into tables**.  
We will introduce the `CREATE TABLE` statement, define column names and data types, and see how a collection of data values becomes a structured dataset ready for querying.