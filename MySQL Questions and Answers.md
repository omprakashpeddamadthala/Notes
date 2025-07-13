# MySQL Questions and Answers

## Basic Level




### Question 1: What is MySQL?
**Answer:** MySQL is an open-source relational database management system (RDBMS) that uses Structured Query Language (SQL).

### Question 2: What is a database?
**Answer:** A database is an organized collection of structured information, or data, typically stored electronically in a computer system.

### Question 3: What is a table in MySQL?
**Answer:** A table is a collection of related data entries, organized into rows and columns within a database.

### Question 4: How do you create a database in MySQL?
**Answer:** You can create a database using the `CREATE DATABASE` statement. For example: `CREATE DATABASE my_company;`

### Question 5: How do you select a database to use?
**Answer:** You can select a database using the `USE` statement. For example: `USE my_company;`

### Question 6: How do you create a table in MySQL?
**Answer:** You create a table using the `CREATE TABLE` statement, specifying column names and their data types. For example:
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

### Question 7: What are common data types in MySQL?
**Answer:** Common data types include `INT` (integer), `VARCHAR` (variable-length string), `DATE` (date), `DECIMAL` (fixed-point number), and `BOOLEAN`.

### Question 8: How do you insert data into a table?
**Answer:** You insert data using the `INSERT INTO` statement. For example:
```sql
INSERT INTO employees (id, name, age) VALUES (1, 'John Doe', 30);
```

### Question 9: How do you retrieve all data from a table?
**Answer:** You retrieve all data using the `SELECT * FROM` statement. For example: `SELECT * FROM employees;`

### Question 10: How do you retrieve specific columns from a table?
**Answer:** You specify the column names after `SELECT`. For example: `SELECT name, age FROM employees;`

### Question 11: How do you filter data using a WHERE clause?
**Answer:** You use the `WHERE` clause to specify conditions. For example: `SELECT * FROM employees WHERE age > 25;`

### Question 12: What is the primary key?
**Answer:** A primary key is a column or a set of columns that uniquely identifies each row in a table. It cannot contain NULL values and must be unique.

### Question 13: What is a foreign key?
**Answer:** A foreign key is a column or a set of columns in one table that refers to the primary key in another table. It establishes a link between two tables.

### Question 14: How do you update data in a table?
**Answer:** You update data using the `UPDATE` statement with a `SET` clause and a `WHERE` clause. For example:
```sql
UPDATE employees SET age = 31 WHERE id = 1;
```

### Question 15: How do you delete data from a table?
**Answer:** You delete data using the `DELETE FROM` statement with a `WHERE` clause. For example:
```sql
DELETE FROM employees WHERE id = 1;
```

### Question 16: What is `NULL` in MySQL?
**Answer:** `NULL` represents a missing or unknown value. It is not the same as an empty string or zero.

### Question 17: How do you check for `NULL` values?
**Answer:** You use `IS NULL` or `IS NOT NULL`. For example: `SELECT * FROM employees WHERE email IS NULL;`

### Question 18: What is `ORDER BY` used for?
**Answer:** `ORDER BY` is used to sort the result set of a query in ascending (`ASC`) or descending (`DESC`) order. For example: `SELECT * FROM employees ORDER BY name ASC;`

### Question 19: What is `LIMIT` used for?
**Answer:** `LIMIT` is used to restrict the number of rows returned by a query. For example: `SELECT * FROM employees LIMIT 10;`

### Question 20: How do you count the number of rows in a table?
**Answer:** You use the `COUNT()` aggregate function. For example: `SELECT COUNT(*) FROM employees;`

### Question 21: What is `DISTINCT` used for?
**Answer:** `DISTINCT` is used to retrieve only unique values from a column. For example: `SELECT DISTINCT department FROM employees;`

### Question 22: How do you use `AND`, `OR`, and `NOT` operators?
**Answer:** These are logical operators used to combine or negate conditions in a `WHERE` clause. For example: `SELECT * FROM employees WHERE age > 25 AND department = 'Sales';`

### Question 23: What is `LIKE` operator used for?
**Answer:** `LIKE` is used for pattern matching in a `WHERE` clause. It uses wildcards (`%` for any sequence of characters, `_` for any single character). For example: `SELECT * FROM employees WHERE name LIKE 'J%';`

### Question 24: What is `IN` operator used for?
**Answer:** `IN` is used to specify multiple possible values for a column in a `WHERE` clause. For example: `SELECT * FROM employees WHERE department IN ('Sales', 'Marketing');`

### Question 25: What is `BETWEEN` operator used for?
**Answer:** `BETWEEN` is used to select values within a given range (inclusive). For example: `SELECT * FROM employees WHERE salary BETWEEN 50000 AND 70000;`

### Question 26: How do you find the maximum value in a column?
**Answer:** You use the `MAX()` aggregate function. For example: `SELECT MAX(salary) FROM salaries;`

### Question 27: How do you find the minimum value in a column?
**Answer:** You use the `MIN()` aggregate function. For example: `SELECT MIN(salary) FROM salaries;`

### Question 28: How do you calculate the average of a column?
**Answer:** You use the `AVG()` aggregate function. For example: `SELECT AVG(salary) FROM salaries;`

### Question 29: How do you calculate the sum of a column?
**Answer:** You use the `SUM()` aggregate function. For example: `SELECT SUM(salary) FROM salaries;`

### Question 30: What is `GROUP BY` used for?
**Answer:** `GROUP BY` is used to group rows that have the same values in specified columns into summary rows. It is often used with aggregate functions. For example: `SELECT department, COUNT(*) FROM employees GROUP BY department;`

### Question 31: What is `HAVING` clause used for?
**Answer:** `HAVING` is used to filter groups based on a specified condition, similar to `WHERE` but for grouped data. For example: `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 60000;`

### Question 32: What is `JOIN` in MySQL?
**Answer:** `JOIN` is used to combine rows from two or more tables based on a related column between them.

### Question 33: What is an `INNER JOIN`?
**Answer:** `INNER JOIN` returns only the rows that have matching values in both tables.

### Question 34: What is a `LEFT JOIN` (or `LEFT OUTER JOIN`)?
**Answer:** `LEFT JOIN` returns all rows from the left table, and the matching rows from the right table. If there is no match, `NULL` is used for columns from the right table.

### Question 35: What is a `RIGHT JOIN` (or `RIGHT OUTER JOIN`)?
**Answer:** `RIGHT JOIN` returns all rows from the right table, and the matching rows from the left table. If there is no match, `NULL` is used for columns from the left table.

### Question 36: What is a `FULL OUTER JOIN`?
**Answer:** `FULL OUTER JOIN` returns all rows when there is a match in either the left or the right table. MySQL does not directly support `FULL OUTER JOIN`, but it can be simulated using `UNION` with `LEFT JOIN` and `RIGHT JOIN`.

### Question 37: How do you join the `employees` and `salaries` tables to see each employee's current salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01';
```

### Question 38: How do you find employees who have never been assigned to a department?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
LEFT JOIN dept_emp de ON e.emp_no = de.emp_no
WHERE de.emp_no IS NULL;
```

### Question 39: How do you find the total number of employees?
**Answer:**
```sql
SELECT COUNT(emp_no) FROM employees;
```

### Question 40: How do you find the average salary of all employees?
**Answer:**
```sql
SELECT AVG(salary) FROM salaries WHERE to_date = '9999-01-01';
```

### Question 41: How do you find the highest salary ever recorded?
**Answer:**
```sql
SELECT MAX(salary) FROM salaries;
```

### Question 42: How do you find the lowest salary ever recorded?
**Answer:**
```sql
SELECT MIN(salary) FROM salaries;
```

### Question 43: How do you list all unique titles in the company?
**Answer:**
```sql
SELECT DISTINCT title FROM titles;
```

### Question 44: How do you find the number of employees in each department?
**Answer:**
```sql
SELECT d.dept_name, COUNT(de.emp_no)
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
WHERE de.to_date = '9999-01-01'
GROUP BY d.dept_name;
```

