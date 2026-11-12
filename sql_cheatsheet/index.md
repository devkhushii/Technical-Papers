# Indexes
---

An index is a database object that helps retrieve records faster without scanning the entire table.

It works like the index of a book: instead of reading every page to find a topic, we use the index to locate it directly.

**Example:** Suppose we have an Employees table containing thousands of records. If we frequently search for an employee using `emp_id`, an index on `emp_id` can make the search faster.

##  Sample Data

| emp_id | emp_name | department | salary |
|---|---|---|---:|
| 101 | Rahul | CSE | 50000 |
| 102 | Priya | HR | 45000 |
| 103 | Aman | CSE | 60000 |
| 104 | Neha | IT | 55000 |
| 105 | Ravi | HR | 40000 |

SQL:

```sql
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(30),
    salary INT
);
```

##  Why Do We Need Indexes?

Without an index, the database may need to check every row to find matching records.

This is called a **Full Table Scan**.

Example:

```sql
SELECT *
FROM Employees
WHERE emp_name = 'Priya';
```

The database may examine every row until it finds Priya.

With an index on `emp_name`, the database can locate matching records more efficiently.

**Important:** An index improves data retrieval, but it requires additional storage and maintenance.

##  How Does an Index Work?

An index stores search-key values along with references to the corresponding table rows.

Instead of scanning the entire table, the database can search through the index and locate the required rows.

Most relational databases commonly use **B-Tree or B+ Tree structures** for indexing.

### B-Tree

A B-Tree is a balanced search tree.

- Values are stored in sorted order.
- Searching follows the tree structure.
- It keeps the tree balanced.
- Searching, insertion, and deletion are efficient.

### B+ Tree

A B+ Tree is commonly used for database indexes.

- Internal nodes store search keys.
- Leaf nodes contain indexed values and row references.
- Leaf nodes are linked, making range searches efficient.

**Example:** Finding employees with salaries between 40,000 and 55,000 can benefit from an ordered index on salary.

##  Creating an Index

Syntax:

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

Example:

```sql
CREATE INDEX idx_emp_name
ON Employees(emp_name);
```

Now we can search using:

```sql
SELECT *
FROM Employees
WHERE emp_name = 'Priya';
```

The database may use the index to retrieve the matching record.

**Note:** Creating an index does not guarantee that the database will use it. The query optimizer decides whether it is beneficial.

##  Types of Indexes

### 1. Single-Column Index

An index created on one column.

```sql
CREATE INDEX idx_salary
ON Employees(salary);
```

Useful when queries frequently search or sort using salary.

### 2. Composite Index

An index created on two or more columns.

```sql
CREATE INDEX idx_dept_salary
ON Employees(department, salary);
```

It can help queries such as:

```sql
SELECT *
FROM Employees
WHERE department = 'CSE'
AND salary > 50000;
```

**Important: Column Order Matters**

For an index on `(department, salary)`:

- Searching by department can use the index.
- Searching by department and salary can use the index.
- Searching only by salary may not efficiently use the index.

This is called the **Leftmost Prefix Rule**.

### 3. Unique Index

A unique index ensures that indexed values cannot be duplicated.

```sql
CREATE UNIQUE INDEX idx_emp_name_unique
ON Employees(emp_name);
```

This prevents duplicate employee names.

**Note:** In practice, employee names are usually not unique. A unique index should be created only when uniqueness is a real requirement.

### 4. Clustered Index

A clustered index determines how table records are physically organized according to the indexed key.

- A table generally has only one clustered organization.
- It is useful for range-based retrieval.
- The exact implementation depends on the database.

For example, in SQL Server, a primary key commonly creates a clustered index by default unless configured otherwise.

**Important:** PostgreSQL does not maintain a clustered index automatically. Its `CLUSTER` command physically reorganizes a table once using an index, but later updates do not automatically preserve that order.

### 5. Non-Clustered Index

