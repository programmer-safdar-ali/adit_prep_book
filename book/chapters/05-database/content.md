# Chapter 5: Database Management Systems

---

## Chapter Overview

- **Domain**: Database Management and Data Administration
- **Estimated Study Time**: 6-7 hours
- **Prerequisites**: Chapter 4 (Server Administration), Basic data concepts
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Define** relational database concepts including ACID properties and entity-relationship models (B)
2. **Explain** database normalization forms and their importance for data integrity (B)
3. **Write** SQL queries using SELECT, JOIN, subqueries, and aggregate functions (I)
4. **Implement** database security through user management, roles, and privileges (I)
5. **Analyze** query performance and **apply** optimization techniques including indexing (A)
6. **Compare** relational and NoSQL databases and **evaluate** their appropriate use cases (A)
7. **Design** database backup strategies including replication and point-in-time recovery (E)
8. **Assess** data warehousing architectures and **propose** solutions for analytical workloads (E)

---

## Introduction

Database management systems (DBMS) are the foundation of modern information systems, storing and managing the data that powers government operations, business applications, and decision-making processes. As an Assistant Director IT, you will oversee database infrastructure, evaluate database technologies, ensure data security and compliance, and guide database administration staff.

Understanding database concepts is essential for effective IT leadership. Whether you're evaluating vendor proposals, planning capacity, ensuring disaster recovery capabilities, or implementing security controls, database knowledge enables informed decision-making.

This chapter covers relational database fundamentals, SQL proficiency, database administration, and modern database technologies. These concepts connect directly to data structures (Chapter 6), cloud computing (Chapter 9), and big data technologies (Chapter 13).

---

## Section 5.1: Relational Database Concepts (B)

Relational databases organize data into tables with relationships between them, providing a structured and consistent approach to data management.

### 5.1.1 ACID Properties

ACID properties ensure reliable database transactions:

**Atomicity**:
- Transactions are "all or nothing"
- Either all operations complete successfully, or none do
- If any part fails, the entire transaction is rolled back
- Example: Bank transfer must debit one account AND credit another, or neither

**Consistency**:
- Database moves from one valid state to another
- All rules, constraints, and triggers are enforced
- Data integrity is maintained
- Example: Foreign key constraints prevent orphaned records

**Isolation**:
- Concurrent transactions don't interfere with each other
- Each transaction sees a consistent view of data
- Isolation levels: Read Uncommitted, Read Committed, Repeatable Read, Serializable
- Example: Two users updating the same record don't see partial updates

**Durability**:
- Committed transactions are permanent
- Survive system crashes and power failures
- Typically implemented via transaction logs
- Example: Once "commit" returns success, data is safely stored

### 5.1.2 Entity-Relationship (ER) Diagrams

ER diagrams visually represent database structure:

**Components**:
- **Entities**: Objects or concepts (tables)
- **Attributes**: Properties of entities (columns)
- **Relationships**: Connections between entities
- **Cardinality**: Number of instances in relationships

**Cardinality Types**:
| Type | Description | Example |
|------|-------------|---------|
| 1:1 | One-to-one | Person → Passport |
| 1:N | One-to-many | Department → Employees |
| M:N | Many-to-many | Students ↔ Courses |

### Practical Example 5.1: ER Diagram for HR System

**Scenario**: Design ER diagram for an HR database.

**Entities and Relationships**:
```
[DEPARTMENT] 1────────N [EMPLOYEE] N────────M [PROJECT]
     │                       │                    │
     │                       │                    │
     └── dept_id (PK)        ├── emp_id (PK)      ├── project_id (PK)
         dept_name           ├── first_name       ├── project_name
         location            ├── last_name        ├── start_date
                             ├── email            └── end_date
                             ├── hire_date
                             ├── salary
                             └── dept_id (FK)

[EMPLOYEE_PROJECT] (Junction Table for M:N)
     ├── emp_id (FK)
     ├── project_id (FK)
     └── role
```

### 5.1.3 Functional Dependencies

A functional dependency exists when one attribute determines another:

**Notation**: X → Y (X determines Y)

**Example**:
- emp_id → emp_name (employee ID determines employee name)
- dept_id → dept_name (department ID determines department name)

Understanding functional dependencies is essential for normalization.

---

## Section 5.2: Database Normalization (B)

Normalization reduces data redundancy and improves data integrity through a series of progressive forms.

### 5.2.1 First Normal Form (1NF)

**Requirements**:
- Atomic values (no repeating groups or arrays)
- Each column contains only one value
- Each row is unique (has a primary key)

**Before 1NF**:
| OrderID | Customer | Products |
|---------|----------|----------|
| 1 | John Smith | Laptop, Mouse, Keyboard |

