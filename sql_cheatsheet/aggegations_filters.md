# SQL Aggregations and Filtering

## Sample Data Used Throughout

### employees

| emp_id | emp_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 1 | Rahul | IT | 50000 | 2022-01-10 |
| 2 | Priya | HR | 40000 | 2021-06-15 |
| 3 | Aman | IT | 60000 | 2023-03-20 |
| 4 | Neha | Finance | 55000 | 2022-08-05 |
| 5 | Karan | HR | 45000 | 2024-02-12 |

### departments

| department |
|---|
| IT |
| HR |
| Finance |
| Sales |

---

#  Aggregate Functions

Aggregate functions perform calculations on multiple rows and return a single result.

Common aggregate functions:

- `COUNT()` – counts rows or values.
- `SUM()` – calculates the total.
- `AVG()` – calculates the average.
- `MIN()` – returns the smallest value.
- `MAX()` – returns the largest value.

### COUNT()

```sql
SELECT
    COUNT(*) AS total_rows,
    COUNT(department) AS non_null_departments,
    COUNT(DISTINCT department) AS unique_departments
FROM employees;
```
**output**

| total_rows | non_null_departments | unique_departments |
|---:|---:|---:|
| 5 | 5 | 3 |

- `COUNT(*)` counts all rows.
- `COUNT(column)` counts non-NULL values.
- `COUNT(DISTINCT column)` counts unique, non-NULL values.

### SUM() and AVG()

```sql
SELECT
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary
FROM employees;
```
**output**

| total_salary | average_salary |
|---:|---:|
| 250000 | 50000.00 |


- `SUM()` adds numeric values.
- `AVG()` calculates `SUM / COUNT` of non-NULL values.
- Both ignore NULL values.

### MIN() and MAX()

```sql
SELECT
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary,
    MIN(hire_date) AS earliest_hire,
    MAX(hire_date) AS latest_hire
FROM employees;
```
**output**
| minimum_salary | maximum_salary | earliest_hire | latest_hire |
|---:|---:|---|---|
| 40000 | 60000 | 2021-06-15 | 2024-02-12 |

`MIN()` and `MAX()` work with numbers, dates, and strings (according to their ordering).

---

#  GROUP BY

`GROUP BY` groups rows that have the same value in one or more columns. It is commonly used with aggregate functions to calculate a result for each group.

### Example: Total salary per department

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```
**output**
| department | total_salary |
|---|---:|
| IT | 110000 |
| HR | 85000 |
| Finance | 55000 |

Each department becomes a group, and `SUM()` calculates its total salary.

### Multiple Aggregate Functions

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```
**output**
| department | employee_count | total_salary | average_salary | minimum_salary | maximum_salary |
|---|---:|---:|---:|---:|---:|
| IT | 2 | 110000 | 55000.00 | 50000 | 60000 |
| HR | 2 | 85000 | 42500.00 | 40000 | 45000 |
| Finance | 1 | 55000 | 55000.00 | 55000 | 55000 |

Multiple aggregate functions can be used in the same grouped query.

### GROUP BY Multiple Columns

Group by more than one column when you need a separate group for each unique combination.

```sql
SELECT department, EXTRACT(YEAR FROM hire_date) AS joining_year,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department, EXTRACT(YEAR FROM hire_date);
```
**output**
| department | joining_year | employee_count |
|---|---:|---:|
| IT | 2022 | 1 |
| HR | 2021 | 1 |
| IT | 2023 | 1 |
| Finance | 2022 | 1 |
| HR | 2024 | 1 |

Each unique department-and-year combination becomes a group.

### GROUP BY Without Aggregate Functions

```sql
SELECT department
FROM employees
GROUP BY department;
```
**output**
| department |
|---|
| IT |
| HR |
| Finance |

This returns one row per department. If the goal is only to get unique values, `DISTINCT` is usually simpler:

```sql
SELECT DISTINCT department
FROM employees;
```
**output**
| department |
|---|
| IT |
| HR |
| Finance |

---

#  HAVING

`HAVING` filters groups created by `GROUP BY`. It is commonly used with aggregate conditions.