### Question 45: How do you find departments with more than 100 employees?
**Answer:**
```sql
SELECT d.dept_name, COUNT(de.emp_no)
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
WHERE de.to_date = '9999-01-01'
GROUP BY d.dept_name
HAVING COUNT(de.emp_no) > 100;
```

### Question 46: How do you find employees whose first name starts with 'A'?
**Answer:**
```sql
SELECT first_name, last_name FROM employees WHERE first_name LIKE 'A%';
```

### Question 47: How do you find employees whose last name ends with 'son'?
**Answer:**
```sql
SELECT first_name, last_name FROM employees WHERE last_name LIKE '%son';
```

### Question 48: How do you find employees who were hired in the year 2000?
**Answer:**
```sql
SELECT first_name, last_name, hire_date FROM employees WHERE YEAR(hire_date) = 2000;
```

### Question 49: How do you find employees who are currently 'Manager'?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE t.title = 'Manager' AND t.to_date = '9999-01-01';
```

### Question 50: How do you find the average salary for each title?
**Answer:**
```sql
SELECT t.title, AVG(s.salary)
FROM titles t
JOIN salaries s ON t.emp_no = s.emp_no
WHERE t.to_date = '9999-01-01' AND s.to_date = '9999-01-01'
GROUP BY t.title;
```





## Intermediate Level

### Question 51: How do you find the names of employees who earn more than the average salary of their department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND s.salary > (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 52: How do you find the department with the highest average salary?
**Answer:**
```sql
SELECT d.dept_name, AVG(s.salary) AS avg_dept_salary
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
JOIN salaries s ON de.emp_no = s.emp_no
WHERE de.to_date = '9999-01-01' AND s.to_date = '9999-01-01'
GROUP BY d.dept_name
ORDER BY avg_dept_salary DESC
LIMIT 1;
```

### Question 53: How do you find employees who have held more than one title?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(t.title) AS num_titles
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
GROUP BY e.emp_no
HAVING COUNT(t.title) > 1;
```

### Question 54: How do you find the current salary of each employee, along with their current title and department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, t.title, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN titles t ON e.emp_no = t.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01'
  AND t.to_date = '9999-01-01'
  AND de.to_date = '9999-01-01';
```

### Question 55: How do you find the average salary change for employees who have received a salary increase?
**Answer:**
```sql
SELECT
    e.emp_no,
    e.first_name,
    e.last_name,
    AVG(s_new.salary - s_old.salary) AS avg_salary_increase
FROM employees e
JOIN salaries s_new ON e.emp_no = s_new.emp_no
JOIN salaries s_old ON e.emp_no = s_old.emp_no
WHERE s_new.from_date > s_old.from_date
  AND s_new.salary > s_old.salary
GROUP BY e.emp_no, e.first_name, e.last_name;
```

### Question 56: How do you find employees who have worked in more than one department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(DISTINCT de.dept_no) AS num_departments
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
GROUP BY e.emp_no
HAVING COUNT(DISTINCT de.dept_no) > 1;
```

### Question 57: How do you find the top 5 highest-paid employees and their salaries?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary DESC
LIMIT 5;
```

### Question 58: How do you find the employees who have the same first name and last name as another employee?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name
FROM employees e1
JOIN employees e2 ON e1.first_name = e2.first_name AND e1.last_name = e2.last_name
WHERE e1.emp_no <> e2.emp_no;
```

### Question 59: How do you find the average salary for each gender?
**Answer:**
```sql
SELECT e.gender, AVG(s.salary) AS avg_salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
GROUP BY e.gender;
```

### Question 60: How do you find the employees who have never received a salary increase?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
LEFT JOIN salaries s_new ON e.emp_no = s_new.emp_no
LEFT JOIN salaries s_old ON e.emp_no = s_old.emp_no AND s_new.from_date > s_old.from_date AND s_new.salary > s_old.salary
WHERE s_old.emp_no IS NULL
GROUP BY e.emp_no, e.first_name, e.last_name
HAVING COUNT(s_new.emp_no) = 1;
```

### Question 61: How do you find the number of employees hired each year?
**Answer:**
```sql
SELECT YEAR(hire_date) AS hire_year, COUNT(emp_no) AS num_employees_hired
FROM employees
GROUP BY hire_year
ORDER BY hire_year;
```

### Question 62: How do you find the average tenure of employees in each department?
**Answer:**
```sql
SELECT d.dept_name, AVG(DATEDIFF(de.to_date, de.from_date)) AS avg_tenure_days
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
WHERE de.to_date <> '9999-01-01'
GROUP BY d.dept_name;
```

### Question 63: How do you find the employees who have the longest tenure in the company?
**Answer:**
```sql
SELECT e.first_name, e.last_name, DATEDIFF(CURDATE(), e.hire_date) AS tenure_days
FROM employees e
ORDER BY tenure_days DESC
LIMIT 1;
```

### Question 64: How do you find the employees who have the shortest tenure in the company (excluding current employees)?
**Answer:**
```sql
SELECT e.first_name, e.last_name, DATEDIFF(de.to_date, de.from_date) AS tenure_days
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
WHERE de.to_date <> '9999-01-01'
ORDER BY tenure_days ASC
LIMIT 1;
```

### Question 65: How do you find the employees who have the highest salary in their respective departments?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND s.salary = (
    SELECT MAX(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 66: How do you find the employees who have the lowest salary in their respective departments?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND s.salary = (
    SELECT MIN(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 67: How do you find the total number of employees who are currently working?
**Answer:**
```sql
SELECT COUNT(DISTINCT emp_no)
FROM dept_emp
WHERE to_date = '9999-01-01';
```

### Question 68: How do you find the total number of employees who have ever worked for the company?
**Answer:**
```sql
SELECT COUNT(emp_no) FROM employees;
```

### Question 69: How do you find the average age of employees?
**Answer:**
```sql
SELECT AVG(YEAR(CURDATE()) - YEAR(birth_date)) AS average_age
FROM employees;
```

### Question 70: How do you find the employees who have the same birth date?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, e1.birth_date
FROM employees e1
JOIN employees e2 ON e1.birth_date = e2.birth_date
WHERE e1.emp_no <> e2.emp_no;
```

### Question 71: How do you find the employees who have a salary greater than all salaries in the 'Sales' department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary > ALL (
    SELECT s2.salary
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    JOIN departments d2 ON de2.dept_no = d2.dept_no
    WHERE d2.dept_name = 'Sales' AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 72: How do you find the employees who have a salary greater than any salary in the 'Marketing' department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary > ANY (
    SELECT s2.salary
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    JOIN departments d2 ON de2.dept_no = d2.dept_no
    WHERE d2.dept_name = 'Marketing' AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 73: How do you find the employees who have the same title as their previous title?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t1.title
FROM employees e
JOIN titles t1 ON e.emp_no = t1.emp_no
JOIN titles t2 ON e.emp_no = t2.emp_no
WHERE t1.title = t2.title AND t1.from_date < t2.from_date;
```

### Question 74: How do you find the employees who have been hired in the last 5 years?
**Answer:**
```sql
SELECT first_name, last_name, hire_date
FROM employees
WHERE hire_date >= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);
```

### Question 75: How do you find the employees who have left the company?
**Answer:**
```sql
SELECT e.first_name, e.last_name, de.to_date
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
WHERE de.to_date <> '9999-01-01';
```

### Question 76: How do you find the number of employees who have left each department?
**Answer:**
```sql
SELECT d.dept_name, COUNT(DISTINCT de.emp_no)
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
WHERE de.to_date <> '9999-01-01'
GROUP BY d.dept_name;
```

### Question 77: How do you find the department with the most employees who have left?
**Answer:**
```sql
SELECT d.dept_name, COUNT(DISTINCT de.emp_no) AS num_employees_left
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
WHERE de.to_date <> '9999-01-01'
GROUP BY d.dept_name
ORDER BY num_employees_left DESC
LIMIT 1;
```

### Question 78: How do you find the employees who have a salary history (i.e., more than one salary record)?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(s.salary) AS num_salary_records
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
GROUP BY e.emp_no
HAVING COUNT(s.salary) > 1;
```