**After 1NF**:
| OrderID | Customer | Product |
|---------|----------|---------|
| 1 | John Smith | Laptop |
| 1 | John Smith | Mouse |
| 1 | John Smith | Keyboard |

### 5.2.2 Second Normal Form (2NF)

**Requirements**:
- Must be in 1NF
- No partial dependencies (all non-key attributes depend on the entire primary key)

**Before 2NF** (composite key: OrderID, ProductID):
| OrderID | ProductID | ProductName | Quantity |
|---------|-----------|-------------|----------|
| 1 | 101 | Laptop | 1 |
| 1 | 102 | Mouse | 2 |

*Problem*: ProductName depends only on ProductID, not the full key

**After 2NF**:

Order_Items:
| OrderID | ProductID | Quantity |
|---------|-----------|----------|
| 1 | 101 | 1 |
| 1 | 102 | 2 |

Products:
| ProductID | ProductName |
|-----------|-------------|
| 101 | Laptop |
| 102 | Mouse |

### 5.2.3 Third Normal Form (3NF)

**Requirements**:
- Must be in 2NF
- No transitive dependencies (non-key attributes don't depend on other non-key attributes)

**Before 3NF**:
| EmpID | EmpName | DeptID | DeptName | DeptLocation |
|-------|---------|--------|----------|--------------|
| 1 | John | 10 | IT | Building A |

*Problem*: DeptName and DeptLocation depend on DeptID, not EmpID

**After 3NF**:

Employees:
| EmpID | EmpName | DeptID |
|-------|---------|--------|
| 1 | John | 10 |

Departments:
| DeptID | DeptName | DeptLocation |
|--------|----------|--------------|
| 10 | IT | Building A |

### 5.2.4 Boyce-Codd Normal Form (BCNF)

**Requirements**:
- Must be in 3NF
- Every determinant must be a candidate key
- Addresses anomalies when multiple candidate keys exist

### 5.2.5 Fourth and Fifth Normal Forms (4NF, 5NF)

**4NF**: Eliminates multi-valued dependencies
**5NF**: Eliminates join dependencies

These higher forms are rarely needed in practice but important for exam knowledge.

### Practical Example 5.2: Normalization Exercise

**Scenario**: Normalize the following table to 3NF.

**Unnormalized Table**:
| StudentID | StudentName | Courses | InstructorName | InstructorPhone |
|-----------|-------------|---------|----------------|-----------------|
| 101 | Alice | Math, Physics | Dr. Smith | 555-1234 |
| 102 | Bob | Math | Dr. Smith | 555-1234 |

**Step 1 - 1NF** (eliminate repeating groups):

| StudentID | StudentName | Course | InstructorName | InstructorPhone |
|-----------|-------------|--------|----------------|-----------------|
| 101 | Alice | Math | Dr. Smith | 555-1234 |
| 101 | Alice | Physics | Dr. Johnson | 555-5678 |
| 102 | Bob | Math | Dr. Smith | 555-1234 |

**Step 2 - 2NF** (remove partial dependencies):

Students:
| StudentID | StudentName |
|-----------|-------------|

Enrollments:
| StudentID | CourseID |

Courses:
| CourseID | CourseName | InstructorName | InstructorPhone |

**Step 3 - 3NF** (remove transitive dependencies):

Instructors:
| InstructorID | InstructorName | InstructorPhone |

Courses:
| CourseID | CourseName | InstructorID |

### 5.2.6 Denormalization

Sometimes denormalization improves performance by reducing joins:

**When to Denormalize**:
- Frequently accessed read-heavy data
- Reporting and analytics workloads
- When join performance is unacceptable
- Data warehousing scenarios

**Trade-offs**:
- Faster reads vs. slower writes
- Storage increase
- Risk of data inconsistency
- More complex update logic

---

## Section 5.3: SQL Queries (I)

Structured Query Language (SQL) is the standard language for interacting with relational databases.

### 5.3.1 SELECT Statements

**Basic SELECT**:
```sql
-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT first_name, last_name, salary FROM employees;

-- With alias
SELECT first_name AS "First Name", salary * 12 AS "Annual Salary"
FROM employees;

-- Distinct values
SELECT DISTINCT department_id FROM employees;
```

**WHERE Clause**:
```sql
-- Comparison operators
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees WHERE hire_date >= '2024-01-01';

-- Logical operators
SELECT * FROM employees WHERE department_id = 10 AND salary > 60000;
SELECT * FROM employees WHERE department_id = 10 OR department_id = 20;

-- IN operator
SELECT * FROM employees WHERE department_id IN (10, 20, 30);

-- BETWEEN
SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;

-- LIKE (pattern matching)
SELECT * FROM employees WHERE last_name LIKE 'Smith%';  -- Starts with
SELECT * FROM employees WHERE email LIKE '%@gov.pk';    -- Ends with
SELECT * FROM employees WHERE last_name LIKE '_mith';   -- Single character wildcard

-- NULL handling
SELECT * FROM employees WHERE manager_id IS NULL;
SELECT * FROM employees WHERE commission IS NOT NULL;
```

**ORDER BY**:
```sql
-- Ascending (default)
SELECT * FROM employees ORDER BY last_name;

-- Descending
SELECT * FROM employees ORDER BY salary DESC;

-- Multiple columns
SELECT * FROM employees ORDER BY department_id, salary DESC;
```

### 5.3.2 JOIN Operations

**INNER JOIN** (matching rows only):
```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id;
```

**LEFT JOIN** (all left table rows, matching right):
```sql
SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

**RIGHT JOIN** (all right table rows, matching left):
```sql
SELECT e.first_name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.department_id;
```

**FULL OUTER JOIN** (all rows from both tables):
```sql
SELECT e.first_name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.department_id = d.department_id;
```

**CROSS JOIN** (Cartesian product):
```sql
SELECT e.first_name, p.project_name
FROM employees e
CROSS JOIN projects p;
```

**SELF JOIN** (table joined with itself):
```sql
SELECT e.first_name AS Employee, m.first_name AS Manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.employee_id;
```

### Practical Example 5.3: Complex JOIN Query

**Scenario**: List all employees with their department name, manager name, and project assignments.

```sql
SELECT
    e.employee_id,
    e.first_name || ' ' || e.last_name AS employee_name,
    d.department_name,
    m.first_name || ' ' || m.last_name AS manager_name,
    p.project_name,
    ep.role
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
LEFT JOIN employees m ON e.manager_id = m.employee_id
LEFT JOIN employee_projects ep ON e.employee_id = ep.employee_id
LEFT JOIN projects p ON ep.project_id = p.project_id
ORDER BY d.department_name, e.last_name;
```

### 5.3.3 Aggregate Functions

**Common Aggregates**:
```sql
-- COUNT
SELECT COUNT(*) FROM employees;  -- Total rows
SELECT COUNT(DISTINCT department_id) FROM employees;  -- Distinct departments

-- SUM, AVG
SELECT SUM(salary) AS total_payroll FROM employees;
SELECT AVG(salary) AS average_salary FROM employees;

-- MIN, MAX
SELECT MIN(salary), MAX(salary) FROM employees;
SELECT MIN(hire_date) AS earliest_hire FROM employees;
```

**GROUP BY**:
```sql
-- Aggregate by group
SELECT department_id, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;

-- Multiple grouping columns
SELECT department_id, job_title, COUNT(*) AS count
FROM employees
GROUP BY department_id, job_title;
```

**HAVING** (filter aggregated results):
```sql
-- Departments with more than 5 employees
SELECT department_id, COUNT(*) AS emp_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;

-- Departments with average salary over 50000
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

### 5.3.4 Subqueries

**Scalar Subquery** (returns single value):
```sql
SELECT first_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Table Subquery** (returns multiple values):
```sql
SELECT first_name, department_id
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Islamabad'
);
```

**Correlated Subquery** (references outer query):
```sql
SELECT e.first_name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

