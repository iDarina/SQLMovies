### Data Definition Language 
* CREATE - creates a new database or a new table
* ALTER - Modifies the structure of a database or a table
* DROP - Deletes a database or a table
* TRUNCATE - removes all table records and the allocated table spaces
* RENAME - renames a database or a table

### Data Manipulation Language 
* INSERT - adds new rows to a table
* UPDATE - Updates the existing data or rows or records in a table
* DELETE - deletes records from a table
* MERGE - this is also calles UPSERT (as in UPDATE/INSERT). MERGE is used to insert new records or update existing records based on conditions.

### Data Control Language 
* GRANT - gives access privileges to a user for the data in a database
* REVOKE - takes away the privileges a user has on the specified data

### Transaction Control Language
* COMMIT - saves the changes permanently in the database
* ROLLBACK - restores the database to its original form until the last COMMIT
* SAVEPOINT - creates a point for later use in order to roll back the new changes
* SET TRANSACTION - sets transaction properties to make it read-only, for example

### Data Query Language
* SELECT - displays static data or retrieves data from a table, based on certain parameters

### Numeric data types
<img width="587" alt="Screenshot 2024-12-15 at 5 20 44 PM" src="https://github.com/user-attachments/assets/a34b3637-e14e-436a-bf8d-2e1ac8d9bd85" />


------------------------



```
create database studentdemo;
```
```
use studentdemo;
```
```
create table Student
(
    StudentID      CHAR (4),
    StudentName VARCHAR (30),
    grade       CHAR(1),
    age         INT,
    course      VARCHAR(50),
    PRIMARY KEY (StudentID)
);
```


---------------------