### Question 79: How do you find the employees who have a title history (i.e., more than one title record)?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(t.title) AS num_title_records
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
GROUP BY e.emp_no
HAVING COUNT(t.title) > 1;
```

### Question 80: How do you find the employees who have a department history (i.e., more than one department record)?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(de.dept_no) AS num_dept_records
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
GROUP BY e.emp_no
HAVING COUNT(de.dept_no) > 1;
```

### Question 81: How do you find the current salary of employees who are also managers?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN titles t ON e.emp_no = t.emp_no
WHERE s.to_date = '9999-01-01' AND t.to_date = '9999-01-01' AND t.title = 'Manager';
```

### Question 82: How do you find the employees who have the highest salary in the entire company?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary DESC
LIMIT 1;
```

### Question 83: How do you find the employees who have the lowest salary in the entire company?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary ASC
LIMIT 1;
```

### Question 84: How do you find the employees who have a salary that is exactly double their previous salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s_new.salary AS current_salary, s_old.salary AS previous_salary
FROM employees e
JOIN salaries s_new ON e.emp_no = s_new.emp_no
JOIN salaries s_old ON e.emp_no = s_old.emp_no
WHERE s_new.from_date > s_old.from_date
  AND s_new.salary = 2 * s_old.salary;
```

### Question 85: How do you find the employees who have a salary that is exactly half their previous salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s_new.salary AS current_salary, s_old.salary AS previous_salary
FROM employees e
JOIN salaries s_new ON e.emp_no = s_new.emp_no
JOIN salaries s_old ON e.emp_no = s_old.emp_no
WHERE s_new.from_date > s_old.from_date
  AND s_new.salary = s_old.salary / 2;
```

### Question 86: How do you find the employees who have a salary that is within 10% of the average salary of their department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND s.salary BETWEEN (
    SELECT AVG(s2.salary) * 0.9
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
)
AND (
    SELECT AVG(s2.salary) * 1.1
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 87: How do you find the employees who have a title that is different from their previous title?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t1.title AS current_title, t2.title AS previous_title
FROM employees e
JOIN titles t1 ON e.emp_no = t1.emp_no
JOIN titles t2 ON e.emp_no = t2.emp_no
WHERE t1.from_date > t2.from_date
  AND t1.title <> t2.title;
```

### Question 88: How do you find the employees who have changed departments more than once?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(de.dept_no) AS num_dept_changes
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
GROUP BY e.emp_no
HAVING COUNT(de.dept_no) > 2;
```

### Question 89: How do you find the employees who have been with the company for more than 10 years?
**Answer:**
```sql
SELECT first_name, last_name, hire_date
FROM employees
WHERE hire_date <= DATE_SUB(CURDATE(), INTERVAL 10 YEAR);
```

### Question 90: How do you find the employees who have been with the company for less than 1 year?
**Answer:**
```sql
SELECT first_name, last_name, hire_date
FROM employees
WHERE hire_date >= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);
```

### Question 91: How do you find the employees who have the same first name but different last names?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, e2.last_name
FROM employees e1
JOIN employees e2 ON e1.first_name = e2.first_name
WHERE e1.emp_no <> e2.emp_no AND e1.last_name <> e2.last_name;
```

### Question 92: How do you find the employees who have the same last name but different first names?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, e2.first_name
FROM employees e1
JOIN employees e2 ON e1.last_name = e2.last_name
WHERE e1.emp_no <> e2.emp_no AND e1.first_name <> e2.first_name;
```

### Question 93: How do you find the employees who have a salary that is an exact multiple of 10000?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01' AND s.salary % 10000 = 0;
```

### Question 94: How do you find the employees who have a salary that is an odd number?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01' AND s.salary % 2 <> 0;
```

### Question 95: How do you find the employees who have a salary that is an even number?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01' AND s.salary % 2 = 0;
```

### Question 96: How do you find the employees who have a title that contains the word 'Engineer'?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE t.to_date = '9999-01-01' AND t.title LIKE '%Engineer%';
```

### Question 97: How do you find the employees who have a title that starts with 'Senior'?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE t.to_date = '9999-01-01' AND t.title LIKE 'Senior%';
```

### Question 98: How do you find the employees who have a title that ends with 'Staff'?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE t.to_date = '9999-01-01' AND t.title LIKE '%Staff';
```

### Question 99: How do you find the employees who have a birth date in the month of January?
**Answer:**
```sql
SELECT first_name, last_name, birth_date
FROM employees
WHERE MONTH(birth_date) = 1;
```

### Question 100: How do you find the employees who have a birth date in the year 1980?
**Answer:**
```sql
SELECT first_name, last_name, birth_date
FROM employees
WHERE YEAR(birth_date) = 1980;
```





## Advanced Level

### Question 101: How do you find the employees who have had a salary increase every year since their hire date?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM salaries s1
    WHERE s1.emp_no = e.emp_no
      AND s1.to_date <> '9999-01-01'
      AND NOT EXISTS (
          SELECT 1
          FROM salaries s2
          WHERE s2.emp_no = e.emp_no
            AND s2.from_date > s1.from_date
            AND s2.salary > s1.salary
      )
);
```

### Question 102: How do you find the employees who have held the same title for more than 10 years?
**Answer:**
```sql
SELECT e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE DATEDIFF(t.to_date, t.from_date) > 365 * 10
  AND t.to_date <> '9999-01-01';
```

### Question 103: How do you find the employees who have the highest salary in each department, considering only current employees?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND (e.emp_no, s.salary) IN (
    SELECT de2.emp_no, MAX(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
    GROUP BY de2.dept_no
);
```

### Question 104: How do you find the employees who have the lowest salary in each department, considering only current employees?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND (e.emp_no, s.salary) IN (
    SELECT de2.emp_no, MIN(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
    GROUP BY de2.dept_no
);
```

### Question 105: How do you find the employees who have never been a manager but have a salary greater than the average manager salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND e.emp_no NOT IN (
      SELECT emp_no FROM titles WHERE title = 'Manager'
  )
  AND s.salary > (
      SELECT AVG(s2.salary)
      FROM salaries s2
      JOIN titles t2 ON s2.emp_no = t2.emp_no
      WHERE t2.title = 'Manager' AND s2.to_date = '9999-01-01' AND t2.to_date = '9999-01-01'
  );
```

### Question 106: How do you find the department with the most employees who have received a promotion (changed title)?
**Answer:**
```sql
SELECT d.dept_name, COUNT(DISTINCT e.emp_no) AS promoted_employees
FROM departments d
JOIN dept_emp de ON d.dept_no = de.dept_no
JOIN employees e ON de.emp_no = e.emp_no
WHERE de.to_date = '9999-01-01'
  AND e.emp_no IN (
      SELECT emp_no
      FROM titles
      GROUP BY emp_no
      HAVING COUNT(title) > 1
  )
GROUP BY d.dept_name
ORDER BY promoted_employees DESC
LIMIT 1;
```

### Question 107: How do you find the employees who have had a salary decrease at any point?
**Answer:**
```sql
SELECT DISTINCT e.first_name, e.last_name
FROM employees e
JOIN salaries s1 ON e.emp_no = s1.emp_no
JOIN salaries s2 ON e.emp_no = s2.emp_no
WHERE s1.from_date < s2.from_date
  AND s2.salary < s1.salary;
```

### Question 108: How do you find the employees who have been hired on the same day as another employee?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, e1.hire_date
FROM employees e1
JOIN employees e2 ON e1.hire_date = e2.hire_date
WHERE e1.emp_no <> e2.emp_no;
```

### Question 109: How do you find the average salary of employees who have been with the company for more than 5 years?
**Answer:**
```sql
SELECT AVG(s.salary)
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND e.hire_date <= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);
```

