# Conditional Expessions and Operators

### CASE

- A **SQL case statement** is used to execute a series of conditional expressions and returns one of the specified results when a condition is true. It is often used to transform data or apply conditional logic directly within SQL queries.
  
  ```sql
  SELECT
    CASE
      WHEN condition1 THEN result1
      WHEN condition2 THEN result2
      ...
      ELSE resultN
    END AS alias_name
  FROM table_name;
  ```

```sql
SELECT 
  employee_name,
  salary,
  CASE
    WHEN salary > 50000 THEN 'High Salary'
    WHEN salary BETWEEN 30000 AND 50000 THEN 'Medium Salary'
    ELSE 'Low Salary'
  END AS salary_category
FROM employees;
```

* You can use `CASE` in `SELECT`, `WHERE`, `ORDER BY`, or even `JOIN` clauses, providing a flexible way to handle conditional logic

### CASE Expression

A **`CASE Expression`** is the **complete evaluation** that happens as part of a SQL query using the `CASE` structure. It’s the term used to describe the result of the `CASE` operation in a query.

```sql
CASE expression -- [Expression here could be a cloumn_name]
  WHEN value1 THEN result1
  WHEN value2 THEN result2
  ...
  ELSE resultN
END


```

```sql
-- CASE
SELECT customer_id,
CASE 
	WHEN (customer_id <=100) THEN 'Premium'
	WHEN (customer_id BETWEEN 100 AND 200) THEN 'Plus'
	ELSE 'Normal'
END
FROM customer
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-11-25-31-image.png)

```sql
-- CASE EXPRESSION
SELECT customer_id,
CASE customer_id
	WHEN 2 THEN 'Winner'
	WHEN 5 THEN 'Runner-up'
	ELSE 'Normal'
END AS Lottery_winner
FROM customer
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-11-29-24-image.png)

* We  can also use CASE statment to count a particular value is repeated how many time

```sql
SELECT 
SUM(CASE rental_rate 
	WHEN 0.99 THEN 1
	ELSE 0
END) AS number_of_bargin
FROM film
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-11-33-16-image.png)

Here we are calculating how many movies are 0.99 the shop has

## ⚔️ CASE Challenge

Ques) we want to know and compare the various amounts of films we have per movie rating. Use CASE and dvd_rental Database

```sql
SELECT
SUM(CASE rating WHEN 'PG-13' THEN 1 ELSE 0 END) AS PG_13,
SUM(CASE rating WHEN 'NC-17' THEN 1 ELSE 0 END) AS NC_17,
SUM(CASE rating WHEN 'R' THEN 1 ELSE 0 END) AS R,
SUM(CASE rating WHEN 'G' THEN 1 ELSE 0 END) AS G,
SUM(CASE rating WHEN 'PG' THEN 1 ELSE 0 END) AS PG
FROM film
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-11-42-47-image.png)

### COALESCE

The **`COALESCE`** function in SQL is used to return the first non-null value from a list of expressions. It's particularly useful for handling null values and providing default values when dealing with potentially missing data.

- It's commonly used for ensuring that queries return meaningful data when nulls are present.  [If you want to perform operation on a column but there are some NULL in it then you can use COALESCE to handle those NULL]

```sql
SELECT 
  employee_id,
  COALESCE(email_address, personal_email, 'No Email Provided') AS email
FROM employees;
```

### CAST

The **`CAST`** function in SQL is used to convert an expression from one data type to another. It is particularly useful when you need to ensure that data types match for operations, comparisons, or for formatting purposes

```sql
SELECT 
  CAST(age AS INTEGER) AS age_integer
FROM users;
```

```sql
SELECT 
  '123'::INTEGER AS converted_integer;
```

Here's a table of the most common data types in PostgreSQL along with their syntax for using the **`CAST`** function:

| **Data Type**        | **CAST Syntax**                            | **Example**                                                           |
| -------------------- | ------------------------------------------ | --------------------------------------------------------------------- |
| **INTEGER**          | `CAST(value AS INTEGER)`                   | `SELECT CAST('42' AS INTEGER) AS integer_value;`                      |
| **BIGINT**           | `CAST(value AS BIGINT)`                    | `SELECT CAST('123456789012345' AS BIGINT) AS big_integer_value;`      |
| **SMALLINT**         | `CAST(value AS SMALLINT)`                  | `SELECT CAST('30000' AS SMALLINT) AS small_integer_value;`            |
| **DECIMAL/NUMERIC**  | `CAST(value AS DECIMAL(precision, scale))` | `SELECT CAST('123.456' AS DECIMAL(5, 3)) AS decimal_value;`           |
| **REAL**             | `CAST(value AS REAL)`                      | `SELECT CAST('3.14' AS REAL) AS real_value;`                          |
| **DOUBLE PRECISION** | `CAST(value AS DOUBLE PRECISION)`          | `SELECT CAST('3.14159' AS DOUBLE PRECISION) AS double_value;`         |
| **VARCHAR**          | `CAST(value AS VARCHAR(length))`           | `SELECT CAST(42 AS VARCHAR(10)) AS varchar_value;`                    |
| **TEXT**             | `CAST(value AS TEXT)`                      | `SELECT CAST(123 AS TEXT) AS text_value;`                             |
| **CHAR**             | `CAST(value AS CHAR(length))`              | `SELECT CAST('A' AS CHAR(1)) AS char_value;`                          |
| **DATE**             | `CAST(value AS DATE)`                      | `SELECT CAST('2024-09-28' AS DATE) AS date_value;`                    |
| **TIME**             | `CAST(value AS TIME)`                      | `SELECT CAST('12:34:56' AS TIME) AS time_value;`                      |
| **TIMESTAMP**        | `CAST(value AS TIMESTAMP)`                 | `SELECT CAST('2024-09-28 10:30:00' AS TIMESTAMP) AS timestamp_value;` |
| **BOOLEAN**          | `CAST(value AS BOOLEAN)`                   | `SELECT CAST('true' AS BOOLEAN) AS boolean_value;`                    |

