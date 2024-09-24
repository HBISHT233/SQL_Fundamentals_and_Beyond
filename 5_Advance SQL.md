# Advance SQL
## Timestamps and Extract functionality
In SQL, there are various data types and functions for working with **time** and **date** values. These help in storing, retrieving, and manipulating temporal data like timestamps, dates, or times. Here's an overview of how you can work with them:

### Date and Time Data Types:
1. **DATE**: Stores date values (`YYYY-MM-DD` format).
   - Example: `'2024-09-24'`
   
2. **TIME**: Stores time values (`HH:MM:SS` format).
   - Example: `'08:45:00'`
   
3. **DATETIME / TIMESTAMP**: Stores both date and time values (`YYYY-MM-DD HH:MM:SS` format).
   - Example: `'2024-09-24 08:45:00'`

4. **INTERVAL**: Used to represent a span of time (e.g., days, hours).

### Common Date and Time Functions:

#### 1. **`CURRENT_DATE`**
   - Returns the current date.
   ```sql
   SELECT CURRENT_DATE;
   ```

#### 2. **`CURRENT_TIME`**
   - Returns the current time.
   ```sql
   SELECT CURRENT_TIME;
   ```

#### 3. **`CURRENT_TIMESTAMP` or `NOW()`**
   - Returns the current date and time.
   ```sql
   SELECT CURRENT_TIMESTAMP;
   -- or
   SELECT NOW();
   ```

#### 4. **Extract Parts of Date or Time**
   - You can extract specific parts of a date or time (e.g., year, month, day).
   ```sql
   SELECT EXTRACT(YEAR FROM CURRENT_DATE);   -- Extracts year

   SELECT EXTRACT(QUARTER FROM CURRENT_DATE);-- Extract Quarter
    - SELECT EXTRACT(QUARTER FROM '2024-09-24') AS quarter_number;

   SELECT EXTRACT(MONTH FROM CURRENT_DATE);  -- Extracts month

   SELECT EXTRACT(WEEK FROM CURRENT_DATE);   -- Extarct week
    - - SELECT EXTRACT(WEEK FROM '2024-09-24') AS week_number;

   SELECT EXTRACT(DAY FROM CURRENT_DATE);    -- Extracts day
  
   SELECT EXTRACT(HOUR FROM CURRENT_TIME);   -- Extracts hour
   ```

#### 5. **DATE_ADD / ADDDATE**:
   - Add an interval to a date.
   ```sql
   SELECT DATE_ADD('2024-09-24', INTERVAL 7 DAY);  -- Adds 7 days
   ```

#### 6. **DATE_SUB / SUBDATE**:
   - Subtract an interval from a date.
   ```sql
   SELECT DATE_SUB('2024-09-24', INTERVAL 1 MONTH);  -- Subtracts 1 month
   ```

#### 7. **DATEDIFF**:
   - Calculate the difference between two dates.
   ```sql
   SELECT DATEDIFF('2024-09-24', '2024-09-01');  -- Returns number of days between two dates
   ```

#### 8. **FORMAT Date/Time**
   - You can format dates and times using `DATE_FORMAT()` in MySQL.
   ```sql
   SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s');  -- Formats the date and time
   ```
#### 9. **SHOW TIMEZONE**
  - To show the current time zone you are on
  ```sql
  SHOW TIMEZONE -- return Asia/Calcutta
  ```

#### 10. **Age**
```sql
SELECT AGE(payment_date)
FROM payment
```
![**Age**](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-05-41.png)

### Example Queries:

#### 1. Get the current date:
```sql
SELECT CURRENT_DATE;
```

#### 2. Find all records from the past 30 days:
```sql
SELECT *
FROM orders
WHERE order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 30 DAY);
```

#### 3. Find the difference in days between two dates:
```sql
SELECT DATEDIFF('2024-10-01', '2024-09-24') AS days_difference;
```

#### 4. Retrieve records where the time is after a certain point in the day:
```sql
SELECT *
FROM schedule
WHERE appointment_time > '15:00:00';
```

### TO CHAR
- The TO_CHAR function in SQL is used to convert date, time, and numeric values into a string format. This is especially useful when you want to format dates or numbers in a specific way for display or reporting purposes.
```sql
TO_CHAR(expression, format)
```

```sql
SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD') AS formatted_date
FROM dual;
```
- Example 1
```sql
SELECT TO_CHAR(payment_date,'DD-MM-YYYY')  -- new date format
FROM payment
```
![TO CHAR](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-08-02.png)

- Example 2
```sql
SELECT TO_CHAR(payment_date, 'Month DD, YYYY') AS formatted_order_date
FROM payment;
```
![TO CHAR](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-10-27.png)

### ⚔️ Timestamp and Extract challenge
Ques 1) During which months did payments occurs and format the answer to return back the full month name
```sql
SELECT DISTINCT (TO_CHAR(payment_date,'Month')) FROM payment
```
![TO CHAR](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-16-02.png)

Ques 2) How many payment did occur on monday

Solution: 1
```sql
SELECT COUNT(*) FROM payment
WHERE EXTRACT(dow FROM payment_date)=1
```
- dow =  day of the week
0 = Sunday
1 = Monday
2 = Tuesday and so on

Solution: 2
```sql
SELECT COUNT(*)
FROM payment
WHERE TO_CHAR(payment_date, 'D') = '2';
```
1 = Sunday
2 = Monday
3 = Tuesday
4 = Wednesday
5 = Thursday
6 = Friday

