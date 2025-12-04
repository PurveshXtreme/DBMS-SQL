# Common SQL Interview Queries — Practice Sheet

## Table of Contents

- [Basic SELECT / Filtering / Sorting](#basic-select--filtering--sorting)  
- [Aggregate Functions & GROUP BY / HAVING](#aggregate-functions--group-by--having)  
- [JOINs and Combining Tables](#joins-and-combining-tables)  
- [Subqueries & Correlated Subqueries](#subqueries--correlated-subqueries)  
- [Ranking / Nth-Highest / Window Functions](#ranking--nth-highest--window-functions)  
- [De-duplication, NULL-handling, Existence & Anti-Join Patterns](#de-duplication--null-handling--existence--anti-join-patterns)  
- [Set Operations, UNION / UNION ALL](#set-operations--union--union-all)  
- [Common Table Expressions (CTE) & Recursive Queries](#common-table-expressions-cte--recursive-queries)  
- [Misc / Utility Queries (e.g. first/last record per group, gaps, pagination)](#misc--utility-queries)  

---

## Basic SELECT / Filtering / Sorting

```sql
-- Select all columns from a table
SELECT * FROM Employees;

-- Select specific columns
SELECT id, name, salary FROM Employees;

-- Filtering using WHERE, with comparisons
SELECT * FROM Employees WHERE salary > 50000;
SELECT * FROM Employees WHERE name LIKE 'A%';
SELECT * FROM Employees WHERE dept_id IN (1, 2, 3);

-- Sorting results
SELECT id, name, salary FROM Employees ORDER BY salary DESC;
SELECT id, name, salary FROM Employees ORDER BY dept_id ASC, salary DESC;

-- Limit (MySQL / PostgreSQL style)
SELECT * FROM Employees ORDER BY salary DESC LIMIT 10;
```

---

## Aggregate Functions & GROUP BY / HAVING

```sql
-- Count of employees per department
SELECT department_id, COUNT(*) AS emp_count
FROM Employees
GROUP BY department_id;

-- Sum / Average / Min / Max salary per department
SELECT department_id, 
       SUM(salary) AS total_salary, 
       AVG(salary) AS avg_salary, 
       MIN(salary) AS min_salary,
       MAX(salary) AS max_salary
FROM Employees
GROUP BY department_id;

-- Departments with more than 5 employees
SELECT department_id, COUNT(*) AS emp_count
FROM Employees
GROUP BY department_id
HAVING COUNT(*) > 5;

-- Example combining filtering + aggregation
SELECT department_id, AVG(salary) AS avg_salary
FROM Employees
WHERE joining_date >= '2023-01-01'
GROUP BY department_id
HAVING AVG(salary) > 60000;
```

---

## JOINs and Combining Tables

```sql
-- INNER JOIN: only matching rows
SELECT e.name, d.department_name
FROM Employees e
INNER JOIN Departments d
    ON e.dept_id = d.id;

-- LEFT JOIN: all from left, match or null from right
SELECT p.id, p.first_name, a.city, a.state
FROM Person p
LEFT JOIN Address a
    ON p.personId = a.personId;

-- RIGHT JOIN: all from right, match or null from left
SELECT e.name, d.manager_id
FROM Employees e
RIGHT JOIN Managers d
    ON e.id = d.emp_id;

-- FULL OUTER JOIN (if supported / or via union workaround)
-- Some DBs don’t support FULL JOIN — combine LEFT + RIGHT
SELECT e.id, d.department_name
FROM Employees e
LEFT JOIN Departments d ON e.dept_id = d.id
UNION
SELECT e.id, d.department_name
FROM Employees e
RIGHT JOIN Departments d ON e.dept_id = d.id;
```

---

## Subqueries & Correlated Subqueries

```sql
-- Simple subquery: find employees earning more than overall average
SELECT * FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);

-- Correlated subquery: employees earning more than their department’s average
SELECT e.id, e.name, e.salary
FROM Employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM Employees
    WHERE department_id = e.department_id
);

-- Subquery in FROM (derived table)
SELECT dept_id, avg_salary, emp_count
FROM (
   SELECT department_id AS dept_id,
          AVG(salary) AS avg_salary,
          COUNT(*) AS emp_count
   FROM Employees
   GROUP BY department_id
) AS DeptStats
WHERE emp_count > 5;
```

---

## Ranking / Nth-Highest / Window Functions

```sql
-- 2nd highest salary using subquery (generic SQL)
SELECT MAX(salary) AS SecondHighestSalary
FROM Employees
WHERE salary < (SELECT MAX(salary) FROM Employees);

-- 2nd highest salary using DISTINCT + ORDER BY + LIMIT (MySQL / PostgreSQL)
SELECT DISTINCT salary 
FROM Employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;

-- Nth highest salary (e.g. 5th) using window function
WITH RankedSalaries AS (
  SELECT salary,
         ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn
  FROM Employees
)
SELECT salary
FROM RankedSalaries
WHERE rn = 5;

-- Rank per department (top 3 salaries per dept)
SELECT name, department_id, salary
FROM (
  SELECT name, department_id, salary,
         RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dept_rank
  FROM Employees
) sub
WHERE dept_rank <= 3;

-- Running total (cumulative sum) per department ordered by hire_date
SELECT name, department_id, hire_date,
       SUM(salary) OVER (PARTITION BY department_id ORDER BY hire_date) AS running_total
FROM Employees;
```

---

## De-duplication, NULL-handling, Existence & Anti-Join Patterns

```sql
-- Find duplicate rows based on some columns
SELECT name, department_id, COUNT(*) AS cnt
FROM Employees
GROUP BY name, department_id
HAVING COUNT(*) > 1;

-- Delete duplicates, keep lowest id (MySQL style example)
DELETE FROM Employees
WHERE id NOT IN (
  SELECT MIN(id)
  FROM Employees
  GROUP BY name, department_id, salary
);

-- Find records in one table with no matching records in another (anti-join pattern)
-- E.g. products never ordered
SELECT p.product_id, p.product_name
FROM Products p
LEFT JOIN Orders o
  ON p.product_id = o.product_id
WHERE o.order_id IS NULL;

-- NULL handling example
SELECT * FROM Employees WHERE manager_id IS NULL;
```

---

## Set Operations — UNION / UNION ALL

```sql
-- Combine results of two queries, remove duplicates
SELECT name, email FROM Customers_US
UNION
SELECT name, email FROM Customers_Europe;

-- Combine results and keep duplicates
SELECT name, email FROM Customers_US
UNION ALL
SELECT name, email FROM Customers_Europe;
```

---

## Common Table Expressions (CTE) & Recursive Queries

```sql
-- Simple CTE for readability / modularization
WITH DeptSalary AS (
  SELECT department_id, AVG(salary) AS avg_salary
  FROM Employees
  GROUP BY department_id
)
SELECT e.name, e.salary, d.avg_salary
FROM Employees e
JOIN DeptSalary d
  ON e.department_id = d.department_id;

-- Recursive CTE — hierarchical data (e.g. org chart)
WITH RECURSIVE EmployeeHierarchy AS (
  SELECT id, name, manager_id
  FROM Employees
  WHERE manager_id IS NULL  -- top-level managers
  UNION ALL
  SELECT e.id, e.name, e.manager_id
  FROM Employees e
  JOIN EmployeeHierarchy eh
    ON e.manager_id = eh.id
)
SELECT * FROM EmployeeHierarchy;
```

---

## Misc / Utility Queries

```sql
-- Get first and last record by date (e.g. earliest / latest hire)
(SELECT * FROM Employees ORDER BY hire_date ASC LIMIT 1)
UNION
(SELECT * FROM Employees ORDER BY hire_date DESC LIMIT 1);

-- Find gaps / missing IDs in a sequence (e.g. employee IDs)
SELECT (e1.id + 1) AS missing_id
FROM Employees e1
LEFT JOIN Employees e2
  ON e1.id + 1 = e2.id
WHERE e2.id IS NULL;

-- Pagination (MySQL / PostgreSQL style)
SELECT * FROM Employees
ORDER BY id
LIMIT 10 OFFSET 20;
```

---

## 🔎 Why These Queries Matter

- They cover nearly all SQL fundamentals that interviewers commonly test: basic retrieval, filtering, sorting, grouping, joining, subqueries, windowing, de-duplication, set ops, CTEs, recursion, and edge-case handling (NULLs, duplicates, gaps).  
- Many of these — e.g. Nth highest salary, de-duplication, anti-join patterns — appear repeatedly across SQL interview question lists. :contentReference[oaicite:0]{index=0}  
- Mastering them ensures you’re prepared for freshers, junior-level, or even medium-level SQL rounds (as expected by companies like yours).  

---

If you like — I can also **add 10–15 “challenge / tricky” queries** (slightly harder than medium) which often appear in tougher interviews.  
``` ````
::contentReference[oaicite:1]{index=1}