### 5.3.5 Window Functions

Window functions perform calculations across related rows:

```sql
-- ROW_NUMBER
SELECT
    first_name,
    department_id,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank_in_dept
FROM employees;

-- RANK (with gaps for ties)
SELECT
    first_name,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;

-- DENSE_RANK (no gaps for ties)
SELECT
    first_name,
    salary,
    DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;

-- Running total
SELECT
    hire_date,
    first_name,
    salary,
    SUM(salary) OVER (ORDER BY hire_date) AS running_total
FROM employees;

-- Moving average
SELECT
    hire_date,
    salary,
    AVG(salary) OVER (ORDER BY hire_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM employees;
```

### 5.3.6 Common Table Expressions (CTEs)

CTEs provide named temporary result sets:

```sql
-- Basic CTE
WITH high_earners AS (
    SELECT employee_id, first_name, salary
    FROM employees
    WHERE salary > 70000
)
SELECT * FROM high_earners WHERE first_name LIKE 'A%';

-- Multiple CTEs
WITH
dept_stats AS (
    SELECT department_id, AVG(salary) AS avg_salary, COUNT(*) AS emp_count
    FROM employees
    GROUP BY department_id
),
large_depts AS (
    SELECT department_id, avg_salary
    FROM dept_stats
    WHERE emp_count > 10
)
SELECT d.department_name, ld.avg_salary
FROM large_depts ld
JOIN departments d ON ld.department_id = d.department_id;
```

### Practical Example 5.4: Complex Report Query

**Scenario**: Generate a salary report showing each employee's salary compared to department and company averages.