### Mathematical function
```sql
SELECT title,rental_rate,
replacement_cost,
ROUND(rental_rate*100/replacement_cost,2) AS Rental_percentage
FROM film
ORDER BY ROUND(rental_rate*100/replacement_cost,2) DESC

```
![Mathematical function](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-34-04.png)

### String Functions  
#### Common SQL String Functions

1. **`LENGTH` / `LEN`**
   - **Description**: Returns the length of a string.
   - **Syntax**:
     - PostgreSQL/Oracle: `LENGTH(string)`
     - SQL Server: `LEN(string)`
   - **Example**:
     ```sql
     SELECT LENGTH('Hello') AS length;  -- Returns 5 in PostgreSQL/Oracle
     SELECT LEN('Hello') AS length;     -- Returns 5 in SQL Server
     ```

2. **`UPPER` / `LOWER`**
   - **Description**: Converts a string to upper or lower case.
   - **Syntax**:
     - `UPPER(string)`
     - `LOWER(string)`
   - **Example**:
     ```sql
     SELECT UPPER('hello') AS upper_case;  -- Returns 'HELLO'
     SELECT LOWER('HELLO') AS lower_case;  -- Returns 'hello'
     ```

3. **`SUBSTRING` / `SUBSTR`**
   - **Description**: Extracts a substring from a string.
   - **Syntax**:
     - PostgreSQL: `SUBSTRING(string FROM start FOR length)`
     - MySQL: `SUBSTR(string, start, length)`
     - SQL Server: `SUBSTRING(string, start, length)`
   - **Example**:
     ```sql
     SELECT SUBSTRING('Hello World', 1, 5) AS substring;  -- Returns 'Hello'
     SELECT SUBSTR('Hello World', 7, 5) AS substring;     -- Returns 'World' (MySQL)
     ```

4. **`TRIM`**
   - **Description**: Removes leading and trailing spaces from a string.
   - **Syntax**:
     - `TRIM(string)`
   - **Example**:
     ```sql
     SELECT TRIM('   Hello World   ') AS trimmed;  -- Returns 'Hello World'
     ```

5. **`REPLACE`**
   - **Description**: Replaces all occurrences of a substring within a string with another substring.
   - **Syntax**:
     - `REPLACE(string, old_substring, new_substring)`
   - **Example**:
     ```sql
     SELECT REPLACE('Hello World', 'World', 'SQL') AS replaced;  -- Returns 'Hello SQL'
     ```

6. **`CONCAT`**
   - **Description**: Concatenates two or more strings together.
   - **Syntax**:
     - `CONCAT(string1, string2, ...)`
   - **Example**:
     ```sql
     SELECT CONCAT('Hello', ' ', 'World') AS concatenated;  -- Returns 'Hello World'
     ```
  - **Example**:
  ```sql
SELECT first_name || ' ' ||last_name,email AS Full_Name FROM customer
```
![String Functions](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-40-07.png)

```sql
SELECT CONCAT(first_name, ' ',last_name),email AS Full_Name FROM customer
```

7. **`CHARINDEX` / `INSTR`**
   - **Description**: Returns the position of a substring within a string.
   - **Syntax**:
     - SQL Server: `CHARINDEX(substring, string)`
     - MySQL: `INSTR(string, substring)`
   - **Example**:
     ```sql
     SELECT CHARINDEX('World', 'Hello World') AS position;  -- Returns 7 (SQL Server)
     SELECT INSTR('Hello World', 'World') AS position;      -- Returns 7 (MySQL)
     ```

8. **`LEFT` / `RIGHT`**
   - **Description**: Returns a specified number of characters from the left or right side of a string.
   - **Syntax**:
     - SQL Server: `LEFT(string, length)` and `RIGHT(string, length)`
   - **Example**:
     ```sql
     SELECT LEFT('Hello', 2) AS left_part;  -- Returns 'He'
     SELECT RIGHT('Hello', 2) AS right_part;  -- Returns 'lo'
     SELECT LOWER(LEFT(first_name,2)) || LOWER(LEFT(last_name,2)) || '@gmail.com' FROM customer
     ```
     ![Common SQL String Functions](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-22-47-49.png)

### subQuery
- A subquery, also known as a nested query or inner query, is a query within another SQL query. Subqueries can be used in various places, such as in the SELECT, FROM, WHERE, or HAVING clauses.

*<u>**Note: Subquery is executed first**</u>*

Example -1
```sql
SELECT customer_id,amount
FROM payment
WHERE amount = (SELECT MAX(amount) FROM payment);
```

Example -2
```sql
SELECT title,rental_rate,replacement_cost 
FROM film
WHERE rental_rate >= (SELECT AVG(rental_rate) FROM film)
ORDER by rental_rate ASC
```

![subQuery](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-25-00-39-59.png)

### EXIST
- The EXISTS operator in SQL is used to test whether a subquery returns any rows. It returns TRUE if the subquery produces any result, and FALSE if it doesn’t return any rows. EXISTS is often used in combination with subqueries, and it is a way to check for the existence of rows that meet a certain

```sql
SELECT customer_id, first_name, last_name
FROM customers
WHERE EXISTS (
    SELECT * 
    FROM orders 
    WHERE customers.customer_id = orders.customer_id);

```

### SELF JOIN 
- A self join is a type of join where a table is joined with itself. This can be useful when you want to compare rows within the same table, such as comparing employees with their managers or finding pairs of related data points.

Note: When using a self join it is necessary to use an alias for the table, otherwise the table names would be ambigious.

```sql
SELECT f1.title,f2.title,f1.length FROM film as f1
INNER JOIN film AS f2 ON
f1.film_id != f2.film_id AND f1.length = f2.length
```
![SELF JOIN ](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-25-01-00-25.png)
