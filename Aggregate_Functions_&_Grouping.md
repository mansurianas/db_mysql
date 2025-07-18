## Aggregate function

Aggregate functions operate on the values of an entire column — producing a summary of the entire table.

count () , sum () , avg(), max () min() 



##### GROUP BY Clause

When you want to get a summary according to a group of columns.

It is used with COUNT, SUM, AVG.

`Example: How many employees are there in each department?`
```mysql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department;
```
 ##### WHERE vs HAVING (in SQL)

| Clause   | Use                               | When It’s Applied             |
| -------- | --------------------------------- | ----------------------------- |
| `WHERE`  | Filters **rows before** grouping  | Applied **before** `GROUP BY` |
| `HAVING` | Filters **groups after** grouping | Applied **after** `GROUP BY`  |

how only those departments which have more than 3 employees

```sql

SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department
HAVING COUNT(*) > 3;
```
##### Grouping with Multiple Columns (in SQL)

you can group by multiple columns in SQL.


`How many employees are there for each gender in each department?`

```sql

SELECT department, gender, COUNT(*) 
FROM employees 
GROUP BY department, gender;
```

###### now create a table employee
```mysql

 create table employee (
    ->     id INT PRIMARY KEY,
    ->     name VARCHAR(50),
    ->     age INT,
    ->     gender VARCHAR(10),
    ->     department VARCHAR(50),
    ->     salary INT,
    ->     city VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.09 sec)

mysql> insert into employee (id, name, age, gender, department, salary, city) VALUES
    -> (1, 'Anas', 30, 'Male', 'IT', 60000, 'Delhi'),
    -> (2, 'Zara', 25, 'Female', 'HR', 50000, 'Mumbai'),
    -> (3, 'Muskan', 28, 'Female', 'IT', 70000, 'Kolkata'),
    -> (4, 'Aman', 32, 'Male', 'Finance', 45000, 'Delhi'),
    -> (5, 'Riya', 29, 'Female', 'IT', 75000, 'Mumbai'),
    -> (6, 'Raj', 31, 'Male', 'HR', 52000, 'Kolkata'),
    -> (7, 'Rahul', 26, 'Male', 'Finance', 48000, 'Hyderabad'),
    -> (8, 'Priya', 27, 'Female', 'IT', 71000, 'Delhi');
Query OK, 8 rows affected (0.01 sec)
Records: 8  Duplicates: 0  Warnings: 0
```


# SQL Query Examples

## 1. Total number of employees
```sql
SELECT COUNT(*) AS total_employees FROM employee;
```
**Output:**
```
total_employees
----------------
8
```

## 2. Total salary of all employee
```sql
SELECT SUM(salary) AS total_salary FROM employees;
```
**Output:**
```
total_salary
-------------
471000
```

## 3. Average salary of IT department
```sql
SELECT AVG(salary) AS avg_it_salary
FROM employee
WHERE department = 'IT';
```
**Output:**
```
avg_it_salary
--------------
69000
```

## 4. Maximum and minimum salary of employees
```sql
SELECT MAX(salary) AS max_salary, MIN(salary) AS min_salary
FROM employee;
```
**Output:**
```
max_salary | min_salary
------------------------
75000      | 45000
```

## 5. Count of employees in each department
```sql
SELECT department, COUNT(*) AS employee_count
FROM employee
GROUP BY department;
```
**Output:**
```
department | employee_count
----------------------------
IT         | 4
HR         | 2
Finance    | 2
```

## 6. Number of male and female employees in each department
```sql
SELECT department, gender, COUNT(*) AS gender_count
FROM employee
GROUP BY department, gender;
```
**Output:**
```
department | gender | gender_count
----------------------------------
IT         | Male   | 1
IT         | Female | 3
HR         | Male   | 1
HR         | Female | 1
Finance    | Male   | 2
```

## 7. Departments with more than 2 employees
```sql
SELECT department, COUNT(*) AS emp_count
FROM employee
GROUP BY department
HAVING COUNT(*) > 2;
```
**Output:**
```
department | emp_count
-----------------------
IT         | 4
```

## 8. Cities where average salary is more than 60000
```sql
SELECT city, AVG(salary) AS avg_city_salary
FROM employees
GROUP BY city
HAVING AVG(salary) > 60000;
```
**Output:**
```
city     | avg_city_salary
---------------------------
Kolkata  | 61000
Mumbai   | 62500
Delhi    | 64000
```

## 9. For each department and gender, count the employees
```sql
SELECT department, gender, COUNT(*) AS count
FROM employee
GROUP BY department, gender;
```
**Output:**
```
department | gender | count
----------------------------
IT         | Male   | 1
IT         | Female | 3
HR         | Male   | 1
HR         | Female | 1
Finance    | Male   | 2
```