A non-clustered index is stored separately from the table data and contains references to the corresponding rows.

- Multiple non-clustered indexes can exist.
- It helps retrieve records without scanning the entire table.
- It requires additional storage.

### 6. Primary Key Index

A primary key uniquely identifies each row.

```sql
CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(30),
    salary INT
);
```

Most relational databases automatically create an index to enforce the primary key.

### 7. Partial Index

A partial index contains only rows that satisfy a specified condition.

Example (PostgreSQL):

```sql
CREATE INDEX idx_cse_salary
ON Employees(salary)
WHERE department = 'CSE';
```

This index contains only CSE employee records.

It can help queries that use the matching condition.

### 8. Covering Index

A covering index contains all the columns required by a query.

Example:

```sql
CREATE INDEX idx_dept_salary_name
ON Employees(department, salary, emp_name);
```

Query:

```sql
SELECT emp_name, salary
FROM Employees
WHERE department = 'CSE';
```

The database may retrieve the required information directly from the index without accessing the table.

The exact behavior depends on the database engine and query plan.

##  Unique Index vs Non-Unique Index

| Unique Index | Non-Unique Index |
|---|---|
| Does not allow duplicate indexed values | Allows duplicate indexed values |
| Enforces uniqueness | Does not enforce uniqueness |
| Useful for unique identifiers | Useful for frequently searched columns |

##  Clustered vs Non-Clustered Index

| Clustered Index | Non-Clustered Index |
|---|---|
| Determines table data organization | Stored separately from table data |
| Generally one clustered organization per table | Multiple indexes can exist |
| Useful for range queries | Useful for different search conditions |
| Leaf-level data organization depends on the database | Contains indexed keys and row references |

##  Indexing and Query Performance

Indexes can improve queries involving:

- `WHERE`
- `JOIN`
- `ORDER BY`
- `GROUP BY`
- Range conditions such as `BETWEEN`

Example:

```sql
SELECT *
FROM Employees
WHERE salary BETWEEN 40000 AND 55000
ORDER BY salary;
```

An index on salary may help the database retrieve and sort the matching records efficiently.

However, the optimizer may choose a different execution plan if a table scan is cheaper.

##  How to Check Whether an Index Is Used

Use `EXPLAIN` to inspect the query execution plan.

PostgreSQL example:

```sql
EXPLAIN
SELECT *
FROM Employees
WHERE emp_name = 'Priya';
```

Common plan terms:

- **Seq Scan:** Reads table rows sequentially.
- **Index Scan:** Uses an index to find matching rows.
- **Index Only Scan:** Retrieves required values from the index when possible.
- **Bitmap Index Scan:** Uses an index to identify matching row locations, often followed by a bitmap heap scan.

##  Deleting an Index

Syntax:

```sql
DROP INDEX index_name;
```

Example (PostgreSQL):

```sql
DROP INDEX idx_emp_name;
```

This removes the index but does not delete the table data.

##  Advantages of Indexes

- Faster data retrieval.
- Improves search performance.
- Can improve joins and sorting.
- Helps with range queries.
- Can enforce uniqueness.
- Reduces unnecessary table scanning.

##  Disadvantages of Indexes

- Requires additional storage.
- Slows down INSERT operations because indexes must be updated.
- Slows down DELETE operations because index entries must be removed.
- Can slow down UPDATE operations when indexed columns change.
- Too many indexes increase maintenance overhead.

##  When Should We Create an Index?

Create indexes on columns that are frequently used in:

- Search conditions.
- Join conditions.
- Sorting.
- Grouping.
- Unique constraints.

Avoid unnecessary indexes on:

- Columns that are rarely searched.
- Very small tables where scanning is cheaper.
- Columns with frequent updates when the performance benefit is low.

**Important:** Low-cardinality columns, such as a column containing only a few distinct values, may not always benefit from a normal index. The decision depends on data distribution and query patterns.