```sql
WITH
company_avg AS (
    SELECT AVG(salary) AS avg_salary FROM employees
),
dept_avg AS (
    SELECT department_id, AVG(salary) AS dept_avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT
    e.first_name,
    e.last_name,
    d.department_name,
    e.salary,
    da.dept_avg_salary,
    ca.avg_salary AS company_avg_salary,
    ROUND((e.salary - da.dept_avg_salary) / da.dept_avg_salary * 100, 2) AS pct_vs_dept,
    ROUND((e.salary - ca.avg_salary) / ca.avg_salary * 100, 2) AS pct_vs_company
FROM employees e
JOIN departments d ON e.department_id = d.department_id
JOIN dept_avg da ON e.department_id = da.department_id
CROSS JOIN company_avg ca
ORDER BY d.department_name, e.salary DESC;
```

---

## Section 5.4: Database Administration (I)

Database administration encompasses user management, security, backup, and performance tuning.

### 5.4.1 User Management

**Creating Users**:
```sql
-- MySQL
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'SecurePassword123!';
CREATE USER 'appuser'@'%' IDENTIFIED BY 'SecurePassword123!';  -- Any host

-- PostgreSQL
CREATE USER appuser WITH PASSWORD 'SecurePassword123!';
CREATE ROLE appuser WITH LOGIN PASSWORD 'SecurePassword123!';

-- SQL Server
CREATE LOGIN appuser WITH PASSWORD = 'SecurePassword123!';
CREATE USER appuser FOR LOGIN appuser;

-- Oracle
CREATE USER appuser IDENTIFIED BY SecurePassword123;
```

### 5.4.2 Roles and Privileges

**GRANT Permissions**:
```sql
-- Grant specific privileges
GRANT SELECT, INSERT, UPDATE ON employees TO appuser;
GRANT SELECT ON departments TO appuser;

-- Grant all privileges on table
GRANT ALL PRIVILEGES ON employees TO appuser;

-- Grant with ability to grant to others
GRANT SELECT ON employees TO appuser WITH GRANT OPTION;

-- Grant role membership
GRANT db_datareader TO appuser;  -- SQL Server
GRANT readonly TO appuser;       -- PostgreSQL
```

**REVOKE Permissions**:
```sql
REVOKE UPDATE ON employees FROM appuser;
REVOKE ALL PRIVILEGES ON employees FROM appuser;
```

**Creating Roles**:
```sql
-- PostgreSQL
CREATE ROLE readonly;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly;
GRANT readonly TO appuser;

-- SQL Server
CREATE ROLE reporting;
GRANT SELECT ON SCHEMA::dbo TO reporting;
ALTER ROLE reporting ADD MEMBER appuser;
```

### Practical Example 5.5: Role-Based Access Control

**Scenario**: Implement RBAC for an HR application.

**Roles and Permissions**:

| Role | Tables | Permissions |
|------|--------|-------------|
| hr_viewer | employees, departments | SELECT |
| hr_editor | employees | SELECT, INSERT, UPDATE |
| hr_admin | employees, departments, salaries | ALL |
| payroll | salaries, employees | SELECT, UPDATE (salary columns) |

**Implementation** (PostgreSQL):
```sql
-- Create roles
CREATE ROLE hr_viewer;
CREATE ROLE hr_editor;
CREATE ROLE hr_admin;
CREATE ROLE payroll;

-- Assign permissions
GRANT SELECT ON employees, departments TO hr_viewer;

GRANT SELECT, INSERT, UPDATE ON employees TO hr_editor;
GRANT USAGE, SELECT ON SEQUENCE employees_id_seq TO hr_editor;

GRANT ALL ON employees, departments, salaries TO hr_admin;
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO hr_admin;

GRANT SELECT ON employees, salaries TO payroll;
GRANT UPDATE (salary, bonus) ON employees TO payroll;

-- Create users and assign roles
CREATE USER viewer1 WITH PASSWORD 'password1';
CREATE USER editor1 WITH PASSWORD 'password2';
CREATE USER admin1 WITH PASSWORD 'password3';

GRANT hr_viewer TO viewer1;
GRANT hr_editor TO editor1;
GRANT hr_admin TO admin1;
```

### 5.4.3 Backup Strategies

**Backup Types**:

| Type | Description | Use Case |
|------|-------------|----------|
| Full | Complete database copy | Baseline, disaster recovery |
| Differential | Changes since last full backup | Faster than full, simpler restore |
| Incremental/Log | Transaction log backup | Point-in-time recovery |

**MySQL Backup**:
```bash
# Full backup with mysqldump
mysqldump -u root -p --all-databases > full_backup.sql
mysqldump -u root -p mydb > mydb_backup.sql

# Binary backup with mysqlpump (parallel)
mysqlpump -u root -p --all-databases > full_backup.sql

# Physical backup with Percona XtraBackup
xtrabackup --backup --target-dir=/backup/full
```

