# SQL_Fundamentals_and_Beyond
"This repository is dedicated to mastering SQL, from foundational concepts to advanced querying techniques. It covers essential SQL commands, best practices, and real-world examples, providing a comprehensive guide for learners and professionals seeking to enhance their database management and data analysis skills."

# Setup the PostgresSQL
### Step-1: Donwload PostgresSQL
- From the Link download the latest Stable version of PostgresSQL based on your operating system
[PostgresSQL Download Page](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)

### Step-2: Install the setup and keep all the settings to Default

### Step-3: Install the PgAdmin application
- pgAdmin is a popular open-source administration and development platform for PostgreSQL. It provides a graphical interface to manage PostgreSQL databases, making it easier to perform administrative tasks and database development compared to using command-line tools. [PgAdmin Download link](https://www.postgresql.org/ftp/pgadmin/pgadmin4/v8.11/windows/)

# Download the practice Database
- For this Repo i will be practicing on [DvD Rental Database](https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip). So if you want to follow along i would suggest you to donwload the database and practice the assignmenets that we will be doing later.

# Load the Database

### Step-1: Open pgAdmin 
- Open pgAdmin in your PC and on the left hand top corner select the postgreSQL 16 option
### Step-2: Create empty Data base
- Right click on the PostgreSQL 16 and create a empty Database
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/1.png)
- Give the name to you empty Database and press Save
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/2.png)

### Ste-3: Add DvD rental Database to you empty Database
- Right Click on the empty database that you just created in the previous step and click "Restore"
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/3.png)
- Go to General setting and Select the Database file that you have downloaded Earlier
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/4.png)
- Now go to the Data options panel and enable these 3 options
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/5.png)

- Now go ahead and click "Restore"
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/6.png)

Note: If you see some error then ignore them as most of the time the software try to restore twice and thus gets an error on the second time of restoration
### Step-4: verify Database is loaded Correctly
- Open the "Query Tool" by right clicking on the Database
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/8.png)

- Run the Command
```sql
SELECT * FROM film;
```
![Create empty Data base](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/Setup_Files/Setup_Images/7.png)