### NULLIF

* The **`NULLIF`** function in SQL is used to return `NULL` if two expressions are equal. If the expressions are not equal, it returns the first expression. 

* This function can be particularly useful for handling cases where you want to avoid division by zero or when you want to substitute a specific value with `NULL`.

```sql
SELECT 
    salary / NULLIF(bonus, 0) AS adjusted_salary
FROM employees;
-- In this example, if bonus is 0, 
-- the division would return NULL 
-- instead of causing a division by zero error.
```

```sql
-- Conditional Statment using NULLIF
SELECT 
    employee_id,
    CASE 
        WHEN NULLIF(bonus, 0) IS NULL THEN 'No Bonus'
        ELSE 'Bonus Available'
    END AS bonus_status
FROM employees;
```

### VIEWS

In SQL, a **view** is a virtual table that provides a way to present data from one or more tables in a structured format. Views can simplify complex queries, enhance security by restricting access to certain data, and provide a consistent interface to the underlying data.

```sql
-- Let say we have this below query
SELECT first_name,last_name,address FROM customer
INNER JOIN address
ON customer.address_id = address.address_id
```

so instead of writing the query every time we can create a VIEW for it which can be called later directly 

```sql
CREATE VIEW customer_info AS
SELECT first_name,last_name,address FROM customer
INNER JOIN address
ON customer.address_id = address.address_id


-- To call it next time
SELECT * FROM customer_info
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-12-32-57-image.png)

* We can also REPLACE [edit] the VIEW

```sql
CREATE OR REPLACE VIEW customer_info AS
SELECT first_name,last_name,address,district FROM customer
INNER JOIN address
ON customer.address_id = address.address_id

-- we have added a new column "district"
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-12-34-20-image.png)

*  To delete your view

```sql
DROP VIEW IF EXIST customer_info
```

* To change the name of VIEW

```sql
ALTER VIEW customer_info RENAME to c_info
```

![Conditional Expessions and Operators](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-28-12-36-50-image.png)

### ROW_NUMBER()

The **`ROW_NUMBER()`** function is a window function in SQL that assigns a unique sequential integer to rows within a partition of a result set. This function is often used for tasks such as ranking data, paginating results, or identifying duplicates.

```sql
ROW_NUMBER() 
OVER (PARTITION BY column1, column2, ... ORDER BY column_name [ASC|DESC])
AS ranked_columns
```

* The `PARTITION BY` clause divides the result set into partitions to which the `ROW_NUMBER()` function is applied. [optional clause]
  
  * It defines the groups of rows to which the `ROW_NUMBER()` function is applied.

* The `ORDER BY` clause within the `OVER` clause defines the order in which the rows are numbered. [mandatory clause]

Example

```sql
SELECT 
    employee_id,
    first_name,
    last_name,
    department_id,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank
FROM employees;
```

The output will be:

| employee_id | first_name | last_name | department_id | salary | salary_rank |
| ----------- | ---------- | --------- | ------------- | ------ | ----------- |
| 2           | Jane       | Smith     | 1             | 60000  | 1           |
| 1           | John       | Doe       | 1             | 50000  | 2           |
| 5           | Chris      | Davis     | 1             | 45000  | 3           |
| 4           | Mike       | Brown     | 2             | 65000  | 1           |
| 3           | Emily      | Johnson   | 2             | 55000  | 2           |

#### Practice Question

Select the 3rd highest salary of each department and if the department has less than 3 memeber than return the lowest salary

```sql
WITH RankedSalaries AS (
    SELECT 
        department_id,
        salary,
        ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank,
        COUNT(*) OVER (PARTITION BY department_id) AS member_count
    FROM employees
)

SELECT 
    department_id,
    CASE 
        WHEN member_count < 3 THEN MIN(salary)
        ELSE MAX(CASE WHEN salary_rank = 3 THEN salary END)
    END AS salary_value
FROM RankedSalaries
GROUP BY department_id, member_count;

```

The results are grouped by `department_id` and `member_count` to ensure the query returns one row per department.
