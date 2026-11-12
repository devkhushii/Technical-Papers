# Normalization

Normalization is the process of organizing data in database tables to:

- Reduce duplicate data.
- Avoid data inconsistencies.
- Make inserting, updating, and deleting data easier.
- Maintain data accuracy.

**Example:** Suppose a college stores student details and course details in one table. If a student enrolls in multiple courses, the student's name and department may be repeated.

Normalization helps organize this data into separate related tables.

##  Sample Data

### Student_Course Table

| Student_ID | Student_Name | Department | Course_ID | Course_Name | Instructor |
|---|---|---|---|---|---|
| 1 | Rahul | CSE | C101 | DBMS | Amit |
| 1 | Rahul | CSE | C102 | Python | Neha |
| 2 | Priya | ECE | C101 | DBMS | Amit |
| 3 | Aman | CSE | C103 | Java | Ravi |

Notice that Rahul's details are repeated because he is enrolled in two courses.

This creates unnecessary duplication.

##  Problems Without Normalization

There are three common problems called **database anomalies**.

### 1. Insertion Anomaly

An insertion anomaly occurs when we cannot insert certain information without inserting some unrelated information.

**Example:** We want to add a new course, C104, but no student has enrolled in it yet.

In the original table, we may not be able to store the course details without providing a Student_ID.

### 2. Update Anomaly

An update anomaly occurs when the same information is stored in multiple rows and must be updated everywhere.

**Example:** If Rahul changes his department, we must update every row containing Rahul's details.

If we update only one row, the database becomes inconsistent.

### 3. Deletion Anomaly

A deletion anomaly occurs when deleting one record accidentally removes other important information.

**Example:** If Aman is the only student enrolled in Java and we delete his record, we also lose the information about the Java course and its instructor.


## Functional Dependency

Functional dependency describes the relationship between columns in a table.

It is written as:

`A → B`

It means that the value of column A uniquely determines the value of column B.

Using our sample data:

- `Student_ID → Student_Name, Department`
- `Course_ID → Course_Name, Instructor`

This means:
- A Student_ID identifies one student and their department.
- A Course_ID identifies one course and its instructor.

### Types of Functional Dependency

**1. Full Functional Dependency**

A column depends on the complete candidate key, not just part of it.

**2. Partial Functional Dependency**

A non-key column depends on only part of a composite candidate key.

**3. Transitive Functional Dependency**

A non-key column depends on another non-key column.

Example:

`Student_ID → Department`

If the department also determines the department head:

`Department → Department_Head`

Then:

`Student_ID → Department_Head`

This is a transitive dependency.

##  Keys Used in Normalization

Keys help identify records and establish relationships between tables.

- **Primary Key:** Uniquely identifies each row.
- **Candidate Key:** A minimal set of columns that can uniquely identify a row.
- **Composite Key:** A key made using two or more columns.
- **Foreign Key:** A column that references a key in another table.
- **Super Key:** Any set of columns that uniquely identifies a row.

In our sample table, assuming each student can enroll in a course only once:

`(Student_ID, Course_ID)`

is the composite primary key.

Neither Student_ID nor Course_ID alone uniquely identifies every row.

##  First Normal Form (1NF)

A table is in First Normal Form when:

1. Every column contains atomic (single) values.
2. There are no multiple values in one cell.
3. Each row can be uniquely identified.

**Example of a table violating 1NF:**

| Student_ID | Student_Name | Courses |
|---|---|---|
| 1 | Rahul | DBMS, Python |
| 2 | Priya | DBMS |

The Courses column contains multiple values.

**After converting into 1NF:**

| Student_ID | Student_Name | Course_ID | Course_Name | Instructor |
|---|---|---|---|---|
| 1 | Rahul | C101 | DBMS | Amit |
| 1 | Rahul | C102 | Python | Neha |
| 2 | Priya | C101 | DBMS | Amit |
| 3 | Aman | C103 | Java | Ravi |

Now every cell contains a single value.

Our original sample table is already in 1NF.

##  Second Normal Form (2NF)

A table is in Second Normal Form when:

1. It is already in 1NF.
2. It has no partial functional dependency.

In simple words, every non-key column must depend on the complete candidate key.

Our composite key is:

`(Student_ID, Course_ID)`

But:

- Student_Name depends only on Student_ID.
- Department depends only on Student_ID.
- Course_Name depends only on Course_ID.
- Instructor depends only on Course_ID.

These are partial dependencies.

Therefore, the table is not in 2NF.

### Conversion into 2NF

Divide the table into three tables.

**Student Table**

| Student_ID | Student_Name | Department |
|---|---|---|
| 1 | Rahul | CSE |
| 2 | Priya | ECE |
| 3 | Aman | CSE |

**Course Table**

| Course_ID | Course_Name | Instructor |
|---|---|---|
| C101 | DBMS | Amit |
| C102 | Python | Neha |
| C103 | Java | Ravi |

**Enrollment Table**

| Student_ID | Course_ID |
|---|---|
| 1 | C101 |
| 1 | C102 |
| 2 | C101 |
| 3 | C103 |

Now student details depend on Student_ID, course details depend on Course_ID, and enrollment depends on the combination of both.

The tables are in 2NF, assuming the stated dependencies.

##  Third Normal Form (3NF)

A table is in Third Normal Form when:

1. It is already in 2NF.
2. It has no transitive dependency of non-key attributes on a candidate key.