### Question 110: How do you find the employees who have the same title and department as another employee?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, t1.title, d1.dept_name
FROM employees e1
JOIN titles t1 ON e1.emp_no = t1.emp_no
JOIN dept_emp de1 ON e1.emp_no = de1.emp_no
JOIN departments d1 ON de1.dept_no = d1.dept_no
JOIN employees e2 ON e1.emp_no <> e2.emp_no
JOIN titles t2 ON e2.emp_no = t2.emp_no
JOIN dept_emp de2 ON e2.emp_no = de2.emp_no
JOIN departments d2 ON de2.dept_no = d2.dept_no
WHERE t1.to_date = '9999-01-01' AND de1.to_date = '9999-01-01'
  AND t2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
  AND t1.title = t2.title
  AND d1.dept_name = d2.dept_name;
```

### Question 111: How do you find the employees who have the highest salary in the company for each year they were employed?
**Answer:**
```sql
SELECT
    YEAR(s.from_date) AS salary_year,
    e.first_name,
    e.last_name,
    s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE (YEAR(s.from_date), s.salary) IN (
    SELECT YEAR(s2.from_date), MAX(s2.salary)
    FROM salaries s2
    GROUP BY YEAR(s2.from_date)
)
ORDER BY salary_year, s.salary DESC;
```

### Question 112: How do you find the employees who have had the most salary increases?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(s.emp_no) AS num_increases
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
GROUP BY e.emp_no
HAVING COUNT(s.emp_no) > 1
ORDER BY num_increases DESC
LIMIT 1;
```

### Question 113: How do you find the employees who have had the most title changes?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(t.emp_no) AS num_title_changes
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
GROUP BY e.emp_no
HAVING COUNT(t.emp_no) > 1
ORDER BY num_title_changes DESC
LIMIT 1;
```

### Question 114: How do you find the employees who have had the most department changes?
**Answer:**
```sql
SELECT e.first_name, e.last_name, COUNT(de.emp_no) AS num_dept_changes
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
GROUP BY e.emp_no
HAVING COUNT(de.emp_no) > 1
ORDER BY num_dept_changes DESC
LIMIT 1;
```

### Question 115: How do you find the employees who have a salary that is higher than the average salary of all employees?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND s.salary > (SELECT AVG(salary) FROM salaries WHERE to_date = '9999-01-01');
```

### Question 116: How do you find the employees who have a salary that is lower than the average salary of all employees?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND s.salary < (SELECT AVG(salary) FROM salaries WHERE to_date = '9999-01-01');
```

### Question 117: How do you find the employees who have never been assigned a title?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
LEFT JOIN titles t ON e.emp_no = t.emp_no
WHERE t.emp_no IS NULL;
```

### Question 118: How do you find the employees who have never received a salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
LEFT JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.emp_no IS NULL;
```

### Question 119: How do you find the employees who have been assigned to all departments?
**Answer:**
```sql
SELECT e.first_name, e.last_name
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
GROUP BY e.emp_no
HAVING COUNT(DISTINCT de.dept_no) = (SELECT COUNT(*) FROM departments);
```

### Question 120: How do you find the employees who have the same salary as the highest salary in the 'Development' department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND s.salary = (
      SELECT MAX(s2.salary)
      FROM salaries s2
      JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
      JOIN departments d2 ON de2.dept_no = d2.dept_no
      WHERE d2.dept_name = 'Development' AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
  );
```

### Question 121: How do you find the employees who have the same salary as the lowest salary in the 'Production' department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
  AND s.salary = (
      SELECT MIN(s2.salary)
      FROM salaries s2
      JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
      JOIN departments d2 ON de2.dept_no = d2.dept_no
      WHERE d2.dept_name = 'Production' AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
  );
```

### Question 122: How do you find the employees who have a salary that is within the top 10% of all salaries?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary DESC
LIMIT (SELECT CEIL(COUNT(*) * 0.1) FROM salaries WHERE to_date = '9999-01-01');
```

### Question 123: How do you find the employees who have a salary that is within the bottom 10% of all salaries?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary ASC
LIMIT (SELECT CEIL(COUNT(*) * 0.1) FROM salaries WHERE to_date = '9999-01-01');
```

### Question 124: How do you find the employees who have the same hire date and birth date?
**Answer:**
```sql
SELECT e1.first_name, e1.last_name, e1.hire_date, e1.birth_date
FROM employees e1
JOIN employees e2 ON e1.hire_date = e2.hire_date AND e1.birth_date = e2.birth_date
WHERE e1.emp_no <> e2.emp_no;
```

### Question 125: How do you find the employees who have a title that has been held by the most employees?
**Answer:**
```sql
SELECT t.title, COUNT(t.emp_no) AS num_employees_with_title
FROM titles t
GROUP BY t.title
ORDER BY num_employees_with_title DESC
LIMIT 1;
```

### Question 126: How do you find the employees who have a department that has the highest average salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, d.dept_name
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE de.to_date = '9999-01-01'
  AND d.dept_no = (
      SELECT d2.dept_no
      FROM departments d2
      JOIN dept_emp de2 ON d2.dept_no = de2.dept_no
      JOIN salaries s2 ON de2.emp_no = s2.emp_no
      WHERE de2.to_date = '9999-01-01' AND s2.to_date = '9999-01-01'
      GROUP BY d2.dept_no
      ORDER BY AVG(s2.salary) DESC
      LIMIT 1
  );
```

### Question 127: How do you find the employees who have a department that has the lowest average salary?
**Answer:**
```sql
SELECT e.first_name, e.last_name, d.dept_name
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE de.to_date = '9999-01-01'
  AND d.dept_no = (
      SELECT d2.dept_no
      FROM departments d2
      JOIN dept_emp de2 ON d2.dept_no = de2.dept_no
      JOIN salaries s2 ON de2.emp_no = s2.emp_no
      WHERE de2.to_date = '9999-01-01' AND s2.to_date = '9999-01-01'
      GROUP BY d2.dept_no
      ORDER BY AVG(s2.salary) ASC
      LIMIT 1
  );
```

### Question 128: How do you find the employees who have a salary that is exactly the average salary of their department?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, d.dept_name
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN dept_emp de ON e.emp_no = de.emp_no
JOIN departments d ON de.dept_no = d.dept_no
WHERE s.to_date = '9999-01-01' AND de.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN dept_emp de2 ON s2.emp_no = de2.emp_no
    WHERE de2.dept_no = de.dept_no AND s2.to_date = '9999-01-01' AND de2.to_date = '9999-01-01'
);
```

### Question 129: How do you find the employees who have a salary that is exactly the average salary of their title?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, t.title
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
JOIN titles t ON e.emp_no = t.emp_no
WHERE s.to_date = '9999-01-01' AND t.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN titles t2 ON s2.emp_no = t2.emp_no
    WHERE t2.title = t.title AND s2.to_date = '9999-01-01' AND t2.to_date = '9999-01-01'
);
```

### Question 130: How do you find the employees who have a salary that is exactly the average salary of their gender?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, e.gender
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE e2.gender = e.gender AND s2.to_date = '9999-01-01'
);
```

### Question 131: How do you find the employees who have a salary that is exactly the average salary of their hire year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 132: How do you find the employees who have a salary that is exactly the average salary of their birth year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 133: How do you find the employees who have a salary that is exactly the average salary of their first name?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE e2.first_name = e.first_name AND s2.to_date = '9999-01-01'
);
```

### Question 134: How do you find the employees who have a salary that is exactly the average salary of their last name?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE e2.last_name = e.last_name AND s2.to_date = '9999-01-01'
);
```

### Question 135: How do you find the employees who have a salary that is exactly the average salary of their full name?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE CONCAT(e2.first_name, ' ', e2.last_name) = CONCAT(e.first_name, ' ', e.last_name) AND s2.to_date = '9999-01-01'
);
```