**PostgreSQL Backup**:
```bash
# Logical backup
pg_dump -U postgres mydb > mydb_backup.sql
pg_dumpall -U postgres > all_databases.sql

# Physical backup (base backup)
pg_basebackup -U postgres -D /backup/full -Fp -Xs -P

# Point-in-time recovery requires WAL archiving
```

**SQL Server Backup**:
```sql
-- Full backup
BACKUP DATABASE MyDB TO DISK = 'C:\Backup\MyDB_Full.bak';

-- Differential backup
BACKUP DATABASE MyDB TO DISK = 'C:\Backup\MyDB_Diff.bak' WITH DIFFERENTIAL;

-- Transaction log backup
BACKUP LOG MyDB TO DISK = 'C:\Backup\MyDB_Log.trn';
```

### 5.4.4 Point-in-Time Recovery

Point-in-time recovery (PITR) restores a database to a specific moment:

**PostgreSQL PITR**:
1. Configure WAL archiving (`archive_mode = on`)
2. Take base backup
3. Archive WAL files continuously
4. For recovery:
   - Restore base backup
   - Configure `recovery.conf` with target time
   - Start database to replay WAL files

**SQL Server PITR**:
```sql
-- Restore to specific time
RESTORE DATABASE MyDB FROM DISK = 'C:\Backup\MyDB_Full.bak' WITH NORECOVERY;
RESTORE LOG MyDB FROM DISK = 'C:\Backup\MyDB_Log.trn'
    WITH STOPAT = '2026-02-01 14:30:00', RECOVERY;
```

---

## Section 5.5: Indexing and Query Optimization (A)

Proper indexing and query optimization are essential for database performance.

### 5.5.1 Index Types

**B-Tree Index** (default):
- Balanced tree structure
- Good for equality and range queries
- Most common index type

**Hash Index**:
- Hash table structure
- Fast for equality comparisons
- Not suitable for range queries

**Full-Text Index**:
- Text search optimization
- Supports word-based queries

**Composite Index**:
- Multiple columns in one index
- Order matters (leftmost prefix rule)

**Covering Index**:
- Contains all columns needed by query
- Avoids table lookup

### 5.5.2 Index Creation

```sql
-- Basic index
CREATE INDEX idx_employee_lastname ON employees(last_name);

-- Composite index
CREATE INDEX idx_emp_dept_salary ON employees(department_id, salary);

-- Unique index
CREATE UNIQUE INDEX idx_emp_email ON employees(email);

-- Partial index (PostgreSQL)
CREATE INDEX idx_active_employees ON employees(employee_id)
WHERE status = 'active';

-- Include columns (SQL Server, PostgreSQL)
CREATE INDEX idx_emp_search ON employees(last_name)
INCLUDE (first_name, email);

-- Drop index
DROP INDEX idx_employee_lastname;
```

### 5.5.3 Query Execution Plans

**Viewing Execution Plans**:

```sql
-- MySQL
EXPLAIN SELECT * FROM employees WHERE department_id = 10;
EXPLAIN ANALYZE SELECT * FROM employees WHERE department_id = 10;

-- PostgreSQL
EXPLAIN SELECT * FROM employees WHERE department_id = 10;
EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM employees WHERE department_id = 10;

-- SQL Server
SET SHOWPLAN_TEXT ON;
SELECT * FROM employees WHERE department_id = 10;

-- Or use graphical execution plan in SSMS
```

**Key Plan Elements**:
- **Seq Scan / Table Scan**: Full table read (often slow)
- **Index Scan**: Using index to find rows
- **Index Only Scan**: Query satisfied entirely from index
- **Nested Loop**: Row-by-row join (good for small sets)
- **Hash Join**: Hash table join (good for larger sets)
- **Merge Join**: Sorted data join (good for sorted data)

### Practical Example 5.6: Query Optimization

**Scenario**: Optimize a slow query.

**Original Query** (slow):
```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id
AND UPPER(e.last_name) = 'SMITH'
AND e.hire_date > '2020-01-01';
```

**Issues Identified**:
1. `UPPER()` function prevents index use
2. Implicit join syntax (harder to read)
3. Missing indexes

**Optimized Query**:
```sql
-- Create supporting index
CREATE INDEX idx_emp_lastname_hire ON employees(last_name, hire_date);

-- Optimized query
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id
WHERE e.last_name = 'Smith'
AND e.hire_date > '2020-01-01';
```

**If case-insensitive search needed**:
```sql
-- PostgreSQL: functional index
CREATE INDEX idx_emp_lastname_lower ON employees(LOWER(last_name));

SELECT * FROM employees WHERE LOWER(last_name) = 'smith';
```

