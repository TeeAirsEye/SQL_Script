# SQL_Script


### 1. **Overview**
The SQL script contains a set of 50 queries aimed at retrieving insights from a sample database, which appears to be related to employee management, covering data like employee names, salaries, departments, job titles, and more. The dataset includes tables such as `countries`, `departments`, `employees`, `jobs`, `locations`, and `regions`. The goal of these queries is to address various questions about employee details, job history, salary ranges, and other employee-related data.

To incorporate the SQL file link into your analysis, you can add a section at the beginning or end of the document that references the file. Here’s how you can integrate it into your existing outline:

---

### **SQL Script Analysis**

#### **Link to SQL Script**
You can access the SQL script containing the queries [here](https://drive.google.com/file/d/12pjIgjmZ9ge29kCNyi5rZV674uAVsabF/view?usp=sharing).


### 2. **Analysis Process**

Below is the process for each question, breaking down the logic and methodology used to derive the results:

---

#### **1. Employees Outside Salary Range ($10,000–$15,000)**

**Objective**: Display names and salaries of employees whose salaries are **not** between $10,000 and $15,000.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, SALARY
FROM employees
WHERE SALARY < 10000 OR SALARY > 15000;
```

**Explanation**:
- The query fetches employee names and salaries where the salary falls outside the range $10,000 to $15,000.
- It uses the condition `SALARY < 10000 OR SALARY > 15000` to exclude salaries in that range.

---

#### **2. Employees in Department 30 or 100**

**Objective**: Display the name and department ID of all employees in departments 30 or 100, sorted by department ID.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, DEPARTMENT_ID
FROM employees
WHERE DEPARTMENT_ID IN (30, 100)
ORDER BY DEPARTMENT_ID ASC;
```

**Explanation**:
- The query filters employees who belong to department IDs 30 or 100 and orders them by department in ascending order.
- The `IN` clause simplifies filtering for multiple values.

---

#### **3. Employees in Departments 30 or 100 with Salary Outside $10,000–$15,000**

**Objective**: Display names and salaries of employees in departments 30 or 100 whose salaries are outside the $10,000–$15,000 range.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, SALARY
FROM employees
WHERE DEPARTMENT_ID IN (30, 100)
AND SALARY NOT BETWEEN 10000 AND 15000;
```

**Explanation**:
- This combines two conditions: employees must belong to departments 30 or 100 and have a salary outside the specified range.
- The `NOT BETWEEN` condition is used to exclude the salary range.

---

#### **4. Employees Hired in 1987**

**Objective**: Retrieve the names and hire dates of all employees hired in 1987.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE
FROM employees
WHERE YEAR(HIRE_DATE) = 1987;
```

**Explanation**:
- The `YEAR()` function extracts the year from the `HIRE_DATE` column, and the query filters only those employees hired in 1987.

---

#### **5. Employees with "b" and "c" in Their First Name**

**Objective**: Display the first names of employees who have both "b" and "c" in their names.

**Query**:
```sql
SELECT FIRST_NAME
FROM employees
WHERE FIRST_NAME LIKE '%b%' AND FIRST_NAME LIKE '%c%';
```

**Explanation**:
- The `LIKE` operator searches for patterns in the `FIRST_NAME` column. The `%` wildcard is used to match any number of characters.
- Both conditions ensure the name contains both letters "b" and "c."

---

#### **6. Employees Who are Programmers or Shipping Clerks, Excluding Certain Salaries**

**Objective**: Display the last name, job, and salary of employees whose job is Programmer or Shipping Clerk and whose salary is not $4,500, $10,000, or $15,000.

**Query**:
```sql
SELECT c.LAST_NAME, j.JOB_TITLE, c.SALARY
FROM employees AS c
LEFT JOIN jobs AS j ON c.JOB_ID = j.JOB_ID
WHERE j.JOB_TITLE IN ('Programmer', 'Shipping Clerk')
AND c.SALARY NOT IN (4500, 10000, 15000);
```

**Explanation**:
- The `LEFT JOIN` combines the `employees` and `jobs` tables to fetch job titles.
- The query filters employees with specific job titles and excludes the specified salaries using `NOT IN`.

---

#### **7. Employees with Exactly 6 Characters in Last Name**

**Objective**: Retrieve the last names of employees whose names have exactly 6 characters.

**Query**:
```sql
SELECT LAST_NAME
FROM employees
WHERE LENGTH(LAST_NAME) = 6;
```

**Explanation**:
- The `LENGTH()` function is used to count the number of characters in the `LAST_NAME` field, and the condition filters for exactly 6 characters.

---

### 3. **Optimization and Efficiency**
Some queries may benefit from indexing the `employees` table on frequently queried columns like `SALARY`, `DEPARTMENT_ID`, and `HIRE_DATE` to improve performance. For complex joins, indexing on foreign keys in both the `employees` and `jobs` tables can also optimize the query execution.

### 4. **Conclusion**
This SQL script addresses a range of business questions involving employee data, with particular focus on salary ranges, department assignments, and hiring periods. The use of joins, filtering conditions, and SQL functions such as `YEAR()` and `LENGTH()` allows the script to extract meaningful insights from the dataset.

### 5. **Recommendations**
- **Indexing**: Add indexes to columns frequently used in `WHERE` conditions (e.g., `SALARY`, `DEPARTMENT_ID`, `HIRE_DATE`) to enhance query performance.
- **Data Validation**: Ensure that all columns (such as `SALARY` and `DEPARTMENT_ID`) are complete and correctly populated, as missing data could skew the results.
- **Further Analysis**: Additional questions could focus on employee retention, performance metrics, and salary trends over time.

---

#### **8. Employees in Departments with High Salaries (Over $100,000)**

**Objective**: Retrieve names and salaries of employees whose salaries exceed $100,000.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, SALARY
FROM employees
WHERE SALARY > 100000;
```

**Explanation**:
- The query filters for employees with a salary greater than $100,000, allowing the organization to identify high earners.

---

#### **9. Count of Employees by Department**

**Objective**: Get the total number of employees in each department.

**Query**:
```sql
SELECT DEPARTMENT_ID, COUNT(*) AS Employee_Count
FROM employees
GROUP BY DEPARTMENT_ID;
```

**Explanation**:
- The `GROUP BY` clause aggregates the employee count by department ID, providing insight into department sizes.

---

#### **10. Employees Hired After a Specific Date**

**Objective**: Retrieve names and hire dates of employees hired after January 1, 2020.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, HIRE_DATE
FROM employees
WHERE HIRE_DATE > '2020-01-01';
```

**Explanation**:
- This query filters employees hired after a specified date, useful for understanding recent hires.

---

#### **11. Highest Salary in Each Department**

**Objective**: Find the highest salary within each department.

**Query**:
```sql
SELECT DEPARTMENT_ID, MAX(SALARY) AS Highest_Salary
FROM employees
GROUP BY DEPARTMENT_ID;
```

**Explanation**:
- The `MAX()` function retrieves the highest salary for each department, helping to identify top earners by department.

---

#### **12. Employees with Specific Job Titles and Salaries Above a Threshold**

**Objective**: List names and salaries of employees with job titles of "Manager" or "Senior Developer" and salaries over $75,000.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME, SALARY
FROM employees
WHERE JOB_ID IN (SELECT JOB_ID FROM jobs WHERE JOB_TITLE IN ('Manager', 'Senior Developer'))
AND SALARY > 75000;
```

**Explanation**:
- The query uses a subquery to filter for specific job titles, combined with a salary threshold, providing insights into high-paying managerial and senior developer roles.

---

#### **13. Average Salary by Job Title**

**Objective**: Calculate the average salary for each job title.

**Query**:
```sql
SELECT j.JOB_TITLE, AVG(e.SALARY) AS Average_Salary
FROM employees e
JOIN jobs j ON e.JOB_ID = j.JOB_ID
GROUP BY j.JOB_TITLE;
```

**Explanation**:
- This query joins the `employees` and `jobs` tables to calculate the average salary for each job title, giving insight into pay scales across different roles.

---

#### **14. Employees with No Manager**

**Objective**: Retrieve names of employees who do not have a manager assigned.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME
FROM employees
WHERE MANAGER_ID IS NULL;
```

**Explanation**:
- This query identifies employees without a manager, potentially flagging them for further review or action regarding team structure.

---

#### **15. Employees with Similar Last Names**

**Objective**: List employees with last names that start with the same letter.

**Query**:
```sql
SELECT LAST_NAME, COUNT(*) AS Name_Count
FROM employees
GROUP BY LAST_NAME
HAVING COUNT(*) > 1;
```

**Explanation**:
- The `HAVING` clause filters for last names that appear more than once, identifying employees with common last names.

---

### **16. Salary Range Analysis**

**Objective**: Analyze the distribution of employee salaries by creating salary ranges.

**Query**:
```sql
SELECT CASE 
           WHEN SALARY < 30000 THEN 'Low'
           WHEN SALARY BETWEEN 30000 AND 60000 THEN 'Medium'
           WHEN SALARY > 60000 THEN 'High'
       END AS Salary_Range,
       COUNT(*) AS Employee_Count
FROM employees
GROUP BY Salary_Range;
```

**Explanation**:
- This query categorizes employees into salary ranges (Low, Medium, High) and counts the number of employees in each range, providing a distribution overview.

---

### **17. Employees by Location**

**Objective**: Count employees by their respective locations.

**Query**:
```sql
SELECT l.CITY, COUNT(e.EMPLOYEE_ID) AS Employee_Count
FROM employees e
JOIN locations l ON e.LOCATION_ID = l.LOCATION_ID
GROUP BY l.CITY;
```

**Explanation**:
- This query counts employees in each city by joining the `employees` and `locations` tables, highlighting workforce distribution across locations.

---

### **18. Employees with Commissions**

**Objective**: Retrieve names of employees who receive commissions.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME
FROM employees
WHERE COMMISSION_PCT IS NOT NULL;
```

**Explanation**:
- The query filters for employees with a non-null `COMMISSION_PCT`, identifying those who earn commissions.

---

### **19. Employees with First Names Starting with a Vowel**

**Objective**: List employees whose first names begin with a vowel.

**Query**:
```sql
SELECT FIRST_NAME, LAST_NAME
FROM employees
WHERE FIRST_NAME REGEXP '^[AEIOUaeiou]';
```

**Explanation**:
- This query uses a regular expression to filter first names starting with a vowel, providing insights into naming patterns.

---

### **20. Job Titles with No Employees**

**Objective**: Identify job titles that currently have no employees assigned.

**Query**:
```sql
SELECT j.JOB_TITLE
FROM jobs j
LEFT JOIN employees e ON j.JOB_ID = e.JOB_ID
WHERE e.EMPLOYEE_ID IS NULL;
```

**Explanation**:
- A `LEFT JOIN` is used to find job titles without employees, helping the organization identify roles that need filling.

---

### **Conclusion of the Current Analysis**

This section of the SQL script further demonstrates the capability to extract valuable insights regarding employee data, salary distributions, hiring trends, and job roles. The use of various SQL functions and techniques, such as `GROUP BY`, `HAVING`, and `JOIN`, enhances the depth of the analysis.

