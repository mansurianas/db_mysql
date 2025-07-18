
# SQL Joins Explained with Examples

##  What is a SQL JOIN?

A JOIN is used to combine rows from two or more tables based on a related column (like a foreign key).

## Why Use Joins?
In relational databases, data is often spread across multiple tables. Joins are used to:
- Retrieve related data stored in different tables.
- Reduce data duplication by using foreign keys.
- Build meaningful relationships between datasets.

## When to Use Joins?
- Whenever you need data from two or more related tables.
- Common in reporting, dashboard queries, and normalized database structures.

---
<img width="570" height="592" alt="Screenshot 2025-07-19 012945" src="https://github.com/user-attachments/assets/ed572bc0-567b-4a79-93d4-55c6eeb23505" />




## Sample Tables:

### Table: Employees
| emp_id | name   | dept_id |
|--------|--------|---------|
| 1      | Alice  | 101     |
| 2      | Bob    | 102     |
| 3      | Carol  | NULL    |
| 4      | David  | 101     |

### Table: Departments
| dept_id | dept_name     |
|---------|---------------|
| 101     | IT            |
| 102     | HR            |
| 103     | Marketing     |

---

## 1. INNER JOIN
Returns records that have matching values in both tables.

```sql
SELECT e.name, d.dept_name
FROM Employees e
INNER JOIN Departments d ON e.dept_id = d.dept_id;
```
```
SELECT: e.name, d.dept_name - Get names and department names.
FROM: Employees e - Main table is Employees (alias e).
INNER JOIN: Departments d - Join Departments (alias d).
ON: e.dept_id = d.dept_id - Match dept_id.
```

`This query selects the names of employees and their corresponding department names from the Employees and Departments tables. It only returns rows where there is a match between the dept_id in both tables. In this case, it returns Alice, Bob, and David, who all belong to departments that exist in the Departments table.`
### Result:
| name  | dept_name |
|-------|-----------|
| Alice | IT        |
| Bob   | HR        |
| David | IT        |

---

## 2. LEFT JOIN (LEFT OUTER JOIN)
Returns all records from the left table, and the matched records from the right table.

```sql
SELECT e.name, d.dept_name
FROM Employees e
LEFT JOIN Departments d ON e.dept_id = d.dept_id;
```

`This query retrieves all employees, including those who do not belong to any department (like Carol). If there is no matching department, the dept_name will be NULL. Thus, it returns Alice, Bob, Carol, and David, with Carol showing NULL for dept_name.`

### Result:
| name  | dept_name |
|-------|-----------|
| Alice | IT        |
| Bob   | HR        |
| Carol | NULL      |
| David | IT        |

---

## 3. RIGHT JOIN (RIGHT OUTER JOIN)
Returns all records from the right table, and the matched records from the left table.

```sql
SELECT e.name, d.dept_name
FROM Employees e
RIGHT JOIN Departments d ON e.dept_id = d.dept_id;
```
`This query retrieves all departments, including those that do not have any employees assigned to them. If there is no matching employee, the name will be NULL. In this case, it returns Alice, Bob, David, and also the Marketing department with no employees.`

### Result:
| name  | dept_name |
|-------|-----------|
| Alice | IT        |
| Bob   | HR        |
| David | IT        |
| NULL  | Marketing |

---

## 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

```sql
SELECT e.name, d.dept_name
FROM Employees e
FULL OUTER JOIN Departments d ON e.dept_id = d.dept_id;
```
`This query combines the results of both the LEFT JOIN and RIGHT JOIN. It returns all employees and all departments, showing NULL where there are no matches. Thus, it includes all employees (Alice, Bob, Carol, David) and all departments (IT, HR, Marketing), with Carol and the Marketing department showing NULL where applicable.`

### Result:
| name  | dept_name |
|-------|-----------|
| Alice | IT        |
| Bob   | HR        |
| Carol | NULL      |
| David | IT        |
| NULL  | Marketing |

---

## 5. CROSS JOIN
Returns the Cartesian product of both tables.

```sql
SELECT e.name, d.dept_name
FROM Employees e
CROSS JOIN Departments d;
```
`This query pairs each employee with every department, resulting in a Cartesian product. For example, Alice will be paired with IT, HR, and Marketing, and this continues for each employee. This type of join is useful when you want to combine every row from one table with every row from another.`


### Result (each employee paired with each department):
| name  | dept_name |
|-------|-----------|
| Alice | IT        |
| Alice | HR        |
| Alice | Marketing |
| Bob   | IT        |
| ...   | ...       |

---

## 6. SELF JOIN
Used to join a table with itself.

### Example: Find employees who work in the same department

```sql
SELECT A.name AS Employee1, B.name AS Employee2
FROM Employees A
JOIN Employees B ON A.dept_id = B.dept_id AND A.emp_id != B.emp_id;
```
`This query finds pairs of employees who work in the same department. It uses aliases (A and B) to differentiate between the two instances of the Employees table. The condition A.emp_id != B.emp_id ensures that an employee is not paired with themselves.`

---
```
| Employee1 | Employee2 |
| --------- | --------- |
| Alice     | David     |
| David     | Alice     |
```
```
Join Condition: The query joins the Employees table with itself based on the condition that both employees must belong to the same department (A.dept_id = B.dept_id), and they must be different employees (A.emp_id != B.emp_id).```
```
]
`Analysis of the Data:`

```
Alice (emp_id 1) and David (emp_id 4) are in the same department (dept_id 101).
Bob (emp_id 2) is in department 102, which does not have any other employees in the same department.
Carol (emp_id 3) has a NULL dept_id, so she will not match with any other employee.
```


## Using Aliases with Joins
- Use aliases to simplify table names in joins.
- Makes queries more readable and easier to write.

```sql
SELECT e.name, d.dept_name
FROM Employees AS e
JOIN Departments AS d ON e.dept_id = d.dept_id;
```
` This query uses aliases (e for Employees and d for Departments) to make the SQL statement cleaner and easier to read. It functions the same as the INNER JOIN example but is more concise.`

    
| Name  | Dept\_Name |
| ----- | ---------- |
| Alice | IT         |
| David | IT         |
| Bob   | HR         |

---

## Summary
| Join Type      | Includes Non-Matching Rows? |
|----------------|-----------------------------|
| INNER JOIN     | No                          |
| LEFT JOIN      | Yes, from left table        |
| RIGHT JOIN     | Yes, from right table       |
| FULL OUTER JOIN| Yes, from both tables       |
| CROSS JOIN     | Cartesian product           |
| SELF JOIN      | Join within same table      |

---

