# Assesment TEST-1
1. Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2. 
    ```sql
    SELECT customer_id, SUM(amount) FROM payment
    WHERE staff_id=2
    GROUP BY customer_id
    HAVING SUM(amount)>=110
    ORDER BY SUM(amount) DESC;
    ```
    ![Assesment TEST-1](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-16-17-39.png)

2. How many films begin with the letter J?

  ```sql
  SELECT COUNT(*) FROM film
  WHERE title LIKE 'J%'
  ```
  ![Assesment TEST-1](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-16-22-15.png)

3. What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?

```sql
SELECT first_name,last_name FROM customer
WHERE first_name LIKE 'E%' AND address_id <500
ORDER BY customer_id DESC
LIMIT 1;
```
![Assesment TEST-1](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-16-25-45.png)