### 5.5.4 Performance Tuning Best Practices

**Query Optimization Tips**:
1. Use `SELECT specific_columns` instead of `SELECT *`
2. Avoid functions on indexed columns in WHERE clause
3. Use appropriate JOIN types
4. Limit result sets with `LIMIT`/`TOP`
5. Use `EXISTS` instead of `IN` for subqueries
6. Avoid `OR` conditions; use `UNION` instead
7. Use bind variables/parameters (prevents SQL injection, enables plan caching)

**Index Strategy**:
1. Index columns used in WHERE, JOIN, ORDER BY
2. Consider composite indexes for common queries
3. Index foreign keys
4. Don't over-index (slows writes)
5. Regularly review and remove unused indexes

---

## Section 5.6: Stored Procedures, Triggers, and Views (A)

Procedural database objects enable code reuse, security, and automation.

### 5.6.1 Stored Procedures

**Creating Procedures**:

```sql
-- PostgreSQL
CREATE OR REPLACE FUNCTION get_employees_by_dept(p_dept_id INT)
RETURNS TABLE (
    employee_id INT,
    first_name VARCHAR,
    last_name VARCHAR,
    salary NUMERIC
) AS $$
BEGIN
    RETURN QUERY
    SELECT e.employee_id, e.first_name, e.last_name, e.salary
    FROM employees e
    WHERE e.department_id = p_dept_id;
END;
$$ LANGUAGE plpgsql;

-- Call
SELECT * FROM get_employees_by_dept(10);

-- SQL Server
CREATE PROCEDURE GetEmployeesByDept
    @DeptID INT
AS
BEGIN
    SELECT employee_id, first_name, last_name, salary
    FROM employees
    WHERE department_id = @DeptID;
END;

-- Execute
EXEC GetEmployeesByDept @DeptID = 10;
```

### 5.6.2 Triggers

Triggers automatically execute in response to table events:

```sql
-- PostgreSQL: Audit trigger
CREATE OR REPLACE FUNCTION audit_employee_changes()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'UPDATE' THEN
        INSERT INTO employee_audit (employee_id, old_salary, new_salary, changed_at)
        VALUES (OLD.employee_id, OLD.salary, NEW.salary, NOW());
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_employee_audit
AFTER UPDATE OF salary ON employees
FOR EACH ROW
EXECUTE FUNCTION audit_employee_changes();

-- SQL Server: Audit trigger
CREATE TRIGGER trg_Employee_Audit
ON employees
AFTER UPDATE
AS
BEGIN
    INSERT INTO employee_audit (employee_id, old_salary, new_salary, changed_at)
    SELECT
        i.employee_id,
        d.salary AS old_salary,
        i.salary AS new_salary,
        GETDATE()
    FROM inserted i
    INNER JOIN deleted d ON i.employee_id = d.employee_id
    WHERE i.salary <> d.salary;
END;
```

### 5.6.3 Views

Views are virtual tables based on queries:

```sql
-- Create view
CREATE VIEW v_employee_details AS
SELECT
    e.employee_id,
    e.first_name || ' ' || e.last_name AS full_name,
    e.email,
    d.department_name,
    m.first_name || ' ' || m.last_name AS manager_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
LEFT JOIN employees m ON e.manager_id = m.employee_id;

-- Use view
SELECT * FROM v_employee_details WHERE department_name = 'IT';

-- Materialized view (PostgreSQL)
CREATE MATERIALIZED VIEW mv_dept_summary AS
SELECT
    d.department_id,
    d.department_name,
    COUNT(*) AS employee_count,
    AVG(e.salary) AS avg_salary
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;

-- Refresh materialized view
REFRESH MATERIALIZED VIEW mv_dept_summary;
```

---

## Section 5.7: NoSQL Databases (A)

NoSQL databases offer alternatives to relational databases for specific use cases.

### 5.7.1 NoSQL Categories

| Type | Description | Examples | Use Cases |
|------|-------------|----------|-----------|
| Document | JSON/BSON documents | MongoDB, CouchDB | Content management, catalogs |
| Key-Value | Simple key-value pairs | Redis, DynamoDB | Caching, session storage |
| Column-Family | Wide-column stores | Cassandra, HBase | Time-series, analytics |
| Graph | Nodes and relationships | Neo4j, OrientDB | Social networks, recommendations |

### 5.7.2 CAP Theorem

Distributed databases can only guarantee two of three properties:

- **Consistency**: All nodes see the same data
- **Availability**: Every request receives a response
- **Partition Tolerance**: System operates despite network failures

**Trade-offs**:
- CP: Consistent and partition-tolerant (e.g., MongoDB with majority writes)
- AP: Available and partition-tolerant (e.g., Cassandra, DynamoDB)
- CA: Not achievable in distributed systems

