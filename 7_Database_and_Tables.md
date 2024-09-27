# Creating Database and Tables

#### Primary key

-  A primary key is a column or a group of columns used to identify a row uniquely in a table

- **Properties**:
  
  - Must be unique for each row (no duplicates).
  - Cannot contain `NULL` values (mandatory for every row).
  - A table can have only **one** primary key, but it can consist of multiple columns (composite key).

- Here It can be Seen `[PK] = Primary key`
  
  ![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-14-49-27-image.png)

#### Foreign key

* A column or set of columns in one table that refers to the primary key in another table.

* **Purpose**: To create a relationship between two tables and enforce referential integrity (ensure that data in one table corresponds to valid data in another table).

* **Properties**:
  
  - Can have duplicate values.
  - Can contain `NULL` values (unless constrained otherwise).
  - There can be multiple foreign keys in a table.
  - The foreign key value must match an existing value in the referenced primary key (or be `NULL` if allowed).

#### Constraints

A **constraint** in a database is a rule enforced on data columns in a table. Constraints help ensure the accuracy and integrity of the data by specifying conditions that data in the database must meet. They can be applied to one or more columns of a table during the table creation or modification process.

- **Primary key constraints**: Ensures that each row in a table is unique and cannot be `NULL`.

- **Foreign key constraints**: Ensures that a column’s value matches the values in a related table, enforcing referential integrity.

- **Unique constraints**

- **Not Null**

- **Check constraint**: Ensures that a column's values meet a specified conditions

- **Refrences**: To constraint the value stored in the column that must exist in a column in another table.

# Create a Table

* ```sql
  CREATE TABLE table_name (
      column1 datatype constraint,
      column2 datatype constraint,
      column3 datatype constraint,
      ...
  );
  ```

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,        -- Primary key constraint
    first_name VARCHAR(50) NOT NULL,    -- Not null constraint
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,          -- Unique constraint
    hire_date DATE DEFAULT CURRENT_DATE -- Default constraint
);
```

### Common Datatypes in SQl

Here’s a table of the most common SQL data types, along with their syntax and brief descriptions:

| **Data Type**                      | **Syntax**                 | **Description**                                                                                          |
| ---------------------------------- | -------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Integer Types**                  |                            |                                                                                                          |
| `INT` / `INTEGER`                  | `INT` or `INTEGER`         | Stores whole numbers (positive, negative, or zero).                                                      |
| `SMALLINT`                         | `SMALLINT`                 | Stores small-range integers.                                                                             |
| `BIGINT`                           | `BIGINT`                   | Stores very large whole numbers.                                                                         |
| **Decimal & Floating-Point Types** |                            |                                                                                                          |
| `DECIMAL(p,s)`                     | `DECIMAL(p,s)`             | Fixed precision and scale numbers. `p` is precision (total digits), `s` is scale (digits after decimal). |
| `NUMERIC(p,s)`                     | `NUMERIC(p,s)`             | Same as `DECIMAL`, often used interchangeably.                                                           |
| `FLOAT`                            | `FLOAT` or `FLOAT(n)`      | Stores floating-point numbers, where `n` specifies the precision.                                        |
| `REAL`                             | `REAL`                     | Stores approximate floating-point values with lower precision than `FLOAT`.                              |
| **String Types**                   |                            |                                                                                                          |
| `CHAR(n)`                          | `CHAR(n)`                  | Fixed-length character string of length `n`.                                                             |
| `VARCHAR(n)`                       | `VARCHAR(n)`               | Variable-length character string of up to `n` characters.                                                |
| `TEXT`                             | `TEXT`                     | Stores long strings of variable length.                                                                  |
| **Date/Time Types**                |                            |                                                                                                          |
| `DATE`                             | `DATE`                     | Stores date values (year, month, day).                                                                   |
| `TIME`                             | `TIME`                     | Stores time values (hours, minutes, seconds).                                                            |
| `DATETIME`                         | `DATETIME`                 | Stores both date and time information.                                                                   |
| `TIMESTAMP`                        | `TIMESTAMP`                | Stores a timestamp (date and time) with time zone support in some systems.                               |
| **Boolean Type**                   |                            |                                                                                                          |
| `BOOLEAN`                          | `BOOLEAN`                  | Stores `TRUE`, `FALSE`, or `NULL`.                                                                       |
| **Binary Types**                   |                            |                                                                                                          |
| `BINARY(n)`                        | `BINARY(n)`                | Fixed-length binary data of length `n`.                                                                  |
| `VARBINARY(n)`                     | `VARBINARY(n)`             | Variable-length binary data of up to `n` bytes.                                                          |
| **Other Types**                    |                            |                                                                                                          |
| `BLOB`                             | `BLOB`                     | Stores binary large objects (e.g., images, audio).                                                       |
| `ENUM`                             | `ENUM('value1', 'value2')` | A string object that can only have one value, chosen from a list of values.                              |

#### SERIAL

In SQL, the `SERIAL` data type is commonly used to create auto-incrementing integer columns, often used for primary keys. It automatically generates unique values for new rows without manually specifying a value.

- `SERIAL` is not a standard SQL data type but is specific to databases like **PostgreSQL**

- `SERIAL` implicitly creates a sequence and associates it with the column.

```sql
CREATE TABLE Employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