### Example: Departments with more than one employee

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 1;
```
**output**
| department | employee_count |
|---|---:|
| IT | 2 |
| HR | 2 |

How it works:
1. `GROUP BY` creates department groups.
2. `COUNT(*)` counts employees in each group.
3. `HAVING` keeps groups whose count is greater than one.

`HAVING` can filter using any aggregate:

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 45000;
```
**output**
| department | average_salary |
|---|---:|
| IT | 55000.00 |
| Finance | 55000.00 |

---

#  WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows. | Filters groups. |
| Applied before grouping. | Applied after grouping. |
| Normally filters column values. | Commonly filters aggregate results. |
| Cannot directly use aggregate functions. | Can use aggregate functions. |

### WHERE example

```sql
SELECT *
FROM employees
WHERE salary > 40000;
```

### HAVING example

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 40000;
```
**output** 
| department | average_salary |
|---|---:|
| IT | 55000.00 |
| HR | 42500.00 |
| Finance | 55000.00 |

### Using WHERE and HAVING Together

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
WHERE salary > 40000
GROUP BY department
HAVING AVG(salary) > 45000;
```
**output**
| department | average_salary |
|---|---:|
| IT | 55000.00 |
| Finance | 55000.00 |

Order of work:
1. `WHERE` removes employees whose salary is not greater than 40000.
2. `GROUP BY` groups the remaining employees by department.
3. `AVG()` calculates each department's average using the remaining rows.
4. `HAVING` keeps groups whose average is greater than 45000.

---

#  WHERE and Filtering Operators

`WHERE` selects only rows that satisfy a condition.

```sql
SELECT *
FROM employees
WHERE condition;
```

## Comparison Operators

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `<>` or `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

`<>` is the standard SQL not-equal operator. `!=` is supported by many databases too.

## AND, OR and NOT

- `AND`: all conditions must be true.
- `OR`: at least one condition must be true.
- `NOT`: reverses a condition.

```sql
SELECT *
FROM employees
WHERE department = 'IT' AND salary > 50000;
```

```sql
SELECT *
FROM employees
WHERE department = 'IT' OR department = 'HR';
```

```sql
SELECT *
FROM employees
WHERE NOT department = 'IT';
```

## BETWEEN

Checks whether a value falls within a range. Both boundaries are included.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 55000;
```

Equivalent to:

```sql
WHERE salary >= 40000 AND salary <= 55000;
```

## IN and NOT IN

`IN` checks whether a value matches any value in a list. `NOT IN` excludes the listed values.

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

`NOT IN` can behave unexpectedly if its list or subquery contains `NULL`. For subqueries, `NOT EXISTS` is often safer.

## LIKE

`LIKE` performs string pattern matching.

| Wildcard | Meaning |
|---|---|
| `%` | Zero or more characters |
| `_` | Exactly one character |

```sql
-- Names starting with A
SELECT * FROM employees WHERE emp_name LIKE 'A%';

-- Names ending with a
SELECT * FROM employees WHERE emp_name LIKE '%a';

-- Names containing an
SELECT * FROM employees WHERE emp_name LIKE '%an%';

-- Names containing exactly four characters
SELECT * FROM employees WHERE emp_name LIKE '____';
```

## IS NULL and IS NOT NULL

Use these to check for missing values.

```sql
SELECT * FROM employees WHERE department IS NULL;
SELECT * FROM employees WHERE department IS NOT NULL;
```

Do not use `= NULL` or `!= NULL`. Use `IS NULL` or `IS NOT NULL`.

---

#  DISTINCT

`DISTINCT` removes duplicate rows from the result.

```sql
SELECT DISTINCT department
FROM employees;
```

With multiple columns, it returns unique combinations of those columns:

```sql
SELECT DISTINCT department, salary
FROM employees;
```

It does not independently remove duplicates from each column.

---

# ORDER BY

`ORDER BY` sorts query results.

- `ASC`: ascending order (default).
- `DESC`: descending order.

```sql
-- Lowest salary first
SELECT * FROM employees ORDER BY salary ASC;

-- Highest salary first
SELECT * FROM employees ORDER BY salary DESC;
```

