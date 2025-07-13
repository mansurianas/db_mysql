# SQL Command Types (DDL, DML, DQL, DCL, TCL)

---

## 1. DDL (Data Definition Language)

 **Purpose**:  
Used to **create**, **modify**, or **delete** database structures like tables and schemas.

| Command     | What it does                                           |
|-------------|--------------------------------------------------------|
| `CREATE`    | Creates a new table or database                        |
| `ALTER`     | Adds new columns or modifies existing structure        |
| `DROP`      | Deletes a table or database permanently                |
| `TRUNCATE`  | Deletes all data from a table but keeps the structure  |
| `RENAME`    | Changes the name of a table                            |

---

## 2. DML (Data Manipulation Language)

 **Purpose**:  
Used to **insert**, **update**, or **delete** data inside a table.

| Command     | What it does                              |
|-------------|-------------------------------------------|
| `INSERT`    | Adds new data (rows) into a table         |
| `UPDATE`    | Modifies existing data in a table         |
| `DELETE`    | Removes data (rows) from a table          |

---

## 3. DQL (Data Query Language)

**Purpose**:  
Used to **read/query data** from a table.

| Command     | What it does                             |
|-------------|------------------------------------------|
| `SELECT`    | Retrieves data from a table               |

---

## 4. DCL (Data Control Language)

 **Purpose**:  
Used to control **access and permissions** for users in a database.

| Command     | What it does                                               |
|-------------|------------------------------------------------------------|
| `GRANT`     | Gives specific permissions to users (e.g., read/write)     |
| `REVOKE`    | Removes previously granted permissions from users          |

---

## 5. TCL (Transaction Control Language)

 **Purpose**:  
Used to manage **transactions**, allowing you to **save** or **undo** changes made during a transaction.

| Command       | What it does                                         |
|---------------|------------------------------------------------------|
| `COMMIT`      | Saves all changes permanently to the database        |
| `ROLLBACK`    | Undoes changes made during the transaction           |
| `SAVEPOINT`   | Sets a point to roll back to during a transaction    |




# Full hands-on practice using MySQL CLI — beginner friendly


Show All Databases

```sql
SHOW DATABASES;
```
```
+--------------------+
| Database           |
+--------------------+
| anas               |
| information_schema |
| mydb               |
| mysql              |
| performance_schema |
| sys                |
| tech               |
| wscube             |
+--------------------+
```
Select a Database
```sql

USE mydb;
```
Output:
```
Database changed
```

create a table
```
CREATE TABLE student (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  age INT
);
```
view table
```
SELECT * FROM student;


```

insert data 
```
INSERT INTO student (id, name, age)
VALUES (1, 'Anas', 22);

```
insert Multiple Rows

```
INSERT INTO student (id, name, age)
VALUES 
  (2, 'zara', 21),
  (3, 'muskan', 23),
  (4, 'aman', 20);
```
View Table After Inserts
```
SELECT * FROM student;

```
```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | zara   |   21 |
|  3 | muskan |   23 |
|  4 | aman   |   20 |
+----+--------+------+
````
SELECT Specific Columns
```
SELECT name FROM student;
```
```
+--------+
| name   |
+--------+
| Anas   |
| zara   |
| muskan |
| aman   |
+--------+
```
SELECT name, age FROM student;

```
+--------+------+
| name   | age  |
+--------+------+
| Anas   |   22 |
| zara   |   21 |
| muskan |   23 |
| aman   |   20 |
+--------+------+
```
WHERE Clause (Filter by Name)

```
SELECT * FROM student WHERE name = 'zara';
```
```
+----+------+------+
| id | name | age  |
+----+------+------+
|  2 | zara |   21 |
+----+------+------+
```
WHERE with Conditions

```
SELECT * FROM student WHERE age > 21;
```
```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  3 | muskan |   23 |
+----+--------+------+
```
Update a Record
```
UPDATE student SET age = 18 WHERE name = 'aman';
```
and
```
UPDATE student SET name = 'ZARA' WHERE id = 2;

```
Delete a Row
```
DELETE FROM student WHERE id = 4;
```
IN, BETWEEN, LIKE Conditions
```
SELECT * FROM student WHERE name IN ('ZARA', 'muskan');
```

```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
+----+--------+------+
```

SELECT * FROM student WHERE age BETWEEN 18 AND 25;

```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
+----+--------+------+
```


SELECT * FROM student WHERE name LIKE '%a%';

```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
+----+--------+------+
```

select * from student where name like '%u%';

```
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  3 | muskan |   23 |
+----+--------+------+
```

INSERT INTO student (id, name, age) VALUES (5, 'riya', 45);
```
select *from student;
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
|  5 | riya   |   45 |
+----+--------+------+
```

UPDATE student SET age = 23 WHERE name = 'riya';

```

mysql> select *from student;
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
|  5 | riya   |   23 |
+----+--------+------+
4 rows in set (0.00 sec)
```

DELETE FROM student WHERE id = 5;
```
select *from student;
+----+--------+------+
| id | name   | age  |
+----+--------+------+
|  1 | Anas   |   22 |
|  2 | ZARA   |   21 |
|  3 | muskan |   23 |
+----+--------+------+
3 rows in set (0.00 sec)
```