### 5.7.3 BASE vs ACID

**BASE** (NoSQL approach):
- **B**asically **A**vailable
- **S**oft state
- **E**ventually consistent

Compared to ACID:
| Property | ACID | BASE |
|----------|------|------|
| Consistency | Strong | Eventual |
| Availability | Can be blocked | Always available |
| Focus | Correctness | Performance/availability |

### 5.7.4 MongoDB Example

```javascript
// Insert document
db.employees.insertOne({
    name: "John Smith",
    email: "john.smith@agency.gov",
    department: "IT",
    skills: ["Python", "SQL", "AWS"],
    hire_date: new Date("2024-01-15")
});

// Find documents
db.employees.find({ department: "IT" });
db.employees.find({ skills: { $in: ["Python"] } });

// Update
db.employees.updateOne(
    { email: "john.smith@agency.gov" },
    { $set: { salary: 75000 }, $push: { skills: "Docker" } }
);

// Aggregation
db.employees.aggregate([
    { $match: { department: "IT" } },
    { $group: { _id: "$department", avgSalary: { $avg: "$salary" } } }
]);
```

---

## Section 5.8: Data Warehousing (E)

Data warehouses support analytical workloads and business intelligence.

### 5.8.1 Star Schema

The star schema is the simplest data warehouse design:

**Components**:
- **Fact Table**: Contains measures/metrics and foreign keys
- **Dimension Tables**: Contain descriptive attributes

**Example**:
```
                    [dim_date]
                         │
                         │
[dim_product]───────[fact_sales]───────[dim_customer]
                         │
                         │
                    [dim_store]
```

**Fact Table: fact_sales**:
| sale_id | date_key | product_key | customer_key | store_key | quantity | amount |
|---------|----------|-------------|--------------|-----------|----------|--------|

**Dimension Table: dim_date**:
| date_key | date | day_name | month | quarter | year |
|----------|------|----------|-------|---------|------|

### 5.8.2 Snowflake Schema

Snowflake schema normalizes dimension tables:

```
[dim_category]
      │
      │
[dim_product]───────[fact_sales]
      │
      │
[dim_brand]
```

**Trade-offs**:
- Star: Simpler queries, more redundancy
- Snowflake: Less redundancy, more complex joins

### 5.8.3 OLTP vs OLAP

| Characteristic | OLTP | OLAP |
|----------------|------|------|
| Purpose | Day-to-day transactions | Analytics, reporting |
| Operations | INSERT, UPDATE, DELETE | SELECT, aggregations |
| Normalization | Highly normalized (3NF) | Denormalized (star/snowflake) |
| Query complexity | Simple | Complex |
| Data volume per query | Small | Large |
| Users | Many concurrent | Few analysts |
| Response time | Milliseconds | Seconds to minutes |

### 5.8.4 ETL Processes

**ETL**: Extract, Transform, Load

1. **Extract**: Pull data from source systems
2. **Transform**: Clean, standardize, aggregate
3. **Load**: Insert into data warehouse

**Modern Alternative - ELT**: Extract, Load, Transform
- Load raw data first
- Transform in the data warehouse
- Leverages warehouse compute power

### Practical Example 5.7: Data Warehouse Design

**Scenario**: Design a data warehouse for government procurement analytics.

**Fact Table: fact_procurement**:
```sql
CREATE TABLE fact_procurement (
    procurement_id SERIAL PRIMARY KEY,
    date_key INT REFERENCES dim_date(date_key),
    vendor_key INT REFERENCES dim_vendor(vendor_key),
    department_key INT REFERENCES dim_department(department_key),
    category_key INT REFERENCES dim_category(category_key),
    contract_value DECIMAL(15,2),
    quantity INT,
    delivery_days INT
);
```

**Sample Query**:
```sql
SELECT
    d.year,
    d.quarter,
    dep.department_name,
    cat.category_name,
    SUM(f.contract_value) AS total_value,
    AVG(f.delivery_days) AS avg_delivery_days
FROM fact_procurement f
JOIN dim_date d ON f.date_key = d.date_key
JOIN dim_department dep ON f.department_key = dep.department_key
JOIN dim_category cat ON f.category_key = cat.category_key
WHERE d.year = 2025
GROUP BY d.year, d.quarter, dep.department_name, cat.category_name
ORDER BY total_value DESC;
```

---

## Section 5.9: Database Replication and Sharding (E)

Replication and sharding enable scalability and high availability.

### 5.9.1 Replication Types

**Master-Slave (Primary-Replica)**:
- One primary handles writes
- Replicas handle reads
- Asynchronous or synchronous

**Master-Master (Multi-Primary)**:
- Multiple nodes accept writes
- Conflict resolution required
- Complex but highly available

### 5.9.2 Sharding