### Sorting by Multiple Columns

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```
**output**
| emp_id | emp_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 4 | Neha | Finance | 55000 | 2022-08-05 |
| 2 | Priya | HR | 40000 | 2021-06-15 |
| 5 | Karan | HR | 45000 | 2024-02-12 |
| 3 | Aman | IT | 60000 | 2023-03-20 |
| 1 | Rahul | IT | 50000 | 2022-01-10 |

First sorts by department; within each department, sorts by salary from highest to lowest.

### Sorting by Column Position

```sql
SELECT emp_name, department, salary
FROM employees
ORDER BY 3 DESC;
```

`3` refers to the third selected column (`salary`). Using the column name is generally clearer.

### ORDER BY with Aggregation

```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC;
```
**output**
| department | average_salary |
|---|---:|
| IT | 55000.00 |
| Finance | 55000.00 |
| HR | 42500.00 |

Sorts departments by average salary, highest first.

---

# LIMIT and OFFSET

- `LIMIT` sets the maximum number of rows returned.
- `OFFSET` skips rows before returning results.

```sql
-- Return the three highest-paid employees
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```
**output**
| emp_id | emp_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 3 | Aman | IT | 60000 | 2023-03-20 |
| 4 | Neha | Finance | 55000 | 2022-08-05 |
| 1 | Rahul | IT | 50000 | 2022-01-10 |

```sql
-- Skip the first two and return the next three
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3 OFFSET 2;
```
**output**
| emp_id | emp_name | department | salary | hire_date |
|---:|---|---|---:|---|
| 1 | Rahul | IT | 50000 | 2022-01-10 |
| 5 | Karan | HR | 45000 | 2024-02-12 |
| 2 | Priya | HR | 40000 | 2021-06-15 |

### Pagination

Pagination displays a large result in smaller pages.

```sql
-- Page 1
SELECT * FROM employees ORDER BY emp_id LIMIT 10 OFFSET 0;

-- Page 2
SELECT * FROM employees ORDER BY emp_id LIMIT 10 OFFSET 10;

-- Page 3
SELECT * FROM employees ORDER BY emp_id LIMIT 10 OFFSET 20;
```

**Formula:**

```text
OFFSET = (Page Number - 1) × Page Size
```

For page 3 with 10 rows per page: `(3 - 1) × 10 = 20`.

`LIMIT` and `OFFSET` work in PostgreSQL and MySQL. Other databases may use different syntax.

---

#  CASE Expression

`CASE` adds conditional logic to a query. It is similar to `if-elif-else` in Python. SQL checks conditions from top to bottom and returns the result for the first true condition.

```sql
SELECT
    emp_name,
    salary,
    CASE
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 45000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```
**output**
| emp_name | salary | salary_category |
|---|---:|---|
| Rahul | 50000 | Medium |
| Priya | 40000 | Low |
| Aman | 60000 | High |
| Neha | 55000 | Medium |
| Karan | 45000 | Medium |

- Salary at least 60000 → `High`.
- Otherwise, salary at least 45000 → `Medium`.
- Otherwise → `Low`.

---

# Conditional Aggregation

Conditional aggregation applies an aggregate function only to rows that satisfy a condition. A common method is to put `CASE` inside an aggregate function.

```sql
SELECT
    department,
    COUNT(*) AS total_employees,
    SUM(CASE WHEN salary >= 50000 THEN 1 ELSE 0 END) AS high_salary_count,
    SUM(CASE WHEN salary < 50000 THEN 1 ELSE 0 END) AS low_salary_count
FROM employees
GROUP BY department;
```
**output**
| department | total_employees | high_salary_count | low_salary_count |
|---|---:|---:|---:|
| IT | 2 | 2 | 0 |
| HR | 2 | 0 | 2 |
| Finance | 1 | 1 | 0 |

For each row, `CASE` returns `1` when the condition is true and `0` otherwise. `SUM()` adds the 1s to produce a count.

### FILTER Clause (PostgreSQL)

PostgreSQL also supports `FILTER` for applying a condition to an individual aggregate:

```sql
SELECT
    department,
    COUNT(*) AS total_employees,
    COUNT(*) FILTER (WHERE salary >= 50000) AS high_salary_count,
    COUNT(*) FILTER (WHERE salary < 50000) AS low_salary_count
