
# "GROUP BY" command

## Aggregate Functions
-  In SQL, aggregate functions are used to perform calculations on multiple rows of a table and return a single value. Here are the most commonly used aggregate functions:

![Aggregate Functions](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-08-53.png)

| Function        | Description                          | Example                                 |
|-----------------|--------------------------------------|-----------------------------------------|
| **COUNT()**     | Counts the number of rows            | `SELECT COUNT(*) FROM employees;`       |
| **SUM()**       | Returns the sum of a numeric column   | `SELECT SUM(salary) FROM employees;`    |
| **AVG()**       | Returns the average value of a column | `SELECT AVG(salary) FROM employees;`    |
| **MAX()**       | Returns the maximum value            | `SELECT MAX(salary) FROM employees;`    |
| **MIN()**       | Returns the minimum value            | `SELECT MIN(salary) FROM employees;`    |
| **STRING_AGG()**   | Concatenates values with delimiter  | `SELECT STRING_AGG(name, ', ') FROM employees;` |

- Some aggregate function may give a long decimal value in return so in order to limit the digits after deciman use **"ROUND"** command
  ```sql
  ROUND(value,digits after decimal)
  ```

![Aggregate Functions](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-13-05.png)

## "GROUP BY"
- The GROUP BY statement in SQL is used to group rows that have the same values in specified columns into summary rows, like grouping by a particular field and applying aggregate functions such as COUNT(), SUM(), AVG(), etc. It is often used with aggregate functions to perform calculations on groups of rows.
- Syntax

```sql
 SELECT column1, aggregate_function(column2)
 FROM table_name 
 WHERE condition GROUP BY column1;
 ```
 ### Examples- GROUP BY
 - Ques 1) Find the Amount spent per customer
 ```sql
 SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) ASC
 ```

![Examples- GROUP BY](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-28-16.png)

- Ques 2) Find the top 5 customers by numbers of orders they have placed
```sql
SELECT customer_id, COUNT(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5
```

![Examples- GROUP BY](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-30-33.png)

- Ques 3) Find the amount each customer has spent per staff member of the rental shop
```sql
SELECT customer_id,staff_id, SUM(amount) FROM payment
GROUP by staff_id,customer_id
ORDEr BY customer_id ASC, staff_id ASC
```
![Examples- GROUP BY](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-34-17.png)

Ques 4) We want to know the revenue generated each day. So order the dates based on revenue generated
```sql
SELECT DATE(payment_date),SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) ASC
``` 
![Examples- GROUP BY](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-40-13.png)

## ⚔️ Group BY challenge

- Ques 1) We have 2 staff members, with staff id 1 and 2. We want to give a bonus to the staff member that handled the most payments [Most in terms of number of payment processed, not total dollar amount]. How many payments did each staff memeber handle and who gets the bonus.

```sql
SELECT staff_id,COUNT(amount) FROM payment
GROUP BY staff_id 
ORDER BY staff_id DESC
```
![⚔️ Group BY challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-46-38.png)

- Ques 2) Corporate HQ is connducting a study on the relationship between replacement cost and a movie MPAA rating. what is the average replacement cost per MPAA rating?

```sql
SELECT rating,ROUND(AVG(replacement_cost),3) FROM film
GROUP BY rating
ORDER BY ROUND(AVG(replacement_cost),3) DESC
```
![⚔️ Group BY challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-50-12.png)

- Ques 3) we are running a promotion to reward our top 5 customers with coupons. what are the customer_ids of the top 5 customers by total spend

```sql
SELECT customer_id,SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5;
```
![⚔️ Group BY challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-12-55-18.png)

## "Having" clause
- The HAVING clause in SQL is used to filter the results of a GROUP BY query based on aggregate functions. It's similar to the WHERE clause, but HAVING is used after grouping, while WHERE is used before grouping.
```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

### Key Differences Between WHERE and HAVING:
- WHERE: Filters rows before the grouping.
  - Therefore we cannot use the WHERE clause after an **aggregate function** because WHERE filters rows before any grouping or aggregation takes place.
- HAVING: Filters groups after the grouping.

## Note: you cannot use the HAVING clause after the ORDER BY clause in the same query
!["Having" clause](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-13-06-00.png)

## ⚔️ HAVING challenge
- Ques 1) we are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments. What customer_ids are eligible for platinum status
```sql
SELECT customer_id,COUNT(*) FROM payment
GROUP BY customer_id
HAVING COUNT(*)>=40
ORDER BY COUNT(*) DESC
```
![⚔️ HAVING challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-13-13-22.png)

- Ques 2) what are the customer ids of customers who have spent more than $100 in payment transactions with our staff_id member 2?

### Method: 1
```sql
SELECT customer_id,staff_id,SUM(amount) FROM payment
GROUP BY customer_id,staff_id
HAVING SUM(amount)>100 AND staff_id=2
ORDER BY SUM(amount) DESC;
```

![⚔️ HAVING challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-13-16-52.png)

### Method: 2
```sql
SELECT customer_id,SUM(amount) FROM payment
WHERE staff_id =2
GROUP BY Customer_id
HAVING SUM(amount)>100
ORDER BY SUM(amount) DESC
```
![⚔️ HAVING challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-13-18-51.png)

