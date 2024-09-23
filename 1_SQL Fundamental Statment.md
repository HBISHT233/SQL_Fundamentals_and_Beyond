
# SQL Fundamental Statment
## 1. "SELECT" command
- Syntax: ```SELECT <column_name> FROM <Table_Name>```
  - Note: you can add multiple columns names in it separated by Commas
  - e.g. ```SELECT c1,c3 FROM films;```
 !["SELECT" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-14-14.png)
- Using '*' in place of coulmn name will select all columns

!["SELECT" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-10-44.png)

## ⚔️ Challenge "SELECT"
- Ques) We want to send a promotional email to our exisiting customers. Select first and last names of every customer and theri email address

  - **Solution)** ```SELECT first_name,last_name,email FROM customer;```
  
  ![⚔️ Challenge "SELECT"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-20-48.png)

## 2. "SELECT DISTINCT" command
- The SELECT DISTINCT command in SQL is used to retrieve unique values from a specific column or a combination of columns in a table. It eliminates duplicate records from the result set.
- Syntax: ```SELECT DISTINCT <Coulumn_name> FROM <Table_name>```

![2. "SELECT DISTINCT" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-29-05.png)

## ⚔️ Challenge "SELECT DISTINCT"
- Ques)We want to know the types of movie ratings we have in our database?

  - **Solution)** ```SELECT DISTINCT rating FROM film;```
    
  ![⚔️ Challenge "SELECT DISTINCT"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-32-44.png)

## 3. "Count"
-  Returns the number of input rows that matches a specific Query Condition
- Syntax: ```SELECT COUNT(name) FROM table```
  
![3. "Count"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-47-23.png)
  - Note: **"()"** is must while using COUNT command
    
  ![3. "Count"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-50-55.png)
- One specific use case of COUNT is to **<u>*count Non-NULL Values in a Specific Column*</u>**
  - ```SELECT COUNT(column_name) FROM table``` Will return the count of Non-NULL

## 4. "SELECT WHERE" command
-  The SELECT WHERE command in SQL is used to retrieve specific data from a database based on a condition. The WHERE clause filters the records returned by the SELECT statement, so that only rows meeting the specified condition are included in the result.
![4. "SELECT WHERE" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-38-22.png)

- You can use comarison operaotrs as well as logical operators with the where command
![4. "SELECT WHERE" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-23-23-59-27.png)
  - **Note: In SQL, the equality operator is a single = instead of ==, which is used in many programming languages like C, C++, and Java.** 

  ![](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-00-01-43.png)
  ![](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-00-40-40.png)

## ⚔️ Challenge "SELECT WHERE"
- Ques 1) A customer forgot their wallet at our store! we need to track down their email to inform them. What is the email for the customer with the name Nancy Thomas?
  - **Solution)** ```SELECT email FROM customer WHERE first_name = 'Nancy' AND last_name='Thomas'```
![⚔️ Challenge "SELECT WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-00-47-56.png) 

- Ques 2) A customer wants more info about the movie "Outlaw Hanky"
  - **Solution)** ```SELECT description FROM film WHERE title='Outlaw Hanky'```
  ![⚔️ Challenge "SELECT WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-00-50-44.png)

- Ques 3) A customer is late on their movie return, and we've mailed them a letter to their address at '295 Ipoh Drive'. We should call them on phone as well, so retrieve his phone number
  - **Solution)** ```SELECT phone FROM address WHERE address = '259 Ipoh Drive'```
![⚔️ Challenge "SELECT WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-00-57-37.png)

## 5. "ORDER BY" command
- The ORDER BY command in SQL is used to sort the result set of a query by one or more columns. You can specify the sort order as ascending (ASC) or descending (DESC).
- 
![5. "ORDER BY" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-01-29.png)
- We can also add more than one column for sorting order
  - e.g. we are here first sorting by store_id and then by last_name
      - ```SELECT * FROM customer ORDER BY store_id ASC,last_name ASC;```
        
![5. "ORDER BY" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-06-21.png)

## 6. "LIMIT" command
- The LIMIT command in SQL is used to specify the maximum number of rows that a query should return. It's commonly used to limit results for performance reasons or to paginate data.
  - ```SELECT * FROM payment ORDER BY payment_date DESC LIMIT 5;```
    
![6. "LIMIT" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-14-16.png)

## ⚔️ Challenge "WHERE"
- Ques1 ) we want to reward our first 10 paying customers, what are the customer ids of those customers?
  - **Solution)** ```SELECT customer_id FROM payment 
WHERE amount !=0.00
ORDER BY payment_date ASC 
LIMIT 10;```

![⚔️ Challenge "WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-18-29.png)

Ques 2) A customer wants to quickly rent a video to watch over their short lunch break. What are the titles of the 5 shortest (runtime) movies?
  - **Solution)** ```SELECT title,length FROM film
ORDER BY length ASC
LIMIT 5;```

  ![⚔️ Challenge "WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-22-04.png)

Ques 3) If the previous customer can watch any movie that is 50 minutes or less in run time, how many options does he have?
  - **Solution)**```SELECT COUNT(*) FROM film
WHERE length<=50```

  ![⚔️ Challenge "WHERE"](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-27-13.png)

## 7. "BETWEEN" command
- Syntax ```SELECT column1, column2, ...FROM table_name WHERE column_name BETWEEN value1 AND value2;```
- Both the upper bound and lower bound are included when using the BETWEEN keyword in SQL. This means that the values specified at both ends of the range are part of the result set.
  
![7. "BETWEEN" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-34-03.png)
-  We can also put date but we need to keep a specific format ```2024-12-31 or YYYY-MM-DD```
  - Note: Date exclude the upper bound
    
![7. "BETWEEN" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-38-04.png)  

## 8. "IN" command
- The IN command in SQL is used to specify multiple values in a WHERE clause. It allows you to filter records based on a list of possible values for a specified column.
  
![8. "IN" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-43-13.png)
- Note: You can also use "NOT IN" to do the iverted operation
  
![8. "IN" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-43-54.png)

![8. "IN" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-45-57.png)

## "LIKE" command
The LIKE operator is case-sensitive and is used with wildcards:

- "%" Represents zero or more characters.
  
  !["LIKE" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-51-12.png)
- "_" Represents a single character
  
!["LIKE" command](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-24-01-58-33.png)

Note: NOT LIKE / NOT ILIKE both are just inverted version of the same