FROM employees
GROUP BY department;
```
**output**
| department | total_employees | high_salary_count | low_salary_count |
|---|---:|---:|---:|
| IT | 2 | 2 | 0 |
| HR | 2 | 0 | 2 |
| Finance | 1 | 1 | 0 |

`FILTER` is not supported by every database. The `CASE` method is more portable.

---

# DISTINCT Inside Aggregate Functions

`DISTINCT` inside an aggregate makes the function consider only unique values.

```sql
SELECT
    SUM(DISTINCT salary) AS unique_salary_total,
    AVG(DISTINCT salary) AS unique_salary_average,
    COUNT(DISTINCT department) AS unique_department_count
FROM employees;
```

For example, `SUM(DISTINCT salary)` adds each different salary only once.

---

#  GROUP BY with Expressions and Functions

`GROUP BY` can group by an expression or function, not just a column.

### Group by Joining Year

```sql
SELECT
    EXTRACT(YEAR FROM hire_date) AS joining_year,
    COUNT(*) AS employee_count
FROM employees
GROUP BY EXTRACT(YEAR FROM hire_date);
```

This groups employees by the year they joined.

### Group by Month (PostgreSQL)

```sql
SELECT
    DATE_TRUNC('month', hire_date) AS joining_month,
    COUNT(*) AS employee_count
FROM employees
GROUP BY DATE_TRUNC('month', hire_date)
ORDER BY joining_month;
```

`DATE_TRUNC('month', ...)` sets the day and smaller time parts to the start of that month. Date functions differ between database systems.

---

# Filtering with Subqueries

A subquery is a query inside another query. It can provide a value or set of rows used by the outer query.

### Employees Earning More Than the Average Salary

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query calculates the average salary. The outer query returns employees earning more than that average.

### EXISTS

`EXISTS` is true when its subquery returns at least one row.

```sql
SELECT d.department
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department = d.department
);
```
**output**
| department |
|---|
| IT |
| HR |
| Finance |

Returns departments that have at least one employee.

### NOT EXISTS

`NOT EXISTS` is true when its subquery returns no rows.

```sql
SELECT d.department
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department = d.department
);
```

Returns departments that have no employees.

---

#  Window Functions with Aggregations

Window functions calculate values across related rows while keeping each original row in the result.

Unlike `GROUP BY`, they do not collapse each group into one row.

### Department-Wise Average Salary

```sql
SELECT
    emp_name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_average
FROM employees;
```
**output**
| emp_name | department | salary | department_average |
|---|---|---:|---:|
| Rahul | IT | 50000 | 55000.00 |
| Priya | HR | 40000 | 42500.00 |
| Aman | IT | 60000 | 55000.00 |
| Neha | Finance | 55000 | 55000.00 |
| Karan | HR | 45000 | 42500.00 |


- `OVER()` makes the aggregate a window function.
- `PARTITION BY department` creates a separate calculation group for each department.
- Every employee remains in the output, with their department's average.

### GROUP BY vs Window Function

| GROUP BY | Window Function |
|---|---|
| Combines each group into a result row. | Keeps individual rows. |
| Usually returns one row per group. | Returns a value for each original row. |
| Uses aggregate functions. | Uses `OVER()` with aggregate or window functions. |

---

# Logical Order of SQL Query Execution

SQL is written in one order but logically processed in another.

Common logical order:

1. `FROM`
2. `JOIN` and `ON`
3. `WHERE`
4. `GROUP BY`
5. `HAVING`
6. `SELECT`
7. `DISTINCT`
8. `ORDER BY`
9. `LIMIT` / `OFFSET`

### Example

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary > 40000
GROUP BY department
HAVING AVG(salary) > 45000
ORDER BY average_salary DESC
LIMIT 2;
```

### How It Executes

1. **FROM:** Read rows from `employees`.
2. **WHERE:** Keep employees earning more than 40000.
3. **GROUP BY:** Group the remaining rows by department.
4. **HAVING:** Keep groups whose average salary is greater than 45000.
5. **SELECT:** Calculate and display department and average salary.
6. **ORDER BY:** Sort by average salary, highest first.
7. **LIMIT:** Return only the first two rows.

Understanding this order explains why aggregate functions generally cannot be used directly in `WHERE`: filtering happens before groups and aggregate values are calculated.