Note: If the `SERIAL` data type is used  and then if we delete any column then we will see a break in sequence of row number [This also true for Failed attempts in adding rows]

#### Task 1: Create a Table

```sql
CREATE TABLE account(
user_id SERIAL PRIMARY KEY,
user_name VARCHAR(50) UNIQUE NOT NULL,
password VARCHAR(50) NOT NULL,
email VARCHAR(250) UNIQUE NOT NULL,
created_on TIMESTAMP NOT NULL,
last_login TIMESTAMP
)
```

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-15-23-43-image.png)

```sql
CREATE TABLE job(
job_id SERIAL PRIMARY KEY,
job_name VARCHAR(200) UNIQUE NOT NULL
);
```

```sql
CREATE TABLE account_job(
user_id INTEGER REFERENCES account(user_id),
job_id INTEGER REFERENCES job(job_id),
hire_date TIMESTAMP
);
```

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-15-30-48-image.png) we have created 3 Table



#### Insert Information in Tables

To insert rows into a table, you can use the `INSERT INTO` statement in SQL. Here's a general guide to inserting multiple rows into a table:

```sql
INSERT INTO account(user_name,password,email,created_on)
VALUES
('Jose','password','jose@mail.com',CURRENT_TIMESTAMP)
```

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-16-56-24-image.png)

Note: user_id is automatically created for us

```sql
INSERT INTO job(job_name)
VALUES
('Astronaut')
```

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-16-58-31-image.png)

```sql
INSERT INTO account_job(user_id,job_id,hire_date)
VALUES
(1,1,CURRENT_TIMESTAMP)
```

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-17-01-10-image.png)

Note:  Now we will try to add  someone whose user_id does not exist

- This will violate the foreign key constraint

- ```sql
  CREATE TABLE account_job(
  user_id INTEGER REFERENCES account(user_id),
  job_id INTEGER REFERENCES job(job_id),
  hire_date TIMESTAMP
  );
  ```

- we can see job_id is a refrenced to Table "Job" since there no such `job.job_id` we cannot add that to account_job 

