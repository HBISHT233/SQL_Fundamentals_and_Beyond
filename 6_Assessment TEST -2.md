

# Assessment -2

## Download the Database for this assignment
```
https://drive.google.com/file/d/1wDqIK6zt5twWnCOx97ywipaiWR2d0OfT/view
```
Create a new database and restore the database with this above tar file [For more detailed step please refer the Setup Section of the repo]

### Ques 1) How can you retrieve all the information from the cd.facilities table?
- Since the database has 2 schemas[cd, public] we need to define the schema name along with the table name to retrieve it
```sql
SELECT * FROM cd.facilities
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-41-24.png)

### Ques 2) You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?
```sql
SELECT name,membercost FROM cd.facilities
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-42-57.png)

### Ques 3) How can you produce a list of facilities that charge a fee to members?
```sql
SELECT * FROM cd.facilities
WHERE membercost != 0
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-44-24.png)

### Ques 4) How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.
```sql
SELECT * FROM cd.facilities
WHERE membercost != 0 and membercost < (monthlymaintenance/50)
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-45-58.png)

### Ques 5) How can you produce a list of all facilities with the word 'Tennis' in their name?
```sql
SELECT * FROM cd.facilities
WHERE name LIKE '%Tennis%'
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-49-16.png)

### Ques 6) How can you retrieve the details of facilities with ID 1 and 5? Try to do it without using the OR operator.

```sql
SELECT * FROM cd.facilities
WHERE facid IN (1,5)
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-51-55.png)

### Ques 7) How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.
```sql
SELECT memid, surname, firstname,joindate  FROM cd.members
WHERE Date(joindate) >= '2012-09-01'
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-56-03.png)

### Ques 8) How can you produce an ordered list of the first 10 surnames in the members table? The list must not contain duplicates
```sql
SELECT DISTINCT(surname) FROM cd.members
ORDER BY surname 
LIMIT 10
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-57-59.png)

### Ques 9) You'd like to get the signup date of your last member. How can you retrieve this information?
```sql
SELECT joindate FROM cd.members
ORDER BY joindate DESC
LIMIT 1
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-12-59-51.png)

### Ques 10) Produce a count of the number of facilities that have a cost to guests of 10 or more.
```sql
SELECT COUNT(*) FROM cd.facilities
WHERE guestcost >=10
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-13-01-22.png)

### Ques 11) Produce a list of the total number of slots booked per facility in the month of September 2012. Produce an output table consisting of facility id and slots, sorted by the number of slots.
```sql
SELECT facid, sum(slots) AS "Total Slots" 
FROM cd.bookings 
WHERE starttime >= '2012-09-01' AND starttime < '2012-10-01' 
GROUP BY facid 
ORDER BY SUM(slots) ASC;
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-13-09-36.png)

### Ques 12) Produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and total slots, sorted by facility id.
```sql
SELECT facid, sum(slots) AS "Total Slots" 
FROM cd.bookings 
GROUP BY facid 
HAVING SUM(slots) >1000
ORDER BY facid
```


#### WHERE clause:

- It is used to filter rows before any aggregation occurs.
You can use WHERE to filter based on column values but not with aggregate functions like SUM(), COUNT(), etc.

#### HAVING clause:

- It is used to filter rows after the aggregation has been performed.
HAVING is specifically used with aggregate functions like SUM(), COUNT(), AVG(), etc. after the GROUP BY clause.
- Use HAVING after GROUP statememnt in a sql query

### Ques 13) How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.

```sql
SELECT starttime,name FROM cd.bookings
INNER JOIN cd.facilities
ON cd.facilities.facid = cd.bookings.facid
WHERE name LIKE 'Tennis %' 
AND starttime >= '2012-09-21' 
AND starttime < '2012-09-22'
ORDER BY cd.bookings.starttime;
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-13-22-14.png)

### Ques 14) How can you produce a list of the start times for bookings by members named 'David Farrell'?

```sql
SELECT firstname,surname,starttime FROM cd.members
INNER JOIN cd. bookings
ON cd.members.memid = cd.bookings.memid
WHERE firstname LIKE 'David' AND surname LIKE 'Farrell'
```
![Assessment -2](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/Clipboard_2024-09-27-13-25-57.png)
