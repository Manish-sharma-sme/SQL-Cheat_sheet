# SQL-Cheat_sheet
Cheat Sheet for MY SQL

## Login

```bash
mysql -u root -p
```
## Show employees

```sql
SELECT User, Host FROM mysql.user;
```

## Create User

```sql
CREATE USER 'someuser'@'localhost' IDENTIFIED BY 'somepassword';
```

## Grant All Priveleges On All Databases

```sql
GRANT ALL PRIVILEGES ON * . * TO 'someuser'@'localhost';
FLUSH PRIVILEGES;
```

## Show Grants

```sql
SHOW GRANTS FOR 'someuser'@'localhost';
```

## Remove Grants

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';
```

## Delete User

```sql
DROP USER 'someuser'@'localhost';
```

## Exit

```sql
exit;
```

## Show Databases

```sql
SHOW DATABASES
```

## Create Database

```sql
CREATE DATABASE demo;
```

## Delete Database

```sql
DROP DATABASE demo;
```

## Select Database

```sql
USE demo;
```

## Create Table

```sql
CREATE TABLE employees(
id INT AUTO_INCREMENT,
   first_name VARCHAR(100),
   last_name VARCHAR(100),
   email VARCHAR(50),
   password VARCHAR(20),
   location VARCHAR(100),
   dept VARCHAR(100),
   is_admin TINYINT(1),
   register_date DATETIME,
   PRIMARY KEY(id)
);
```

## Delete / Drop Table

```sql
DROP TABLE tablename;
```

## Show Tables

```sql
SHOW TABLES;
```

## Insert Row / Record

```sql
INSERT INTO employees (first_name, last_name, email, password, location, dept, is_admin, register_date) values ('Manish', 'Sharma', 'manish@gmail.com', '123456','himachal', 'development', 1, now());
```

## Insert Multiple Rows

```sql
INSERT INTO employees (first_name, last_name, email, password, location, dept,  is_admin, register_date) values ('Rubal', 'thakur', 'Rubal@gmail.com', '123456', 'New Delhi', 'design', 0, now()), ('Ismail', 'Shaikh', 'Ismail@gmail.com', '123456', 'Mumbai', 'Tester', 0, now());
```

## Select

```sql
SELECT * FROM employees;
SELECT first_name, last_name FROM employees;
```

## Where Clause

```sql
SELECT * FROM employees WHERE location='New Delhi';
SELECT * FROM employees WHERE location='New Delhi' AND dept='design';
SELECT * FROM employees WHERE is_admin = 1;
SELECT * FROM employees WHERE is_admin > 0;
```

## Delete Row

```sql
DELETE FROM employees WHERE id = 3;
```

## Update Row

```sql
UPDATE employees SET email = 'rubal_thakur@gmail.com' WHERE id = 2;

```

## Add New Column

```sql
ALTER TABLE employees ADD age VARCHAR(20);
```

## Modify Column

```sql
ALTER TABLE employees MODIFY COLUMN age INT;
```

## Order By (Sort)

```sql
SELECT * FROM employees ORDER BY last_name DESC;
SELECT * FROM employees ORDER BY last_name ASC; (default-sort)

```

## Concatenate Columns

```sql
SELECT CONCAT(first_name, ' ', last_name) AS 'full_Name', dept FROM employees;

```

## Select Distinct Rows

```sql
SELECT DISTINCT location FROM employees;

```

## Between (Select Range)

```sql
SELECT * FROM employees WHERE age BETWEEN 20 AND 25;
```

## Like (Searching)

```sql
SELECT * FROM employees WHERE dept LIKE 'd%';
SELECT * FROM employees WHERE dept LIKE 'dev%';
SELECT * FROM employees WHERE dept LIKE '%t';
SELECT * FROM employees WHERE dept LIKE '%e%';
```

## Not Like

```sql
SELECT * FROM employees WHERE dept NOT LIKE 'd%';
```

## IN

```sql
SELECT * FROM employees WHERE dept IN ('design', 'testing');
```

## Create & Remove Index

```sql
CREATE INDEX LIndex On employees(location);
DROP INDEX LIndex ON employees;
```

## New Table With Foreign Key (Posts)

```sql
CREATE TABLE posts(
id INT AUTO_INCREMENT,
   user_id INT,
   title VARCHAR(100),
   body TEXT,
   publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
   PRIMARY KEY(id),
   FOREIGN KEY (user_id) REFERENCES employees(id)
);
```

## Add Data to Posts Table

```sql
INSERT INTO posts(user_id, title, body) VALUES (1, 'Post One', 'This is post one'),(3, 'Post Two', 'This is post two'),(1, 'Post Three', 'This is post three'),(2, 'Post Four', 'This is post four'),(5, 'Post Five', 'This is post five'),(4, 'Post Six', 'This is post six'),(2, 'Post Seven', 'This is post seven'),(1, 'Post Eight', 'This is post eight'),(3, 'Post Nine', 'This is post none'),(4, 'Post Ten', 'This is post ten');
```

## INNER JOIN

```sql
SELECT
  employees.first_name,
  employees.last_name,
  posts.title,
  posts.publish_date
FROM employees
INNER JOIN posts
ON employees.id = posts.user_id
ORDER BY posts.title;
```

## New Table With 2 Foriegn Keys

```sql
CREATE TABLE comments(
	id INT AUTO_INCREMENT,
    post_id INT,
    user_id INT,
    body TEXT,
    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id),
    FOREIGN KEY(user_id) references employees(id),
    FOREIGN KEY(post_id) references posts(id)
);
```

## Add Data to Comments Table

```sql
INSERT INTO comments(post_id, user_id, body) VALUES (1, 3, 'This is comment one'),(2, 1, 'This is comment two'),(5, 3, 'This is comment three'),(2, 4, 'This is comment four'),(1, 2, 'This is comment five'),(3, 1, 'This is comment six'),(3, 2, 'This is comment six'),(5, 4, 'This is comment seven'),(2, 3, 'This is comment seven');
```

## Left Join

```sql
SELECT
comments.body,
posts.title
FROM comments
LEFT JOIN posts ON posts.id = comments.post_id
ORDER BY posts.title;

```

## Join Multiple Tables

```sql
SELECT
comments.body,
posts.title,
employees.first_name,
employees.last_name
FROM comments
INNER JOIN posts on posts.id = comments.post_id
INNER JOIN employees on employees.id = comments.user_id
ORDER BY posts.title;

```

## Aggregate Functions

```sql
SELECT COUNT(id) FROM employees;
SELECT MAX(age) FROM employees;
SELECT MIN(age) FROM employees;
SELECT SUM(age) FROM employees;
SELECT UCASE(first_name), LCASE(last_name) FROM employees;

```

## Group By

```sql
SELECT age, COUNT(age) FROM employees GROUP BY age;
SELECT age, COUNT(age) FROM employees WHERE age > 18 GROUP BY age;
SELECT age, COUNT(age) FROM employees GROUP BY age HAVING count(age) >=2;

```