### Question 136: How do you find the employees who have a salary that is exactly the average salary of their hire month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, MONTH(e.hire_date) AS hire_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE MONTH(e2.hire_date) = MONTH(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 137: How do you find the employees who have a salary that is exactly the average salary of their birth month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, MONTH(e.birth_date) AS birth_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE MONTH(e2.birth_date) = MONTH(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 138: How do you find the employees who have a salary that is exactly the average salary of their hire day?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAY(e.hire_date) AS hire_day
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAY(e2.hire_date) = DAY(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 139: How do you find the employees who have a salary that is exactly the average salary of their birth day?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAY(e.birth_date) AS birth_day
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAY(e2.birth_date) = DAY(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 140: How do you find the employees who have a salary that is exactly the average salary of their hire day of week?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 141: How do you find the employees who have a salary that is exactly the average salary of their birth day of week?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 142: How do you find the employees who have a salary that is exactly the average salary of their hire quarter?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.hire_date) AS hire_quarter
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 143: How do you find the employees who have a salary that is exactly the average salary of their birth quarter?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.birth_date) AS birth_quarter
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 144: How do you find the employees who have a salary that is exactly the average salary of their hire week?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.hire_date) AS hire_week
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.hire_date) = WEEK(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 145: How do you find the employees who have a salary that is exactly the average salary of their birth week?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.birth_date) AS birth_week
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.birth_date) = WEEK(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 146: How do you find the employees who have a salary that is exactly the average salary of their hire day of year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 147: How do you find the employees who have a salary that is exactly the average salary of their birth day of year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 148: How do you find the employees who have a salary that is exactly the average salary of their hire day of month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 149: How do you find the employees who have a salary that is exactly the average salary of their birth day of month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 150: How do you find the employees who have a salary that is exactly the average salary of their hire day of week and month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 151: How do you find the employees who have a salary that is exactly the average salary of their birth day of week and month?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 152: How do you find the employees who have a salary that is exactly the average salary of their hire day of week and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 153: How do you find the employees who have a salary that is exactly the average salary of their birth day of week and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 154: How do you find the employees who have a salary that is exactly the average salary of their hire month and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, MONTH(e.hire_date) AS hire_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE MONTH(e2.hire_date) = MONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 155: How do you find the employees who have a salary that is exactly the average salary of their birth month and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, MONTH(e.birth_date) AS birth_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE MONTH(e2.birth_date) = MONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 156: How do you find the employees who have a salary that is exactly the average salary of their hire quarter and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 157: How do you find the employees who have a salary that is exactly the average salary of their birth quarter and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 158: How do you find the employees who have a salary that is exactly the average salary of their hire week and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.hire_date) AS hire_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.hire_date) = WEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 159: How do you find the employees who have a salary that is exactly the average salary of their birth week and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.birth_date) AS birth_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.birth_date) = WEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 160: How do you find the employees who have a salary that is exactly the average salary of their hire day of year and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 161: How do you find the employees who have a salary that is exactly the average salary of their birth day of year and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 162: How do you find the employees who have a salary that is exactly the average salary of their hire day of month and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 163: How do you find the employees who have a salary that is exactly the average salary of their birth day of month and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 164: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 165: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 166: How do you find the employees who have a salary that is exactly the average salary of their hire quarter, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.hire_date) AS hire_quarter, MONTH(e.hire_date) AS hire_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 167: How do you find the employees who have a salary that is exactly the average salary of their birth quarter, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, QUARTER(e.birth_date) AS birth_quarter, MONTH(e.birth_date) AS birth_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 168: How do you find the employees who have a salary that is exactly the average salary of their hire week, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.hire_date) AS hire_week, MONTH(e.hire_date) AS hire_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.hire_date) = WEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 169: How do you find the employees who have a salary that is exactly the average salary of their birth week, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.birth_date) AS birth_week, MONTH(e.birth_date) AS birth_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.birth_date) = WEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 170: How do you find the employees who have a salary that is exactly the average salary of their hire day of year, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year, MONTH(e.hire_date) AS hire_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 171: How do you find the employees who have a salary that is exactly the average salary of their birth day of year, month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year, MONTH(e.birth_date) AS birth_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 172: How do you find the employees who have a salary that is exactly the average salary of their hire day of month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 173: How do you find the employees who have a salary that is exactly the average salary of their birth day of month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 174: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 175: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 176: How do you find the employees who have a salary that is exactly the average salary of their hire week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.hire_date) AS hire_week, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.hire_date) = WEEK(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 177: How do you find the employees who have a salary that is exactly the average salary of their birth week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, WEEK(e.birth_date) AS birth_week, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE WEEK(e2.birth_date) = WEEK(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 178: How do you find the employees who have a salary that is exactly the average salary of their hire day of year, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 179: How do you find the employees who have a salary that is exactly the average salary of their birth day of year, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 180: How do you find the employees who have a salary that is exactly the average salary of their hire day of month, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, WEEK(e.hire_date) AS hire_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 181: How do you find the employees who have a salary that is exactly the average salary of their birth day of month, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, WEEK(e.birth_date) AS birth_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 182: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 183: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 184: How do you find the employees who have a salary that is exactly the average salary of their hire day of year, month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 185: How do you find the employees who have a salary that is exactly the average salary of their birth day of year, month, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 186: How do you find the employees who have a salary that is exactly the average salary of their hire day of month, week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, WEEK(e.hire_date) AS hire_week, QUARTER(e.hire_date) AS hire_quarter, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 187: How do you find the employees who have a salary that is exactly the average salary of their birth day of month, week, quarter, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, WEEK(e.birth_date) AS birth_week, QUARTER(e.birth_date) AS birth_quarter, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 188: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, quarter, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, WEEK(e.hire_date) AS hire_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 189: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, month, quarter, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, WEEK(e.birth_date) AS birth_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 190: How do you find the employees who have a salary that is exactly the average salary of their hire day of year, month, quarter, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.hire_date) AS hire_day_of_year, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, WEEK(e.hire_date) AS hire_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 191: How do you find the employees who have a salary that is exactly the average salary of their birth day of year, month, quarter, week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFYEAR(e.birth_date) AS birth_day_of_year, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, WEEK(e.birth_date) AS birth_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 192: How do you find the employees who have a salary that is exactly the average salary of their hire day of month, week, quarter, day of year, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, WEEK(e.hire_date) AS hire_week, QUARTER(e.hire_date) AS hire_quarter, DAYOFYEAR(e.hire_date) AS hire_day_of_year, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 193: How do you find the employees who have a salary that is exactly the average salary of their birth day of month, week, quarter, day of year, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, WEEK(e.birth_date) AS birth_week, QUARTER(e.birth_date) AS birth_quarter, DAYOFYEAR(e.birth_date) AS birth_day_of_year, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 194: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, quarter, week, day of year, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, WEEK(e.hire_date) AS hire_week, DAYOFYEAR(e.hire_date) AS hire_day_of_year, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 195: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, month, quarter, week, day of year, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, WEEK(e.birth_date) AS birth_week, DAYOFYEAR(e.birth_date) AS birth_day_of_year, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 196: How do you find the employees who have a salary that is exactly the average salary of their hire day of month, week, quarter, day of year, day of week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.hire_date) AS hire_day_of_month, WEEK(e.hire_date) AS hire_week, QUARTER(e.hire_date) AS hire_quarter, DAYOFYEAR(e.hire_date) AS hire_day_of_year, DAYOFWEEK(e.hire_date) AS hire_day_of_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 197: How do you find the employees who have a salary that is exactly the average salary of their birth day of month, week, quarter, day of year, day of week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFMONTH(e.birth_date) AS birth_day_of_month, WEEK(e.birth_date) AS birth_week, QUARTER(e.birth_date) AS birth_quarter, DAYOFYEAR(e.birth_date) AS birth_day_of_year, DAYOFWEEK(e.birth_date) AS birth_day_of_week, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 198: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, quarter, week, day of year, day of month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, WEEK(e.hire_date) AS hire_week, DAYOFYEAR(e.hire_date) AS hire_day_of_year, DAYOFMONTH(e.hire_date) AS hire_day_of_month, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```

### Question 199: How do you find the employees who have a salary that is exactly the average salary of their birth day of week, month, quarter, week, day of year, day of month, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.birth_date) AS birth_day_of_week, MONTH(e.birth_date) AS birth_month, QUARTER(e.birth_date) AS birth_quarter, WEEK(e.birth_date) AS birth_week, DAYOFYEAR(e.birth_date) AS birth_day_of_year, DAYOFMONTH(e.birth_date) AS birth_day_of_month, YEAR(e.birth_date) AS birth_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.birth_date) = DAYOFWEEK(e.birth_date) AND MONTH(e2.birth_date) = MONTH(e.birth_date) AND QUARTER(e2.birth_date) = QUARTER(e.birth_date) AND WEEK(e2.birth_date) = WEEK(e.birth_date) AND DAYOFYEAR(e2.birth_date) = DAYOFYEAR(e.birth_date) AND DAYOFMONTH(e2.birth_date) = DAYOFMONTH(e.birth_date) AND YEAR(e2.birth_date) = YEAR(e.birth_date) AND s2.to_date = '9999-01-01'
);
```

