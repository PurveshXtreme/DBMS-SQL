## Table of Contents

1. [SQL Basics (Foundation Coding)](#-1-sql-basics-foundation-coding)
2. [SQL Data Types](#-2-sql-data-types)
3. [Constraints (Coding-Based)](#-3-constraints-coding-based)
4. [SQL Filtering & Searching](#-4-sql-filtering--searching)
5. [Sorting & Limiting](#-5-sorting--limiting)
6. [Aggregate Functions](#-7-aggregate-functions)
7. [GROUP BY & HAVING](#-8-group-by--having)
8. [JOINS (Most Important Coding Topic)](#-9-joins-most-important-coding-topic)
9. [Subqueries](#-10-subqueries)
10. [Set Operations](#-11-set-operations)
11. [SQL Functions (Coding Heavy)](#-12-sql-functions-coding-heavy)

---
---



# 🟩 1. SQL Basics (Foundation Coding)

## ✔ Creating a Database
```sql
CREATE DATABASE mydb;
```

## ✔ Using a Database
```sql
USE mydb;
```

## ✔ Creating Tables
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary INT
);
```

## ✔ Inserting Data
```sql
INSERT INTO employees VALUES (1, 'Purvesh', 50000);
```

## ✔ Updating Data
```sql
UPDATE employees 
SET salary = 60000 
WHERE id = 1;
```

## ✔ Deleting Data
```sql
DELETE FROM employees 
WHERE id = 1;
```

## ✔ Selecting Data
```sql
SELECT * FROM employees;
```

---

# 🟦 2. SQL Data Types

- `INT`  
- `VARCHAR(n)`  
- `DATE`  
- `DATETIME`  
- `BOOLEAN`  
- `FLOAT` / `DOUBLE`  
- `TEXT`  

---

# 🟧 3. Constraints (Coding-Based)

### ✔ PRIMARY KEY  
### ✔ FOREIGN KEY  
### ✔ UNIQUE  
### ✔ NOT NULL  
### ✔ CHECK  
### ✔ DEFAULT  

### Example:
```sql
CREATE TABLE student (
    roll INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT CHECK (age > 0),
    city VARCHAR(50) DEFAULT 'Pune'
);
```

### Example with FOREIGN KEY:
```sql
CREATE TABLE department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES department(dept_id)
);
```

---
---

# 🟩 4. SQL Filtering & Searching

## ✔ WHERE (Filter rows based on a condition)
```sql
SELECT * 
FROM employees
WHERE salary > 50000;
```

## ✔ BETWEEN (Range filter, inclusive)
```sql
SELECT * 
FROM employees
WHERE salary BETWEEN 30000 AND 70000;
```

## ✔ IN (Match any value from a list)
```sql
SELECT * 
FROM employees
WHERE dept_id IN (1, 3, 5);
```

## ✔ LIKE (Pattern matching)
```sql
SELECT * 
FROM employees
WHERE name LIKE 'P%';     -- Starts with P

SELECT * 
FROM employees
WHERE name LIKE '%sh';    -- Ends with sh

SELECT * 
FROM employees
WHERE name LIKE '_a%';    -- Second letter is 'a'
```

## ✔ IS NULL / IS NOT NULL (Check for empty values)
```sql
SELECT * 
FROM employees
WHERE manager_id IS NULL;

SELECT * 
FROM employees
WHERE email IS NOT NULL;
```

---

# 🟦 5. Sorting & Limiting

## ✔ ORDER BY (Sort results ascending/descending)
```sql
SELECT * 
FROM employees
ORDER BY salary ASC;

SELECT * 
FROM employees
ORDER BY salary DESC;
```

## ✔ LIMIT (MySQL/PostgreSQL)
```sql
SELECT * 
FROM employees
ORDER BY salary DESC
LIMIT 5;      -- Top 5 highest salaries
```

## ✔ TOP (SQL Server)
```sql
SELECT TOP 5 *
FROM employees
ORDER BY salary DESC;
```


---
---

# 🟪 7. Aggregate Functions

Aggregate functions perform calculations on a set of values and return a single result.

---

## ✔ COUNT() — Counts rows
```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```

---

## ✔ SUM() — Adds numeric values
```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

---

## ✔ AVG() — Calculates average value
```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

---

## ✔ MIN() — Smallest value
```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```

---

## ✔ MAX() — Highest value
```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```


---
---


# 🟫 8. GROUP BY & HAVING

GROUP BY is used to group rows based on a column, and HAVING is used to filter groups (like WHERE for groups).

---

## ✔ GROUP BY (Group rows and apply aggregates)

```sql
SELECT dept_id, COUNT(*) AS total_employees
FROM employees
GROUP BY dept_id;
```

This returns how many employees are in each department.

---

## ✔ GROUP BY with multiple columns

```sql
SELECT dept_id, job_role, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id, job_role;
```

---

## ✔ HAVING (Filter groups after grouping)

WHERE → filters rows  
HAVING → filters groups  

```sql
SELECT dept_id, COUNT(*) AS total_employees
FROM employees
GROUP BY dept_id
HAVING COUNT(*) > 5;   -- only departments with more than 5 employees
```

---

## ✔ HAVING with Aggregate Conditions

```sql
SELECT dept_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id
HAVING AVG(salary) > 60000;
```

---

## ✔ GROUP BY + WHERE together

```sql
SELECT dept_id, SUM(salary) AS total_salary
FROM employees
WHERE salary > 30000      -- filter rows first
GROUP BY dept_id
HAVING SUM(salary) > 200000;  -- filter groups next
```


---
---

# 🟥 9. JOINS (Most Important Coding Topic)

Joins are used to combine rows from two or more tables based on a related column.

---

# ✔ INNER JOIN  
Returns **matching rows only** from both tables.

```sql
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN department d
ON e.dept_id = d.dept_id;
```

---

# ✔ LEFT JOIN (LEFT OUTER JOIN)  
Returns **all rows from left table**, and matched rows from right table.  
If no match → NULL.

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN department d
ON e.dept_id = d.dept_id;
```

---

# ✔ RIGHT JOIN (RIGHT OUTER JOIN)  
Returns **all rows from right table**, and matched rows from left table.

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN department d
ON e.dept_id = d.dept_id;
```

---

# ✔ FULL OUTER JOIN  
Returns **all rows from both tables**, with NULL where no match.  
(Available in PostgreSQL, SQL Server; not in MySQL without workaround.)

```sql
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN department d
ON e.dept_id = d.dept_id;
```

---

# ✔ SELF JOIN  
Join a table with itself.  
Useful for hierarchical data (manager → employee).

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.id;
```

---

# ✔ CROSS JOIN  
Returns **Cartesian product** (every row of A × every row of B).

```sql
SELECT e.name, d.dept_name
FROM employees e
CROSS JOIN department d;
```
---
---

# 🟦 10. Subqueries

Subqueries are queries inside another query.

---

## ✔ Single-row Subquery  
Returns **one value**.  
Used with: =, >, <, >=, <=

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);
```

---

## ✔ Multi-row Subquery (IN, ANY, ALL)

### 🔹 IN  
```sql
SELECT name
FROM employees
WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE location = 'Pune'
);
```

### 🔹 ANY  
```sql
SELECT name
FROM employees
WHERE salary > ANY (
    SELECT salary FROM interns
);
```

### 🔹 ALL  
```sql
SELECT name
FROM employees
WHERE salary > ALL (
    SELECT salary FROM interns
);
```

---

## ✔ Correlated Subquery  
Runs **once for each row** of the outer query.

```sql
SELECT e1.name
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.dept_id = e1.dept_id
);
```

---

## ✔ Subquery in SELECT  
```sql
SELECT name,
       (SELECT COUNT(*) FROM orders o WHERE o.emp_id = e.id) AS total_orders
FROM employees e;
```

---

## ✔ Subquery in FROM (Inline View)  
```sql
SELECT dept_id, avg_salary
FROM (
    SELECT dept_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept_id
) AS temp;
```

---

## ✔ Subquery in WHERE  
```sql
SELECT name
FROM employees
WHERE dept_id = (
    SELECT dept_id FROM departments WHERE dept_name = 'IT'
);
```

---

# 🟧 11. Set Operations

Set operators combine results from two SELECT queries.

---

## ✔ UNION  
Removes duplicates.

```sql
SELECT name FROM table1
UNION
SELECT name FROM table2;
```

---

## ✔ UNION ALL  
Keeps duplicates.

```sql
SELECT name FROM table1
UNION ALL
SELECT name FROM table2;
```

---

## ✔ INTERSECT  
Returns **common rows** (not supported directly in MySQL).

```sql
SELECT email FROM customers_2024
INTERSECT
SELECT email FROM customers_2025;
```

---

## ✔ EXCEPT / MINUS  
Returns rows in the first query **not present** in the second.  
(EXCEPT = PostgreSQL, MINUS = Oracle)

```sql
SELECT id FROM tableA
EXCEPT
SELECT id FROM tableB;
```

Oracle:
```sql
SELECT id FROM tableA
MINUS
SELECT id FROM tableB;
```

---
---

# 🟩 12. SQL Functions (Coding Heavy)

---

# ✔ String Functions

## 🔹 LENGTH()
```sql
SELECT LENGTH('Purvesh') AS name_length;
```

## 🔹 CONCAT()
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

## 🔹 SUBSTRING() / SUBSTR()
```sql
SELECT SUBSTRING('LearnPlay', 1, 5) AS part_string;   -- Output: Learn
```

## 🔹 UPPER() / LOWER()
```sql
SELECT UPPER(name), LOWER(name)
FROM employees;
```

## 🔹 TRIM()
```sql
SELECT TRIM('   Hello World   ') AS cleaned_text;
```

## 🔹 REPLACE()
```sql
SELECT REPLACE('JavaScript', 'Java', 'Type') AS updated_text;  -- Output: TypeScript
```

---

# ✔ Date Functions

## 🔹 NOW()
```sql
SELECT NOW() AS current_datetime;
```

## 🔹 CURDATE()
```sql
SELECT CURDATE() AS current_date;
```

## 🔹 DATEDIFF()
```sql
SELECT DATEDIFF('2025-12-31', '2025-01-01') AS days_difference;
```

## 🔹 YEAR(), MONTH(), DAY()
```sql
SELECT 
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    DAY(order_date) AS order_day
FROM orders;
```

---

# ✔ Numeric Functions

## 🔹 ROUND()
```sql
SELECT ROUND(12.5678, 2) AS rounded_value;   -- Output: 12.57
```

## 🔹 CEIL()
```sql
SELECT CEIL(10.2) AS ceiling_value;   -- Output: 11
```

## 🔹 FLOOR()
```sql
SELECT FLOOR(10.9) AS floor_value;   -- Output: 10
```

## 🔹 ABS()
```sql
SELECT ABS(-45) AS absolute_value;   -- Output: 45
```

## 🔹 MOD()
```sql
SELECT MOD(17, 5) AS remainder;   -- Output: 2
```


---
---





