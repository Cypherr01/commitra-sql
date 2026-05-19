# Topic: What is Data?
## What Is This?
Data refers to raw facts and figures that have no inherent meaning on their own. Examples of data include numbers (`42`), text (`"Alice"`), and dates (`2024-01-01`). Data can be thought of as the building blocks of information. When data is given context and meaning, it becomes information.

## How It Works Internally
Computers store data in a way that allows it to persist even after the program that created it has finished executing. This is known as persistence. Data can be stored in various forms, including structured, semi-structured, and unstructured formats. Structured data is organized into tables with well-defined schemas, such as in SQL databases. Semi-structured data, on the other hand, has some level of organization but does not follow a rigid schema, examples include key-value stores, JSON, and XML. Unstructured data, such as images, video, audio, and freeform text, does not have a predefined organization.

## Syntax and Structure
Since we are just starting to learn about data, we don't have a specific syntax to follow yet. However, we can use simple examples to illustrate the concept of data. For instance, in a library catalog, we might have data such as book titles, authors, and publication dates.
```sql
-- Simple example of data in a library catalog
CREATE TABLE books (
  title VARCHAR(255),
  author VARCHAR(255),
  publication_date DATE
);

-- Inserting some sample data
INSERT INTO books (title, author, publication_date)
VALUES ('To Kill a Mockingbird', 'Harper Lee', '1960-07-11');
```
## Practical Example
Let's consider a simple example of a digital library catalog. We can create a basic HTML page to display the catalog, but first, we need to understand what data we want to store. In this case, we might want to store information about books, such as titles, authors, and publication dates.

## Common Mistakes Beginners Make
When working with data, beginners often make the following mistakes:
1. **Confusing data with information**: Beginners might think that data and information are the same thing, but data is just the raw facts and figures, while information is data with context and meaning.
2. **Not understanding the importance of data storage**: Beginners might not realize that data storage is crucial for persistence and that it's the foundation of every application.
3. **Not distinguishing between structured, semi-structured, and unstructured data**: Beginners might not understand the differences between these types of data and how they are used in different contexts.

## Programming Challenge
Create a simple table to store data about books in a library catalog. The table should include columns for title, author, and publication date.

## Solution
```sql
CREATE TABLE books (
  title VARCHAR(255),
  author VARCHAR(255),
  publication_date DATE
);
```
## What Comes Next
Now that we have a basic understanding of what data is, we can start exploring how to work with data in SQL databases. In the next topic, we will learn about the basics of SQL and how to create and manage databases. We will also start building our digital library project by designing a database schema to store book information.