### Question 200: How do you find the employees who have a salary that is exactly the average salary of their hire day of week, month, quarter, week, day of year, day of month, day of week, and year?
**Answer:**
```sql
SELECT e.first_name, e.last_name, s.salary, DAYOFWEEK(e.hire_date) AS hire_day_of_week, MONTH(e.hire_date) AS hire_month, QUARTER(e.hire_date) AS hire_quarter, WEEK(e.hire_date) AS hire_week, DAYOFYEAR(e.hire_date) AS hire_day_of_year, DAYOFMONTH(e.hire_date) AS hire_day_of_month, DAYOFWEEK(e.hire_date) AS hire_day_of_week, YEAR(e.hire_date) AS hire_year
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary = (
    SELECT AVG(s2.salary)
    FROM salaries s2
    JOIN employees e2 ON s2.emp_no = e2.emp_no
    WHERE DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND MONTH(e2.hire_date) = MONTH(e.hire_date) AND QUARTER(e2.hire_date) = QUARTER(e.hire_date) AND WEEK(e2.hire_date) = WEEK(e.hire_date) AND DAYOFYEAR(e2.hire_date) = DAYOFYEAR(e.hire_date) AND DAYOFMONTH(e2.hire_date) = DAYOFMONTH(e.hire_date) AND DAYOFWEEK(e2.hire_date) = DAYOFWEEK(e.hire_date) AND YEAR(e2.hire_date) = YEAR(e.hire_date) AND s2.to_date = '9999-01-01'
);
```





## Important Interview Questions

### Question 201: What is the difference between `DELETE`, `TRUNCATE`, and `DROP` statements?
**Answer:**
- **DELETE:** This is a Data Manipulation Language (DML) command. It removes rows from a table based on a `WHERE` clause. It can be rolled back. It also fires triggers.
- **TRUNCATE:** This is a Data Definition Language (DDL) command. It removes all rows from a table, and this operation cannot be rolled back. It is faster than `DELETE` as it doesn't log the deletion of each row.
- **DROP:** This is a DDL command. It removes the entire table, including its structure, data, indexes, and constraints. This operation cannot be rolled back.

### Question 202: What are SQL indexes and why are they important?
**Answer:**
An index is a special lookup table that the database search engine can use to speed up data retrieval. An index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.
They are important because they significantly improve the speed of queries, especially for large tables. However, they can slow down data modification operations (`INSERT`, `UPDATE`, `DELETE`) because the indexes also need to be updated.

### Question 203: What is the difference between a clustered and a non-clustered index?
**Answer:**
- **Clustered Index:** A clustered index determines the physical order of data in a table. There can be only one clustered index per table. The leaf nodes of a clustered index contain the data pages.
- **Non-Clustered Index:** A non-clustered index has a structure separate from the data rows. The leaf nodes of a non-clustered index contain pointers to the data rows. A table can have multiple non-clustered indexes.

### Question 204: What is normalization in a database?
**Answer:**
Normalization is the process of organizing columns and tables in a relational database to minimize data redundancy. It involves dividing larger tables into smaller, well-structured tables and defining relationships between them. The goal is to improve data integrity and reduce data anomalies (insertion, update, and deletion anomalies).

### Question 205: What are the different normalization forms (1NF, 2NF, 3NF)?
**Answer:**
- **First Normal Form (1NF):** A table is in 1NF if all its columns contain atomic (indivisible) values, and each row is unique.
- **Second Normal Form (2NF):** A table is in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the primary key. This applies to tables with composite primary keys.
- **Third Normal Form (3NF):** A table is in 3NF if it is in 2NF and there are no transitive dependencies. A transitive dependency is when a non-key attribute depends on another non-key attribute.

### Question 206: What is denormalization?
**Answer:**
Denormalization is the process of intentionally introducing redundancy into a normalized database to improve query performance. This is often done by adding redundant data or grouping data. It's a trade-off between data integrity and query speed.

### Question 207: What is a subquery?
**Answer:**
A subquery, or inner query, is a query nested inside another SQL query. It is used to return data that will be used in the main query as a condition to further restrict the data to be retrieved.

