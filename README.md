# SQL

SQL (Structured Query Language) is a standard language used to communicate with and manage data in relational database management systems (RDBMS) such as SQL Server, MySQL, PostgreSQL, and Oracle. SQL is used to create, modify, retrieve, and manipulate data stored in databases.

---
1. DDL (Data Definition Language)
Used to define and modify the structure of database objects (tables, schemas, etc.).
•	CREATE: Creates a new table or database.
•	ALTER: Modifies an existing database object.
•	DROP: Deletes database objects.
•	TRUNCATE: Removes all records from a table, but not the table itself.
---

---

DML (Data Manipulation Language)
Used to manage data within tables.
•	SELECT: Retrieves data from the database.
•	INSERT: Adds new data.
•	UPDATE: Modifies existing data.
•	DELETE: Removes data.
---

---
DCL (Data Control Language)
Used to control access to data in the database.
•	GRANT: Gives user access privileges.
•	REVOKE: Removes user access privileges.
---
---
 TCL (Transaction Control Language)
Used to manage transactions in the database.
•	COMMIT: Saves all changes made in the transaction.
•	ROLLBACK: Undoes changes since the last commit.
•	SAVEPOINT: Sets a point within a transaction to which you can roll back.
---

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


---
1. What is the difference between INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL OUTER JOIN?
Answer:
•	INNER JOIN: Returns only matching rows from both tables.
•	LEFT JOIN: Returns all rows from the left table, and matching rows from the right table (NULL if no match).
•	RIGHT JOIN: Returns all rows from the right table, and matching rows from the left table (NULL if no match).
•	FULL OUTER JOIN: Returns all rows when there is a match in either left or right table.

```
SELECT a.Name, b.OrderId
FROM Customers a
INNER JOIN Orders b ON a.CustomerId = b.CustomerId;
```
3. What is a primary key? What is a foreign key?
Answer:
•	Primary Key: Uniquely identifies each record in a table.
•	Foreign Key: A field in one table that refers to the primary key in another table, establishing a relationship.
Example:

```
CREATE TABLE Customers (
    CustomerId INT PRIMARY KEY,
    Name NVARCHAR(100)
);

CREATE TABLE Orders (
    OrderId INT PRIMARY KEY,
    CustomerId INT,
    FOREIGN KEY (CustomerId) REFERENCES Customers(CustomerId)
);
```
How do you retrieve the second highest salary from an Employee table?
```
SELECT MAX(Salary) AS SecondHighest
FROM Employees
WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```
What is a view? What are its advantages?
Answer:
A view is a virtual table based on the result of a SQL query.
Advantages: Simplifies complex queries, enhances security, and provides abstraction.
```
CREATE VIEW ActiveCustomers AS
SELECT * FROM Customers WHERE IsActive = 1;
```
What is a stored procedure?
Answer:
A stored procedure is a precompiled collection of SQL statements that can be executed as a single unit.
```
CREATE PROCEDURE GetCustomerOrders
    @CustomerId INT
AS
BEGIN
    SELECT * FROM Orders WHERE CustomerId = @CustomerId;
END
```
What is a CTE (Common Table Expression)?

A CTE is a temporary result set used within a query used for recursion & readability

```
WITH SalesCTE AS (
    SELECT * FROM Sales WHERE Amount > 1000
)
SELECT * FROM SalesCTE WHERE Region = 'West';
```
Explain window functions with an example.
Answer:
Window functions perform calculations across a set of table rows related to the current row.
Example:

```
with gap when multiple rows having same rank
SELECT EmployeeId, Salary,
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
without gap when multiple rows having same rank
SELECT EmployeeId, Salary,
       DEEP_RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
--Sequntial number
SELECT EmployeeId, Salary,
       ROW_Number() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;

```

Unique records from table
```
SELECT DISTINCT FirstName, LastName, Department
FROM Employees;
```

A table can have only one primary key constraint, but that primary key can consist of multiple columns—this is called a composite primary key.

```
CREATE TABLE Orders (
    OrderId INT,
    ProductId INT,
    Quantity INT,
    PRIMARY KEY (OrderId, ProductId)
);
```

A composite key (or composite primary key) uses two or more columns together to uniquely identify each row.
•	Here, the combination of OrderId and ProductId forms the composite key.



