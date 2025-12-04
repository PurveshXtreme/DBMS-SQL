# Most Common SQL Interview **Coding** Questions  
*(Easy → Medium, asked across service + product companies)*

## 📑 Table of Contents  
- [1. Basic SELECT / Filtering](#1-basic-select--filtering)  
- [2. Sorting / Limiting](#2-sorting--limiting)  
- [3. Aggregate Functions](#3-aggregate-functions)  
- [4. GROUP BY + HAVING](#4-group-by--having)  
- [5. JOINs](#5-joins)  
- [6. Subqueries](#6-subqueries)  
- [7. Nth Highest / Ranking](#7-nth-highest--ranking)  
- [8. Duplicate Handling](#8-duplicate-handling)  
- [9. NULL Handling](#9-null-handling)  
- [10. CASE Expressions](#10-case-expressions)  
- [11. Set Operations](#11-set-operations)  
- [12. CTE / Window Functions](#12-cte--window-functions)  
- [13. Misc Practical Queries](#13-misc-practical-queries)

---

## 1. Basic SELECT / Filtering  
```sql
-- 1. Get all employees with salary > 50000
SELECT * FROM Employees WHERE salary > 50000;

-- 2. Fetch employees whose name starts with 'A'
SELECT * FROM Employees WHERE name LIKE 'A%';

-- 3. Fetch employees from departments 1, 3, and 5
SELECT * FROM Employees WHERE dept_id IN (1,3,5);
```

---

## 2. Sorting / Limiting  
```sql
-- 4. Get top 5 highest-paid employees
SELECT * FROM Employees ORDER BY salary DESC LIMIT 5;

-- 5. Sort employees by department, then salary
SELECT * FROM Employees ORDER BY dept_id, salary DESC;
```

---

## 3. Aggregate Functions  
```sql
-- 6. Count employees in company
SELECT COUNT(*) FROM Employees;

-- 7. Find average salary per department
SELECT dept_id, AVG(salary) FROM Employees GROUP BY dept_id;
```

---

## 4. GROUP BY + HAVING  
```sql
-- 8. Departments having more than 5 employees
SELECT dept_id, COUNT(*) 
FROM Employees
GROUP BY dept_id
HAVING COUNT(*) > 5;

-- 9. Departments with average salary > 60000
SELECT dept_id, AVG(salary)
FROM Employees
GROUP BY dept_id
HAVING AVG(salary) > 60000;
```

---

## 5. JOINs  
```sql
-- 10. Get employees with their department names
SELECT e.name, d.department_name
FROM Employees e
JOIN Departments d ON e.dept_id = d.id;

-- 11. List employees who have no manager assigned
SELECT e.name
FROM Employees e
LEFT JOIN Managers m ON e.manager_id = m.id
WHERE m.id IS NULL;

-- 12. Fetch all departments even if no employees exist
SELECT d.department_name, e.name
FROM Departments d
LEFT JOIN Employees e ON d.id = e.dept_id;
```

---

## 6. Subqueries  
```sql
-- 13. Employees earning more than company average
SELECT * FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);

-- 14. Employees with salary = highest salary
SELECT * FROM Employees
WHERE salary = (SELECT MAX(salary) FROM Employees);
```

---

## 7. Nth Highest / Ranking  
```sql
-- 15. Second highest salary (subquery method)
SELECT MAX(salary)
FROM Employees
WHERE salary < (SELECT MAX(salary) FROM Employees);

-- 16. Nth highest salary (generic using LIMIT)
SELECT DISTINCT salary
FROM Employees
ORDER BY salary DESC
LIMIT 1 OFFSET 3;  -- 4th highest

-- 17. Rank employees by salary using window function
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS rnk
FROM Employees;
```

---

## 8. Duplicate Handling  
```sql
-- 18. Find duplicate email IDs
SELECT email, COUNT(*)
FROM Users
GROUP BY email
HAVING COUNT(*) > 1;

-- 19. Delete duplicates, keep lowest ID
DELETE FROM Users
WHERE id NOT IN (
    SELECT MIN(id)
    FROM Users
    GROUP BY email
);
```

---

## 9. NULL Handling  
```sql
-- 20. Fetch employees with no assigned manager
SELECT * FROM Employees WHERE manager_id IS NULL;

-- 21. Replace null commission with 0 (MySQL)
SELECT name, COALESCE(commission, 0) AS commission
FROM Employees;
```

---

## 10. CASE Expressions  
```sql
-- 22. Categorize employees based on salary
SELECT name, salary,
       CASE
           WHEN salary > 80000 THEN 'High'
           WHEN salary BETWEEN 50000 AND 80000 THEN 'Medium'
           ELSE 'Low'
       END AS SalaryLevel
FROM Employees;
```

---

## 11. Set Operations  
```sql
-- 23. Get all unique customer names across US and Europe
SELECT name FROM Customer_US
UNION
SELECT name FROM Customer_EU;

-- 24. Combine all customers and keep duplicates
SELECT name FROM Customer_US
UNION ALL
SELECT name FROM Customer_EU;
```

---

## 12. CTE / Window Functions  
```sql
-- 25. Get department-wise top 2 salaries
WITH SalaryRank AS (
    SELECT name, dept_id, salary,
           RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) AS rnk
    FROM Employees
)
SELECT * FROM SalaryRank WHERE rnk <= 2;

-- 26. Running total of salary ordered by hire date
SELECT name, hire_date, salary,
       SUM(salary) OVER (ORDER BY hire_date) AS cumulative_salary
FROM Employees;
```

---

## 13. Misc Practical Queries  
```sql
-- 27. Get latest hired employee
SELECT * FROM Employees 
ORDER BY hire_date DESC
LIMIT 1;

-- 28. Find gaps in employee ID sequence
SELECT e1.id + 1 AS missing_id
FROM Employees e1
LEFT JOIN Employees e2 ON e1.id + 1 = e2.id
WHERE e2.id IS NULL;

-- 29. Pagination (MySQL/PostgreSQL)
SELECT * FROM Employees
ORDER BY id
LIMIT 10 OFFSET 20;

-- 30. Find employees who did NOT submit timesheets
SELECT e.id, e.name
FROM Employees e
LEFT JOIN Timesheets t ON e.id = t.emp_id
WHERE t.emp_id IS NULL;
```

---

# ✅ Want me to now generate:
### 🔹 50-question SQL Mock Test (with answers)?  
### 🔹 InfoCepts-style SQL test based on company brochure?  
### 🔹 SQL practice sheet categorized by difficulty (Easy–Medium–Hard)?  

Just tell me!  
