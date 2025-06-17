# SQL

# SQL Interview Questions & Answers

This document provides common SQL interview questions with concise answers and practical examples.

---

## 1. What is the difference between `INNER JOIN` and `LEFT JOIN`?

**Answer:**  
- `INNER JOIN` returns only the rows with matching values in both tables.
- `LEFT JOIN` returns all rows from the left table, and matched rows from the right table. If there is no match, NULLs are returned for columns from the right table.

**Example:**
```
-- INNER JOIN SELECT a.Name, b.OrderDate FROM Customers a INNER JOIN Orders b ON a.CustomerId = b.CustomerId;
-- LEFT JOIN SELECT a.Name, b.OrderDate FROM Customers a LEFT JOIN Orders b ON a.CustomerId = b.CustomerId;
```
---

## 2. What is a subquery? Give an example.

**Answer:**  
A subquery is a query nested inside another query.

**Example:**
```
SELECT Name FROM Customers WHERE CustomerId IN (SELECT CustomerId FROM Orders WHERE Amount > 1000);
```

---

## 3. How do you find duplicate records in a table?

**Answer:**  
Use `GROUP BY` and `HAVING` to find duplicates.

**Example:**
```
SELECT Email, COUNT() FROM Users GROUP BY Email HAVING COUNT() > 1;
```

---

## 4. What is the difference between `WHERE` and `HAVING`?

**Answer:**  
- `WHERE` filters rows before grouping.
- `HAVING` filters groups after aggregation.

**Example:**
```
SELECT Department, COUNT() FROM Employees WHERE IsActive = 1 GROUP BY Department HAVING COUNT() > 5;
```

---

## 5. How do you update data in SQL?

**Answer:**
```
UPDATE Products SET Price = Price * 1.1 WHERE Category = 'Electronics';
```

---

## 6. What is an index? Why is it important?

**Answer:**  
An index is a database object that improves the speed of data retrieval. It is important for performance, especially on large tables.

**Example:**
```
CREATE INDEX idx_customer_name ON Customers(Name);

```

---

## 7. How do you get the second highest salary from an Employee table?

**Answer:**
```
SELECT MAX(Salary) AS SecondHighest FROM Employees WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```

---

## 8. What is normalization?

**Answer:**  
Normalization is the process of organizing data to reduce redundancy and improve data integrity.

---

QUOTED_IDENTIFIER is a setting in SQL Server that controls how SQL Server interprets the use of double quotation marks (") in SQL statements.
---
What does QUOTED_IDENTIFIER do?
•	ON (default):
•	Double quotes (" ") can be used to delimit identifiers (such as table or column names), allowing you to use reserved keywords or special characters in those names.
•	Single quotes (' ') are still used for string literals.
•	OFF:
•	Double quotes are treated as string delimiters (like single quotes).
•	Identifiers must be delimited by square brackets ([ ]) if they contain special characters or reserved words.
---
Examples
```
SET QUOTED_IDENTIFIER ON;

CREATE TABLE "Order" (
    "Id" INT,
    "Select" NVARCHAR(50)
);

SELECT "Id", "Select" FROM "Order";
SET QUOTED_IDENTIFIER OFF;

-- This will fail:
-- CREATE TABLE "Order" ( ... )

-- Use square brackets instead:
CREATE TABLE [Order] (
    [Id] INT,
    [Select] NVARCHAR(50)
);
```

SET ANSI_NULLS is a setting in SQL Server that controls how SQL Server handles comparisons to NULL values in queries.
---
What does SET ANSI_NULLS do?
•	ON (default and recommended):
•	Any comparison to NULL using = or != returns UNKNOWN (not TRUE or FALSE).
•	You must use IS NULL or IS NOT NULL to check for NULL values.
•	OFF:
•	Comparisons to NULL using = or != behave as if NULL is a value, so column = NULL can return TRUE if the column is NULL.
---
Examples
```
SET ANSI_NULLS ON;

SELECT * FROM Users WHERE Name = NULL;      -- Returns no rows
SELECT * FROM Users WHERE Name IS NULL;     -- Returns rows where Name is NULL

SET ANSI_NULLS OFF;

SELECT * FROM Users WHERE Name = NULL;      -- Returns rows where Name is NULL (not standard SQL behavior)
```