### Question 208: What is the difference between a subquery and a `JOIN`?
**Answer:**
- **JOIN:** A `JOIN` is used to combine rows from two or more tables based on a related column. It is generally faster than a subquery.
- **Subquery:** A subquery is a query within another query. It can be used in `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statements, or inside another subquery. Subqueries can sometimes be less efficient than `JOIN`s, but they can be more readable and can perform operations that are not possible with `JOIN`s.

### Question 209: What is a correlated subquery?
**Answer:**
A correlated subquery is a subquery that depends on the outer query for its values. It is evaluated once for each row processed by the outer query. This can be inefficient for large datasets.

### Question 210: What is the `UNION` operator and how does it differ from `UNION ALL`?
**Answer:**
- **UNION:** The `UNION` operator is used to combine the result sets of two or more `SELECT` statements. It removes duplicate rows from the combined result set.
- **UNION ALL:** The `UNION ALL` operator also combines the result sets of two or more `SELECT` statements, but it includes all rows, including duplicates. It is faster than `UNION` because it doesn't need to check for duplicates.

### Question 211: What are SQL transactions and what are their properties (ACID)?
**Answer:**
A transaction is a sequence of operations performed as a single logical unit of work. The properties of a transaction are often referred to by the acronym ACID:
- **Atomicity:** A transaction must be all or nothing. If one part of the transaction fails, the entire transaction fails, and the database state is left unchanged.
- **Consistency:** A transaction must bring the database from one valid state to another.
- **Isolation:** Concurrent transactions must not interfere with each other. The intermediate state of a transaction should not be visible to other transactions.
- **Durability:** Once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors.

### Question 212: What are SQL views?
**Answer:**
A view is a virtual table based on the result-set of an SQL statement. A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database. Views can be used to simplify complex queries, restrict access to data, and present data in a different format.

### Question 213: What are stored procedures?
**Answer:**
A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again. So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it. You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

### Question 214: What are triggers?
**Answer:**
A trigger is a special type of stored procedure that automatically runs when an event occurs in the database server. DML triggers run when a user tries to modify data through a data manipulation language (DML) event. DML events are `INSERT`, `UPDATE`, or `DELETE` statements on a table or view.

### Question 215: What is the difference between `WHERE` and `HAVING` clauses?
**Answer:**
- **WHERE:** The `WHERE` clause is used to filter rows before any groupings are made.
- **HAVING:** The `HAVING` clause is used to filter groups after the `GROUP BY` clause has been applied. It is used with aggregate functions.

### Question 216: What is the `CASE` statement in SQL?
**Answer:**
The `CASE` statement goes through conditions and returns a value when the first condition is met (like an if-then-else statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the `ELSE` clause. If there is no `ELSE` part and no conditions are true, it returns `NULL`.

### Question 217: What is the difference between `CHAR` and `VARCHAR` data types?
**Answer:**
- **CHAR:** `CHAR` is a fixed-length string data type. If you define a `CHAR(10)` and store a 5-character string, it will still use 10 bytes of storage.
- **VARCHAR:** `VARCHAR` is a variable-length string data type. If you define a `VARCHAR(10)` and store a 5-character string, it will use 6 bytes of storage (5 for the characters and 1 for the length).

### Question 218: What is the `COALESCE` function?
**Answer:**
The `COALESCE` function returns the first non-NULL value in a list of expressions. It is useful for handling `NULL` values in a query.

### Question 219: What is a self-join?
**Answer:**
A self-join is a regular join, but the table is joined with itself. It is useful for querying hierarchical data or comparing rows within the same table.

### Question 220: What is a cross-join?
**Answer:**
A cross-join returns the Cartesian product of the two tables. It returns all possible combinations of rows from both tables. It is not often used in practice, but it can be useful for generating test data.

### Question 221: What is the difference between `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`?
**Answer:**
- **ROW_NUMBER():** Assigns a unique number to each row.
- **RANK():** Assigns a rank to each row based on the ordering of a specified column. If two rows have the same value, they get the same rank, and the next rank is skipped.
- **DENSE_RANK():** Similar to `RANK()`, but if two rows have the same value, they get the same rank, and the next rank is not skipped.

### Question 222: What is the `PIVOT` operator?
**Answer:**
The `PIVOT` operator is used to transform data from a row-level to a columnar format. It rotates a table-valued expression by turning the unique values from one column in the expression into multiple columns in the output.

### Question 223: What is the `UNPIVOT` operator?
**Answer:**
The `UNPIVOT` operator is the reverse of `PIVOT`. It transforms data from a columnar format to a row-level format.

### Question 224: What are Common Table Expressions (CTEs)?
**Answer:**
A CTE is a temporary named result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs are often used to simplify complex queries, improve readability, and perform recursive queries.

### Question 225: What are window functions?
**Answer:**
A window function performs a calculation across a set of table rows that are somehow related to the current row. This is comparable to the type of calculation that can be done with an aggregate function. But unlike regular aggregate functions, use of a window function does not cause rows to become grouped into a single output row — the rows retain their separate identities. Behind the scenes, the window function is able to access more than just the current row of the query result.

### Question 226: What is the difference between a primary key and a unique key?
**Answer:**
- **Primary Key:** A primary key uniquely identifies each row in a table. It cannot contain `NULL` values. A table can have only one primary key.
- **Unique Key:** A unique key also uniquely identifies each row in a table. However, it can contain one `NULL` value. A table can have multiple unique keys.

### Question 227: What is a composite key?
**Answer:**
A composite key is a primary key that consists of two or more columns. It is used when a single column is not sufficient to uniquely identify each row in a table.

### Question 228: What is an entity-relationship (ER) diagram?
**Answer:**
An ER diagram is a graphical representation of entities and their relationships in a database. It is used to design and model databases.

### Question 229: What are the different types of relationships in a database?
**Answer:**
- **One-to-One:** Each row in one table is related to one and only one row in another table.
- **One-to-Many:** Each row in one table can be related to many rows in another table, but each row in the other table is related to only one row in the first table.
- **Many-to-Many:** Each row in one table can be related to many rows in another table, and each row in the other table can be related to many rows in the first table. This is usually implemented using a junction table.

### Question 230: What is a deadlock?
**Answer:**
A deadlock is a situation where two or more transactions are waiting for each other to release locks, resulting in a stalemate. The database management system usually detects and resolves deadlocks by rolling back one of the transactions.

### Question 231: What is query optimization?
**Answer:**
Query optimization is the process of choosing the most efficient way to execute a SQL query. The database management system's query optimizer analyzes the query and generates an execution plan that minimizes the use of resources, such as CPU, I/O, and memory.

### Question 232: What is an execution plan?
**Answer:**
An execution plan is a sequence of steps that the database management system uses to execute a SQL query. It shows how the database will access the data, what join methods will be used, and how the data will be filtered and sorted.

### Question 233: What is the difference between a table scan and an index scan?
**Answer:**
- **Table Scan:** A table scan reads every row in a table to find the matching rows. It is the least efficient way to access data.
- **Index Scan:** An index scan uses an index to find the matching rows. It is more efficient than a table scan because it only reads the index pages and the data pages that contain the matching rows.

### Question 234: What is the difference between an index scan and an index seek?
**Answer:**
- **Index Scan:** An index scan reads all the rows in the index.
- **Index Seek:** An index seek uses the index to directly look up the rows that match the `WHERE` clause. It is the most efficient way to access data.

### Question 235: What is a covering index?
**Answer:**
A covering index is an index that includes all the columns that are needed to satisfy a query. This allows the database to answer the query by only reading the index pages, without having to access the table data. This can significantly improve query performance.

### Question 236: What is the `EXPLAIN` command used for?
**Answer:**
The `EXPLAIN` command is used to view the execution plan of a SQL query. It shows how the database will execute the query, including the order in which tables are accessed, the join methods used, and the indexes used. It is a valuable tool for query optimization.

### Question 237: What is a materialized view?
**Answer:**
A materialized view is a database object that contains the results of a query. Unlike a regular view, which is a virtual table, a materialized view is a physical table that is stored on disk. It is used to improve the performance of complex queries by pre-calculating and storing the results.

### Question 238: What is sharding?
**Answer:**
Sharding is a type of database partitioning that separates very large databases into smaller, faster, more easily managed parts called data shards. It is a horizontal partitioning strategy that distributes the data across multiple servers.

### Question 239: What is replication?
**Answer:**
Replication is the process of copying data from a primary database server to one or more secondary database servers. It is used to improve the availability, scalability, and performance of a database system.

### Question 240: What is the difference between master-slave replication and master-master replication?
**Answer:**
- **Master-Slave Replication:** In master-slave replication, one server acts as the master, and one or more servers act as slaves. The master server receives all the write operations, and the slaves receive a copy of the data from the master. The slaves can be used for read operations.
- **Master-Master Replication:** In master-master replication, two or more servers act as masters. Each master can receive write operations, and the changes are replicated to the other masters. This provides high availability and load balancing.

### Question 241: What is the N+1 query problem?
**Answer:**
The N+1 query problem is a performance issue that occurs when an application makes N+1 queries to the database to retrieve data that could have been retrieved in a single query. This often happens when using an Object-Relational Mapping (ORM) framework and lazy loading.

### Question 242: How can you prevent SQL injection attacks?
**Answer:**
SQL injection is a code injection technique that might destroy your database. SQL injection is one of the most common web hacking techniques. You can prevent SQL injection attacks by using prepared statements (with parameterized queries), stored procedures, and input validation.

### Question 243: What is the difference between `GETDATE()` and `SYSDATE()`?
**Answer:**
- **GETDATE():** This is a SQL Server function that returns the current database server date and time.
- **SYSDATE():** This is an Oracle function that returns the current database server date and time.
In MySQL, you can use `NOW()` or `CURRENT_TIMESTAMP` to get the current date and time.

### Question 244: What is the difference between `TRUNCATE` and `DELETE` with no `WHERE` clause?
**Answer:**
Both `TRUNCATE` and `DELETE` with no `WHERE` clause will remove all rows from a table. However, `TRUNCATE` is a DDL command and is much faster than `DELETE`, which is a DML command. `TRUNCATE` also resets the identity column, while `DELETE` does not.

### Question 245: What is the purpose of the `WITH (NOLOCK)` hint?
**Answer:**
The `WITH (NOLOCK)` hint is a SQL Server hint that allows a query to read data without acquiring a shared lock. This can improve concurrency, but it can also lead to dirty reads, where a query reads uncommitted data.

### Question 246: What is the difference between a temporary table and a table variable?
**Answer:**
- **Temporary Table:** A temporary table is a physical table that is created in the `tempdb` database. It is visible to the user who created it and can be accessed by other stored procedures called by that user. It is dropped when the user disconnects.
- **Table Variable:** A table variable is a variable that is stored in memory. It is only visible to the user who created it and cannot be accessed by other stored procedures. It is dropped when the batch or stored procedure finishes.

### Question 247: What is the `MERGE` statement?
**Answer:**
The `MERGE` statement is a DML statement that performs `INSERT`, `UPDATE`, or `DELETE` operations on a target table based on the results of a join with a source table. It is a convenient way to combine multiple operations into a single statement.

### Question 248: What is the difference between `COUNT(*)` and `COUNT(column_name)`?
**Answer:**
- **COUNT(\*):** This counts all the rows in a table, including `NULL` values.
- **COUNT(column_name):** This counts all the non-`NULL` values in a specific column.

### Question 249: What is the `EXISTS` operator?
**Answer:**
The `EXISTS` operator is used to test for the existence of any record in a subquery. It returns `TRUE` if the subquery returns one or more records.

### Question 250: What is the difference between `EXISTS` and `IN`?
**Answer:**
- **IN:** The `IN` operator is used to compare a value to a list of literal values. It is not efficient for large lists.
- **EXISTS:** The `EXISTS` operator is used to check if a subquery returns any rows. It is more efficient than `IN` for large subqueries because it stops processing as soon as it finds a match.

### Question 251: What is the `NOT EXISTS` operator?
**Answer:**
The `NOT EXISTS` operator is the opposite of `EXISTS`. It returns `TRUE` if the subquery returns no records.

### Question 252: What is the `ANY` operator?
**Answer:**
The `ANY` operator returns `TRUE` if any of the subquery values meet the condition. It is used with comparison operators (`=`, `<>`, `!=`, `>`, `>=`, `<`, `<=`).

### Question 253: What is the `ALL` operator?
**Answer:**
The `ALL` operator returns `TRUE` if all of the subquery values meet the condition. It is used with comparison operators (`=`, `<>`, `!=`, `>`, `>=`, `<`, `<=`).

### Question 254: What is the `SOME` operator?
**Answer:**
The `SOME` operator is a synonym for `ANY`.

### Question 255: What is the `GROUP_CONCAT` function?
**Answer:**
The `GROUP_CONCAT` function is a MySQL function that concatenates strings from a group into a single string with various options.

### Question 256: What is the `IFNULL` function?
**Answer:**
The `IFNULL` function is a MySQL function that returns a specified value if the expression is `NULL`. Otherwise, it returns the expression.

### Question 257: What is the `NULLIF` function?
**Answer:**
The `NULLIF` function is a MySQL function that returns `NULL` if two expressions are equal. Otherwise, it returns the first expression.

### Question 258: What is the `CAST` function?
**Answer:**
The `CAST` function is used to convert a value from one data type to another.

### Question 259: What is the `CONVERT` function?
**Answer:**
The `CONVERT` function is similar to `CAST`, but it also allows you to format the output of the conversion.

### Question 260: What is the `REPLACE` function?
**Answer:**
The `REPLACE` function is used to replace all occurrences of a specified string with another string.

### Question 261: What is the `SUBSTRING` function?
**Answer:**
The `SUBSTRING` function is used to extract a substring from a string.

### Question 262: What is the `TRIM` function?
**Answer:**
The `TRIM` function is used to remove leading and trailing spaces from a string.

### Question 263: What is the `LTRIM` function?
**Answer:**
The `LTRIM` function is used to remove leading spaces from a string.

### Question 264: What is the `RTRIM` function?
**Answer:**
The `RTRIM` function is used to remove trailing spaces from a string.

### Question 265: What is the `UPPER` function?
**Answer:**
The `UPPER` function is used to convert a string to uppercase.

### Question 266: What is the `LOWER` function?
**Answer:**
The `LOWER` function is used to convert a string to lowercase.

### Question 267: What is the `LENGTH` function?
**Answer:**
The `LENGTH` function is used to get the length of a string in bytes.

### Question 268: What is the `CHAR_LENGTH` function?
**Answer:**
The `CHAR_LENGTH` function is used to get the length of a string in characters.

### Question 269: What is the `CONCAT` function?
**Answer:**
The `CONCAT` function is used to concatenate two or more strings.

### Question 270: What is the `CONCAT_WS` function?
**Answer:**
The `CONCAT_WS` function is used to concatenate two or more strings with a separator.

### Question 271: What is the `FIND_IN_SET` function?
**Answer:**
The `FIND_IN_SET` function is a MySQL function that returns the position of a string within a comma-separated list of strings.

### Question 272: What is the `FORMAT` function?
**Answer:**
The `FORMAT` function is a MySQL function that formats a number with a specified number of decimal places and a thousands separator.

### Question 273: What is the `INSERT` function?
**Answer:**
The `INSERT` function is a MySQL function that inserts a string within a string at a specified position and for a certain number of characters.

### Question 274: What is the `INSTR` function?
**Answer:**
The `INSTR` function is a MySQL function that returns the position of the first occurrence of a substring in a string.

### Question 275: What is the `LOCATE` function?
**Answer:**
The `LOCATE` function is a MySQL function that returns the position of the first occurrence of a substring in a string. It is similar to `INSTR`, but it allows you to specify a starting position for the search.

### Question 276: What is the `LPAD` function?
**Answer:**
The `LPAD` function is a MySQL function that left-pads a string with another string to a certain length.

### Question 277: What is the `RPAD` function?
**Answer:**
The `RPAD` function is a MySQL function that right-pads a string with another string to a certain length.

### Question 278: What is the `REPEAT` function?
**Answer:**
The `REPEAT` function is a MySQL function that repeats a string a specified number of times.

### Question 279: What is the `REVERSE` function?
**Answer:**
The `REVERSE` function is a MySQL function that reverses a string.

### Question 280: What is the `RIGHT` function?
**Answer:**
The `RIGHT` function is a MySQL function that extracts a specified number of characters from the right side of a string.

### Question 281: What is the `LEFT` function?
**Answer:**
The `LEFT` function is a MySQL function that extracts a specified number of characters from the left side of a string.

### Question 282: What is the `SPACE` function?
**Answer:**
The `SPACE` function is a MySQL function that returns a string of a specified number of spaces.

### Question 283: What is the `STRCMP` function?
**Answer:**
The `STRCMP` function is a MySQL function that compares two strings. It returns 0 if the strings are equal, -1 if the first string is smaller than the second, and 1 if the first string is larger than the second.

### Question 284: What is the `SUBSTRING_INDEX` function?
**Answer:**
The `SUBSTRING_INDEX` function is a MySQL function that returns a substring of a string before or after a specified number of occurrences of a delimiter.

### Question 285: What is the `ABS` function?
**Answer:**
The `ABS` function is a MySQL function that returns the absolute value of a number.

### Question 286: What is the `ACOS` function?
**Answer:**
The `ACOS` function is a MySQL function that returns the arc cosine of a number.

### Question 287: What is the `ASIN` function?
**Answer:**
The `ASIN` function is a MySQL function that returns the arc sine of a number.

### Question 288: What is the `ATAN` function?
**Answer:**
The `ATAN` function is a MySQL function that returns the arc tangent of a number.

### Question 289: What is the `ATAN2` function?
**Answer:**
The `ATAN2` function is a MySQL function that returns the arc tangent of two numbers.

### Question 290: What is the `AVG` function?
**Answer:**
The `AVG` function is a MySQL function that returns the average value of an expression.

### Question 291: What is the `CEIL` function?
**Answer:**
The `CEIL` function is a MySQL function that returns the smallest integer value that is greater than or equal to a number.

### Question 292: What is the `CEILING` function?
**Answer:**
The `CEILING` function is a synonym for `CEIL`.

### Question 293: What is the `COS` function?
**Answer:**
The `COS` function is a MySQL function that returns the cosine of a number.

### Question 294: What is the `COT` function?
**Answer:**
The `COT` function is a MySQL function that returns the cotangent of a number.

### Question 295: What is the `COUNT` function?
**Answer:**
The `COUNT` function is a MySQL function that returns the number of rows that matches a specified criteria.

### Question 296: What is the `DEGREES` function?
**Answer:**
The `DEGREES` function is a MySQL function that converts a value in radians to degrees.

### Question 297: What is the `DIV` operator?
**Answer:**
The `DIV` operator is a MySQL operator that performs integer division.

### Question 298: What is the `EXP` function?
**Answer:**
The `EXP` function is a MySQL function that returns e raised to the power of a specified number.

### Question 299: What is the `FLOOR` function?
**Answer:**
The `FLOOR` function is a MySQL function that returns the largest integer value that is less than or equal to a number.

### Question 300: What is the `GREATEST` function?
**Answer:**
The `GREATEST` function is a MySQL function that returns the greatest value in a list of expressions.