In simple words, non-key columns should depend directly on the key, not on another non-key column.

For example, suppose our Student table also contains Department_Head.

| Student_ID | Student_Name | Department | Department_Head |
|---|---|---|---|
| 1 | Rahul | CSE | Amit |
| 2 | Priya | ECE | Neha |
| 3 | Aman | CSE | Amit |

Dependencies:

`Student_ID → Department`

`Department → Department_Head`

Department_Head depends on Department, not directly on the student key. This is a transitive dependency.

### Conversion into 3NF

Divide the data into two tables.

**Student Table**

| Student_ID | Student_Name | Department |
|---|---|---|
| 1 | Rahul | CSE |
| 2 | Priya | ECE |
| 3 | Aman | CSE |

**Department Table**

| Department | Department_Head |
|---|---|
| CSE | Amit |
| ECE | Neha |

Now department details are stored separately.

##  Boyce-Codd Normal Form (BCNF)

BCNF is a stronger version of 3NF.

A table is in BCNF when:

**For every non-trivial functional dependency X → Y, X must be a super key.**

In simple words, every determinant must be a super key.

A determinant is the column or set of columns that determines another column.

### Difference Between 3NF and BCNF

3NF allows a functional dependency if the right-hand-side attribute is a prime attribute (part of some candidate key), even when the determinant is not a super key.

BCNF does not allow this exception.

Therefore, every BCNF table is in 3NF, but every 3NF table is not necessarily in BCNF.

##  Fourth Normal Form (4NF)

A table is in Fourth Normal Form when:

1. It is already in BCNF.
2. It has no non-trivial multivalued dependency unless its determinant is a super key.

A multivalued dependency occurs when one attribute independently determines multiple values of another attribute.

For example, suppose a student can have multiple skills and multiple hobbies, and these are independent.

| Student_ID | Skill | Hobby |
|---|---|---|
| 1 | Python | Reading |
| 1 | Python | Cricket |
| 1 | Java | Reading |
| 1 | Java | Cricket |

The combinations create unnecessary rows.

### Conversion into 4NF

Separate the independent information.

**Student_Skill**

| Student_ID | Skill |
|---|---|
| 1 | Python |
| 1 | Java |

**Student_Hobby**

| Student_ID | Hobby |
|---|---|
| 1 | Reading |
| 1 | Cricket |

This removes the independent multivalued dependencies.

##  Fifth Normal Form (5NF)

Fifth Normal Form is also called Project-Join Normal Form (PJNF).

A table is in 5NF when:

1. It is already in 4NF.
2. It cannot be further decomposed into smaller tables without losing information.
3. Every non-trivial join dependency is implied by the candidate keys.

In simple words, a table should not contain unnecessary join dependencies that can be removed by decomposing it into smaller tables.

5NF is mainly useful in complex databases where relationships involve three or more entities.

##  Decomposition

Decomposition means dividing one large table into smaller tables to reduce duplication and improve data organization.

For example, we divided Student_Course into:

- Student
- Course
- Enrollment

### Types of Decomposition

**1. Lossless Decomposition**

A decomposition is lossless when joining the smaller tables gives exactly the original data without losing or adding incorrect rows.

**2. Lossy Decomposition**

A decomposition is lossy when joining the smaller tables may produce incorrect or extra rows, or fail to reproduce the original data.

A good normalization process aims for lossless decomposition.

### Dependency Preservation

A decomposition is dependency-preserving when all functional dependencies can be checked using the individual tables without needing to join them.

It is desirable because it makes constraint checking easier.

##  Denormalization

Denormalization is the process of intentionally adding some redundant data to improve read performance.

It is sometimes used in reporting and analytics systems.

**Example:** Instead of joining Student, Enrollment, and Course every time, a reporting table may store student and course names together.

**Advantages:**
- Faster read queries in some cases.
- Fewer joins.
- Useful for reporting systems.

**Disadvantages:**
- Duplicate data.
- More storage.
- Updates become harder.
- Risk of inconsistent data.

**Remember:** Normalization reduces redundancy, while denormalization intentionally introduces some redundancy for performance.

##  Normalization Using SQL

We can create the normalized tables using SQL.

```sql
CREATE TABLE Student (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    department VARCHAR(30)
);

CREATE TABLE Course (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(50),
    instructor VARCHAR(50)
);

CREATE TABLE Enrollment (
    student_id INT,
    course_id VARCHAR(10),
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES Student(student_id),
    FOREIGN KEY (course_id) REFERENCES Course(course_id)
);
```

Insert sample data:

```sql
INSERT INTO Student VALUES
(1, 'Rahul', 'CSE'),
(2, 'Priya', 'ECE'),
(3, 'Aman', 'CSE');

INSERT INTO Course VALUES
('C101', 'DBMS', 'Amit'),
('C102', 'Python', 'Neha'),
('C103', 'Java', 'Ravi');

INSERT INTO Enrollment VALUES
(1, 'C101'),
(1, 'C102'),
(2, 'C101'),
(3, 'C103');
```

The data is now stored in separate related tables.

## Advantages of Normalization

- Reduces duplicate data.
- Prevents insertion, update, and deletion anomalies.
- Improves data consistency.
- Makes database maintenance easier.
- Organizes data into meaningful tables.

## Disadvantages of Normalization

- More tables are created.
- Queries may require more joins.
- Complex queries can become slower.
- Database design requires careful planning.