![Creating Database and Tables](https://github.com/HBISHT233/SQL_Fundamentals_and_Beyond/blob/main/attachments/2024-09-27-17-02-08-image.png)

#### Update

The `UPDATE` keyword in SQL is used to modify existing records in a table. You can update one or more columns based on a condition.

- we can either normally update a tabel row or we can use other table to update our current table

```sql
UPDATE Employees
SET hire_date = '2023-10-01'
WHERE hire_date < '2023-01-01';
```

```sql
UPDATE Employees
SET department_name = Departments.department_name
FROM Departments
WHERE Employees.department_id = Departments.department_id;
```

#### Returning

In SQL, the `RETURNING` clause is used to return the updated, inserted, or deleted rows immediately after an `INSERT`, `UPDATE`, or `DELETE` operation. It's particularly useful when you need to retrieve values from a table after making changes, such as generated `SERIAL` values or updated fields

```sql
UPDATE Employees
SET hire_date = '2023-10-01'
WHERE employee_id = 1
RETURNING employee_id, hire_date;
```

#### DELETE

In SQL, the `DELETE` statement is used to remove rows from a table. You can delete specific rows based on a condition, or, if you omit the condition, you can delete all rows from a table.

```sql
DELETE FROM table_name
WHERE condition;
```

#### ALTER

The `ALTER` statement in SQL is used to modify the structure of an existing table. You can use it to add, modify, rename, or drop columns, or to change other properties of a table.

| **Operation**       | **SQL Syntax**                                                                                                                                         | **Example**                                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Add a Column**    | `ALTER TABLE table_name ADD column_name datatype;`                                                                                                     | `ALTER TABLE Employees ADD phone_number VARCHAR(15);`                                                                                                |
| **Modify a Column** | MySQL: `ALTER TABLE table_name MODIFY column_name new_datatype;` <br> PostgreSQL: `ALTER TABLE table_name ALTER COLUMN column_name TYPE new_datatype;` | MySQL: `ALTER TABLE Employees MODIFY phone_number VARCHAR(20);` <br> PostgreSQL: `ALTER TABLE Employees ALTER COLUMN phone_number TYPE VARCHAR(20);` |
| **Rename a Column** | `ALTER TABLE table_name RENAME COLUMN old_column_name TO new_column_name;`                                                                             | `ALTER TABLE Employees RENAME COLUMN phone_number TO contact_number;`                                                                                |
| **Drop a Column**   | `ALTER TABLE table_name DROP COLUMN column_name;`                                                                                                      | `ALTER TABLE Employees DROP COLUMN contact_number;`                                                                                                  |
| **Rename a Table**  | `ALTER TABLE old_table_name RENAME TO new_table_name;`                                                                                                 | `ALTER TABLE Employees RENAME TO Staff;`                                                                                                             |

In SQL, the `ALTER` statement can also be used with the `SET` keyword to modify specific attributes of columns or tables, such as setting default values or constraints. Here are common use cases for `ALTER` with `SET`.

### Common `ALTER` + `SET` Operations:

| **Operation**                              | **SQL Syntax**                                                               | **Example**                                                              |
| ------------------------------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Set a Default Value**                    | `ALTER TABLE table_name ALTER COLUMN column_name SET DEFAULT default_value;` | `ALTER TABLE Employees ALTER COLUMN hire_date SET DEFAULT CURRENT_DATE;` |
| **Remove a Default Value**                 | `ALTER TABLE table_name ALTER COLUMN column_name DROP DEFAULT;`              | `ALTER TABLE Employees ALTER COLUMN hire_date DROP DEFAULT;`             |
| **Set a Column to NOT NULL**               | `ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;`              | `ALTER TABLE Employees ALTER COLUMN last_name SET NOT NULL;`             |
| **Remove NOT NULL Constraint**             | `ALTER TABLE table_name ALTER COLUMN column_name DROP NOT NULL;`             | `ALTER TABLE Employees ALTER COLUMN last_name DROP NOT NULL;`            |
| **Set a Table to Read Only** (PostgreSQL)  | `ALTER TABLE table_name SET READ ONLY;`                                      | `ALTER TABLE Employees SET READ ONLY;`                                   |
| **Set a Table to Read Write** (PostgreSQL) | `ALTER TABLE table_name SET READ WRITE;`                                     | `ALTER TABLE Employees SET READ WRITE;`                                  |

```sql
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);


ALTER TABLE Employees 
ADD CONSTRAINT pk_employee_id PRIMARY KEY (employee_id);
```

#### CHECK

- The CHECK constraint is a powerful feature to enforce data integrity in your tables.

- The **condition** in the CHECK constraint can include one or more columns and can involve various operators such as comparison (`>`, `<`, `=`, etc.) and logical operators (`AND`, `OR`).

```sql
CREATE TABLE Employees (
    employee_id SERIAL PRIMARY KEY,
    age INT,
    parent_age INT,
    CONSTRAINT chk_age CHECK (parent_age > age)  
    -- Ensures parent_age is greater than age
);
```


