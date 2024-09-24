# "JOIN" command

## "AS" Clause
- In SQL, the AS keyword is used to alias (give a temporary name to) columns or tables in a query. This can make the output more readable, especially when dealing with complex expressions or joins. The alias exists only for the duration of the query.
```sql
SELECT column_name AS alias_name
FROM table_name;
```
!["AS" Clause](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-16-36-11.png)
- **Note: AS operator gets executed at the very end of a query, meaning that we can not use the ALIAS inside WHERE operator**
## JOIN
- In SQL, the JOIN command is used to combine rows from two or more tables based on a related column between them. There are different types of joins, such as INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN, each serving different purposes.
## Types of Joins:
![JOIN](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-19-18-29.png)
  ### 1. INNER JOIN [Intersection]
  - Returns only the rows where there is a match in both tables.
  ```sql
  SELECT table1.column1, table2.column2
  FROM table1
  INNER JOIN table2
  ON table1.common_column = table2.common_column;
```

Note: If the column is unique to only one table only then we dont need to mention tha table name but if both table has a particular column common then we have to define the table from where we want that column to be pulled

![Types of Joins:](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-16-53-56.png)

### 2. FULL OUTER JOIN
-  FULL OUTER JOIN (also called a FULL JOIN) in SQL returns all rows when there is a match in either the left or right table. If there is no match, it will still return rows from both tables, with NULL values in place for the missing matches.
```sql
SELECT column1, column2, ...
FROM table1
FULL OUTER JOIN table2
ON table1.common_column = table2.common_column;
```
![2. FULL OUTER JOIN](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-17-03-57.png)

- FULL OUTER JOIN + WHERE NULL = Opposite(INNER JOIN) = UNIQUE Rows

```sql
SELECT column1, column2, ...
FROM table1
FULL OUTER JOIN table2
ON table1.common_column = table2.common_column;
WHERE table1.common_column IS null OR table2.common_column IS null
```
![2. FULL OUTER JOIN](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-17-11-48.png)
### 3. LEFT JOIN (or LEFT OUTER JOIN)
- Returns all the rows from the left table and the matching rows from the right table. If there’s no match, NULL is returned for the right table’s columns.
```sql
SELECT table1.column1, table2.column2
FROM table1         -- Table 1 will be the left table [since it is mentioned first]
LEFT JOIN table2    -- or you can use "LEFT OUTER JOIN"
ON table1.common_column = table2.common_column;
```

- LEFT OUTER JOIN + WHERE not found in B = Exclusive Table 1
```sql
SELECT * FROM Table1
LEFT OUTER JOIN Table2
ON Table1.col_match = Table2.col_match
WHERE Table2.id is null 
```
- Practice Question
  - What SQL query would you use to retrieve a list of films from the film table that do not have any associated records in the inventory table, ensuring that films without any inventory are identified?

  ```sql
  SELECT film.film_id, title, inventory_id,store_id
  FROM film
  LEFT JOIN inventory
  ON inventory.film_id = film.film_id
  WHERE inventory.film_id IS null
  ```
![3. LEFT JOIN (or LEFT OUTER JOIN)](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-19-37-13.png)


### 4. RIGHT JOIN (or RIGHT OUTER JOIN)
- Returns all the rows from the right table and the matching rows from the left table. If there’s no match, NULL is returned for the left table’s columns.
```sql
SELECT table1.column1, table2.column2
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```
### 5. FULL JOIN (or FULL OUTER JOIN)
- Returns all rows when there is a match in either table. If there’s no match, NULL values are returned from the non-matching table.
```sql
SELECT table1.column1, table2.column2
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

## "UNION" Command
- The UNION command in SQL is used to combine the results of two or more SELECT queries into a single result set. By default, the UNION operator removes duplicate rows from the final result. If you want to include duplicates, you can use UNION ALL.
```sql
SELECT column1, column2, ...
FROM table1
UNION
SELECT column1, column2, ...
FROM table2;
```

## ⚔️ JOIN challenge
- Ques 1) mail every customers who live in california about an upcoming sales there
```sql
SELECT first_name,last_name,district,email FROM customer
INNER JOIN address
ON address.address_id = customer.address_id 
WHERE address.district = 'California'
```
![⚔️ JOIN challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-19-58-19.png)

Ques 2) A customer walks in and is a huge fan of the actor "Nick Wahlberg" and wants to know which movie he is in. Get a list of all of his movies.

```sql
SELECT actor.actor_id,first_name,Last_name,film_actor.film_id,title from actor
INNER JOIN film_actor
ON actor.actor_id = film_actor.actor_id 
INNER JOIN film
ON film_actor.film_id = film.film_id
WHERE first_name='Nick' AND last_name ='Wahlberg'
```
- film [title name, film_id] == actor [actor_id, Name of actor] == film_actor[film_id,actor_id
  - we need 2 join 
  - [1st one to join film_actor and actor based on actor_id which will give us "actor_name" and "film_id"]
  - After than we can use film_id to merge film database to get title names based on film_id
![⚔️ JOIN challenge](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-20-16-48.png)