Sharding distributes data across multiple databases:

**Sharding Strategies**:
- **Range-based**: Data split by value ranges
- **Hash-based**: Data distributed by hash function
- **Directory-based**: Lookup table determines shard

**Considerations**:
- Cross-shard queries are complex
- Rebalancing can be difficult
- Choose shard key carefully

---

## Hands-on Labs

### Lab 5.1: Database Design and Normalization

See [labs/lab-05-01-database-design.md](labs/lab-05-01-database-design.md) for complete lab instructions.

**Objective**: Design and normalize a database schema for a government HR system.

### Lab 5.2: SQL Query Development

See [labs/lab-05-02-sql-queries.md](labs/lab-05-02-sql-queries.md) for complete lab instructions.

**Objective**: Write complex SQL queries including joins, subqueries, and aggregations.

### Lab 5.3: Database Security Implementation

See [labs/lab-05-03-db-security.md](labs/lab-05-03-db-security.md) for complete lab instructions.

**Objective**: Implement role-based access control and audit logging.

### Lab 5.4: Backup and Recovery

See [labs/lab-05-04-backup-recovery.md](labs/lab-05-04-backup-recovery.md) for complete lab instructions.

**Objective**: Configure and test database backup and point-in-time recovery.

### Lab 5.5: Query Optimization

See [labs/lab-05-05-query-optimization.md](labs/lab-05-05-query-optimization.md) for complete lab instructions.

**Objective**: Analyze execution plans and optimize slow queries using indexing.

---

## Chapter Summary

Key points covered in this chapter:

- ACID properties (Atomicity, Consistency, Isolation, Durability) ensure reliable database transactions.
- Database normalization (1NF through BCNF) reduces redundancy and improves data integrity through functional dependency analysis.
- SQL provides powerful querying capabilities including JOINs, subqueries, aggregate functions, window functions, and CTEs.
- Database security requires proper user management, role-based access control, and the principle of least privilege.
- Backup strategies must include full, differential, and transaction log backups to enable point-in-time recovery.
- Indexing significantly improves query performance; understanding execution plans helps identify optimization opportunities.
- NoSQL databases offer alternatives for specific use cases, with trade-offs described by the CAP theorem.
- Data warehousing uses star/snowflake schemas optimized for OLAP workloads.
- Replication and sharding enable database scalability and high availability.

---

## Key Takeaways

1. **ACID compliance is essential for transactional systems**: Understanding ACID properties helps evaluate database suitability for different use cases.

2. **Normalization prevents data anomalies**: Following normal forms (at least 3NF) ensures data integrity, though denormalization may be appropriate for read-heavy workloads.

3. **SQL proficiency is a core IT skill**: Complex queries with JOINs, subqueries, and aggregations are frequently needed and often tested.

4. **Database security follows least privilege**: Implement RBAC with specific permissions rather than broad access.

5. **Query optimization requires understanding execution plans**: Proper indexing and query structure can dramatically improve performance.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Explain the ACID properties** with a real-world example of a transaction that requires all four properties. What happens if any property is violated? (B/I)

2. **Normalize the following table to 3NF**, showing each step and explaining the problems you're solving:
   StudentID | StudentName | CourseID | CourseName | InstructorID | InstructorName | InstructorOffice (I/A)

3. **Write a SQL query** to find the top 3 departments by average salary, including only departments with more than 5 employees, showing department name, employee count, and average salary. (A)

4. **Design a data warehouse schema** for a government tax revenue system that tracks tax collections by type, region, and time period. Include fact and dimension tables with sample columns. (E)

5. **Compare relational databases with document databases (e.g., MongoDB)** for a citizen services portal that handles thousands of form submissions daily. What factors would influence your choice? (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 50 Beginner (B) questions (25%)
- 70 Intermediate (I) questions (35%)
- 60 Advanced (A) questions (30%)
- 20 Expert (E) questions (10%)

Total: 200 MCQs

---

## References

- Silberschatz, Abraham, Henry F. Korth, and S. Sudarshan. "Database System Concepts." 7th Edition. 2019.
- Ramakrishnan, Raghu, and Johannes Gehrke. "Database Management Systems." 3rd Edition. 2003.
- PostgreSQL Global Development Group. "PostgreSQL Documentation." 2025. https://www.postgresql.org/docs/
- Oracle. "MySQL Reference Manual." 2025. https://dev.mysql.com/doc/
- Microsoft. "SQL Server Documentation." 2025. https://docs.microsoft.com/en-us/sql/
- MongoDB. "MongoDB Manual." 2025. https://docs.mongodb.com/manual/
- Kimball, Ralph. "The Data Warehouse Toolkit." 3rd Edition. 2013.
- Kleppmann, Martin. "Designing Data-Intensive Applications." 2017.

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
