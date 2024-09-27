# Assessment Test - 3

## Task-1

Create a new database called "School" this database should have two tables: **teachers** and **students.**

The **students** table should have columns for student_id, first_name,last_name, homeroom_number, phone,email, and graduation year.

The **teachers** table should have columns for teacher_id, first_name, last_name,

homeroom_number, department, email, and phone.

The constraints are mostly up to you, but your table constraints do have to consider the following:

1.  We must have a phone number to contact students in case of an emergency.

2.  We must have ids as the primary key of the tables

3. Phone numbers and emails must be unique to the individual.

Once you've made the tables, insert a student named Mark Watney (student_id=1) who has a phone number of 777-555-1234 and doesn't have an email. He graduates in 2035 and has 5 as a homeroom number.

Then insert a teacher names Jonas Salk (teacher_id = 1) who as a homeroom number of 5 and is from the Biology department. His contact info is: jsalk@school.org and a phone number of 777-555-4321.

#### Solution

- Creating the student table
  
  ```sql
  CREATE TABLE student (
      student_id SERIAL PRIMARY KEY,      -- Auto-incrementing primary key
      first_name VARCHAR(50),             -- First name with a max length of 50 characters
      last_name VARCHAR(50),              -- Last name with a max length of 50 characters
      homeroom_number INT,                -- Integer column for homeroom number
      phone VARCHAR(200) NOT NULL UNIQUE, -- Phone number, cannot be NULL, must be unique
      email VARCHAR(200) UNIQUE,          -- Email, must be unique but can be NULL
      graduation_year INT                 -- Integer for graduation year
  );
  
  ```

- Creating the teachers Table
  
  ```sql
  CREATE TABLE teachers (
      teacher_id SERIAL PRIMARY KEY,      -- Auto-incrementing primary key
      first_name VARCHAR(50),             -- First name with a max length of 50 characters
      last_name VARCHAR(50),              -- Last name with a max length of 50 characters
      homeroom_number INT,                -- Integer column for homeroom number
      phone VARCHAR(200) NOT NULL UNIQUE, -- Phone number, cannot be NULL, must be unique
      email VARCHAR(200) UNIQUE,          -- Email, must be unique but can be NULL
      department VARCHAR(50)              -- Department name with a max length of 50 characters
  );
  ```

![Assessment Test - 3](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-22-47-32-image.png)

- Adding the student named Mark Watney (student_id=1) who has a phone number of 777-555-1234 and doesn't have an email. He graduates in 2035 and has 5 as a homeroom numbe
  
  ```sql
  INSERT INTO students (
  first_name, last_name, phone, graduation_year, homeroom_number)
  VALUES ('Mark', 'Watney', '777-555-1234', 2035, 5);
  ```

![Assessment Test - 3](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-22-52-26-image.png)

- Then insert a teacher names Jonas Salk (teacher_id = 1) who as a homeroom number of 5 and is from the Biology department. His contact info is: [jsalk@school.org](mailto:jsalk@school.org) and a phone number of 777-555-4321.
  
  ```sql
  INSERT INTO teachers (
  first_name, last_name, homeroom_number,department,phone,email)
  VALUES (
  'Jonas', 'SALk',5,'Biology','777-555-4321','jsalk@school.org');
  ```

![Assessment Test - 3](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-22-57-26-image.png)