## 10. Employees who earn more than average salary of their department
```sql
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
    WHERE department = e.department
);
```
**Output:**
```
id | name   | age | gender | department | salary | city
---------------------------------------------------------
3  | Muskan | 28  | Female | IT         | 70000  | Kolkata
5  | Riya   | 29  | Female | IT         | Mumbai
8  | Priya  | 27  | Female | IT         | Delhi
6  | Raj    | 31  | Male   | HR         | 52000  | Kolkata
7  | Rahul  | 26  | Male   | Finance    | 48000  | Hyderabad
```
#### now create a  table orderes 
```mysql
CREATE TABLE orders (
    order_id INT,
    customer_name VARCHAR(50),
    product VARCHAR(50),
    category VARCHAR(50),
    quantity INT,
    price_per_unit INT,
    city VARCHAR(50)
);

INSERT INTO orders (order_id, customer_name, product, category, quantity, price_per_unit, city) VALUES
(1, 'Anas', 'Laptop', 'Electronics', 1, 60000, 'Delhi'),
(2, 'Zara', 'Headphones', 'Electronics', 2, 3000, 'Mumbai'),
(3, 'Rahul', 'Shoes', 'Fashion', 3, 2000, 'Kolkata'),
(4, 'Riya', 'Watch', 'Fashion', 1, 5000, 'Delhi'),
(5, 'Aman', 'Phone', 'Electronics', 1, 25000, 'Mumbai'),
(6, 'Muskan', 'Dress', 'Fashion', 2, 4000, 'Kolkata'),
(7, 'Priya', 'Tablet', 'Electronics', 1, 18000, 'Delhi'),
(8, 'Raj', 'Sunglasses', 'Fashion', 2, 1500, 'Hyderabad');

```
Practice Queries with Aggregates & Grouping:


## 1 Total number of orders:

```sql

SELECT COUNT(*) AS total_orders FROM orders;
```
```

total_orders
------------
10
```

## 2  Total quantity of items sold:

```sql

SELECT SUM(quantity) AS total_quantity FROM orders;
```
```
total_quantity
--------------
32
```

###  3 Average price per unit of all products:

```sql

SELECT AVG(price_per_unit) AS avg_price FROM orders;
```
```
avg_price
---------
19250
```


## 4  Maximum and Minimum price per unit:

```sql


SELECT MAX(price_per_unit) AS max_price, MIN(price_per_unit) AS min_price FROM orders;
```

```
max_price | min_price
---------------------
50000     | 1200
```



## 5 Count of orders per city:

```sql

SELECT city, COUNT(*) AS total_orders FROM orders GROUP BY city;
```
```
city      | total_orders
-------------------------
Delhi     | 4
Mumbai    | 3
Kolkata   | 2
Bangalore | 1
```


## 6 Total sales (quantity × price) per category:

```sql

SELECT category, SUM(quantity * price_per_unit) AS total_sales FROM orders GROUP BY category;

```
```
category     | total_sales
--------------------------
Electronics  | 215000
Clothing     | 29500
Footwear     | 17400


```

## 7 Average quantity per product category:

```sql

SELECT category, AVG(quantity) AS avg_quantity FROM orders GROUP BY category;
```
```
category     | avg_quantity
---------------------------
Electronics  | 1.75
Clothing     | 4.5
Footwear     | 3.5
```



## 8  Categories having total sales more than 50000:

```sql

SELECT category, SUM(quantity * price_per_unit) AS total_sales
FROM orders
GROUP BY category
HAVING total_sales > 50000;
```
```
category     | total_sales
--------------------------
Electronics  | 215000

```


## 9 Number of orders in each city and category (Multiple columns):

```sql

SELECT city, category, COUNT(*) AS orders_count
FROM orders
GROUP BY city, category;
```
```
city      | category     | orders_count
---------------------------------------
Delhi     | Electronics  | 1
Delhi     | Clothing     | 2
Delhi     | Footwear     | 1
Mumbai    | Electronics  | 2
Mumbai    | Footwear     | 1
Kolkata   | Clothing     | 2
Bangalore | Electronics  | 1

```


## 10  Orders with price more than average price (using subquery):

```sql

SELECT * FROM orders
WHERE price_per_unit > (SELECT AVG(price_per_unit) FROM orders);
```
```
id | product_name | category    | quantity | price_per_unit | city
---------------------------------------------------------------------
1  | Laptop       | Electronics | 2        | 50000          | Delhi
5  | AC           | Electronics | 1        | 35000          | Mumbai
8  | Refrigerator | Electronics | 1        | 40000          | Bangalore

```




