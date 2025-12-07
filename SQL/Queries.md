## Queries
1.  Retrieve the names of employees and their department names using INNER JOIN.
```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```
**Explanation:** This query retrieves only the employees who are assigned to a department. It combines rows from employees and departments where the department_id matches in both tables.

2.  Retrieve all employees and their department names. If an employee does not belong to a department, show NULL for the department name.
```sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```
**Explanation**: This query retrieves all employees, including those who are not assigned to a department. For those without a department, the department_name will be NULL.

3.  Get the total salary per department.
```sql
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```
**Explanation**: This query groups the employees by their department and calculates the total salary for each department using the `SUM()` function.

4.  Get departments where the total salary is greater than 100,000.
```sql
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id
HAVING SUM(salary) > 100000;
```
**Explanation**: The HAVING clause filters the results after grouping. In this case, only departments with a total salary greater than 100,000 will be shown.

5.  Retrieve the names of employees who earn more than the average salary in their department.
```sql
SELECT name
FROM employees
WHERE salary > (
 SELECT AVG(salary)
 FROM employees
 WHERE department_id = employees.department_id
);
```
**Explanation**: The subquery calculates the average salary within each department, and the outer query retrieves employees whose salary exceeds that average.

6.   Get a list of all employee names and all department names using UNION.
```sql
SELECT name FROM employees
UNION
SELECT department_name FROM departments;
```
Explanation: The UNION operator combines the results of two queries into a single result set, ensuring that duplicate values are removed. This query retrieves all unique employee names and department names from the respective tables.

7.  Scenario: Given a table employees with data like employee ID, name, and department name, normalize the data into two tables: employees and departments.

***Original table***
```sql
CREATE TABLE employees (
 employee_id INT,
 employee_name VARCHAR(100),
 department_name VARCHAR(100)
);
INSERT INTO employees VALUES (1, 'John', 'HR'), (2, 'Jane', 'IT'), (3, 'Mike', 'HR');
Normalized Table
CREATE TABLE departments (
 department_id INT,
 department_name VARCHAR(100)
);
INSERT INTO departments VALUES (1, 'HR'), (2, 'IT');
CREATE TABLE employees (
 employee_id INT,
 employee_name VARCHAR(100),
 department_id INT,
 FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
INSERT INTO employees VALUES (1, 'John', 1), (2, 'Jane', 2), (3, 'Mike', 1);
```
**Explanation**: The normalization process divides the original table into two: employees and departments. The department_name in employees is replaced with a department_id as a foreign key that references the departments table. This reduces data redundancy.

8.  Retrieve distinct department names from the employees table.
```sql
SELECT DISTINCT department_name
FROM employees;
```
**Explanation**: The `DISTINCT` keyword ensures that only unique department names are returned, even if some departments have multiple employees.

9.  Update the salary of employees in the "IT" department by increasing it by 10%.
```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = (SELECT department_id FROM departments WHERE
department_name = 'IT');
```
**Explanation**: This query uses a subquery to find the department_id for "IT" and then updates the salary of all employees in that department by 10%.

10. Delete employees from the employees table who have a salary less than 30,000.
```sql
DELETE FROM employees
WHERE salary < 30000;
```
**Explanation**: This query deletes all employees whose salary is less than 30,000 from the employees table.

11. Retrieve all employees whose name starts with "J".
```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'J%';
```
**Explanation**: The `LIKE` operator is used for pattern matching. The `%` symbol represents any sequence of characters, so this query returns all employees whose name starts with the letter "J".

12.🟥 Retrieve employees who have the same manager. Assume manager_id is a foreign key referencing employee_id.
```sql
SELECT e1.employee_name AS Employee, e2.employee_name AS Manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.employee_id;
```
**Explanation**: This is an example of a self-join, where a table is joined with itself. In this case, it shows which employees have the same manager by matching `manager_id` in one instance (e1) with `employee_id` in another instance (e2).

13. Create a query that displays the salary category of employees based on their salary.
```sql
SELECT employee_name,
 CASE
 WHEN salary < 30000 THEN 'Low'
 WHEN salary BETWEEN 30000 AND 60000 THEN 'Medium'
 WHEN salary > 60000 THEN 'High'
 ELSE 'Not Defined'
 END AS salary_category
FROM employees;
```
**Explanation**: The `CASE` statement allows you to add conditional logic to SQL queries. In this case, it categorizes employees based on their salary.

14. Retrieve employee names and department names for employees who have a salary greater than 50,000.
```sql
SELECT e.employee_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id
WHERE e.salary > 50000;
```
**Explanation**: This query joins the employees and departments tables and filters employees who have a salary greater than 50,000.

15. Rank employees based on their salary within each department.
```sql
SELECT employee_name, salary, department_id,
 RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank
FROM employees;
```
Explanation: The `RANK()` function assigns a rank to each employee's salary within each department, ordered from highest to lowest salary. The PARTITION BY clause groups the data by department_id.

16. 🟥 To find the second-highest salary from an employee table, you can use the following SQL query:
```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```
17. 🟥 Retrieve all employees and their department names. If an employee does not belong to a department, show NULL for the department name.
```sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```
**Explanation**: This query retrieves all employees, including those who are not assigned to a department. For those without a department, the department_name will be NULL.</br>

18. Query to get duplicate salaries:
```sql
SELECT salary
FROM emp
GROUP BY salary
HAVING COUNT(*) > 1;]
```
19. Employees with duplicate salaries:
```sql
SELECT *
FROM emp
WHERE salary IN (
    SELECT salary
    FROM emp
    GROUP BY salary
    HAVING COUNT(*) > 1
);
```