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


1. Create a database using the create statement:
```
create database PACKT_ONLINE_SHOP;
```
2. Switch to this database:
```
use PACKT_ONLINE_SHOP;
```
3. Create the Customers table:

```
create table Customers
(
    FirstName varchar(50) ,
    MiddleName varchar(50) ,
    LastName varchar(50) ,
    HomeAddress varchar(250) ,
    Email varchar(200) ,
    Phone varchar(50) ,
    Notes varchar(250)
);
```

```
USE studentdemo;

INSERT INTO Student (StudentID, StudentName, grade, age, course) VALUES ('S001',
'Prashanth Jayaram', 'A', 36, 'Computer Science');
```

Adding single rows like this in multiple queries will be time-consuming. We can add
multiple rows by writing a query like the following one:
```
INSERT INTO Student (StudentID, StudentName, grade, age, course) VALUES ('S002', 'Frank
Solomon', 'B', 35, 'Physics'), ('S003', 'Rachana Karia', 'B', 36, 'Electronics'),
('S004', 'Ambika Prashanth', 'C', 35, 'Mathematics');
```
```
CREATE TABLE department (
    departmentNo INT PRIMARY KEY AUTO_INCREMENT,
    departmentName VARCHAR(20) NOT NULL,
    departmentLoc VARCHAR(50) DEFAULT 'NJ',
    departmentEstDate DATETIME DEFAULT NOW()
);
```
```
INSERT INTO department (
    departmentName
)
VALUES (
    'MyDepartment'
);
```
```
INSERT INTO department (
    departmentName,
    departmentLoc)
VALUES
(
    'Administration',
    DEFAULT
),
(
    'IT',
    DEFAULT
);
```

Apart from INSERT...SELECT, you could use CREATE 
```
TABLE AS SELECT * FROM:
CREATE TABLE departmentdemo AS
  SELECT *
  FROM department;
```
say you have an employee with empno 1234 who is no longer associated
with the company. In such cases your query would look like the following:
```
DELETE FROM employees
    WHERE empno = 1234;
```
If you would like to remove the top 5 rows from the employees table, we would use the
following query:
```
DELETE FROM employees
    LIMIT 5;
```
```
USE PACKT_ONLINE_SHOP
DELETE FROM products
    WHERE ProductName = 'tomato sauce';
```
The ALTER keyword is used to make changes to the schemas present in the database. For
example, if we want to add or delete columns in a table, we should be using ALTER. It can
also be used rename to tables. For example:
```
ALTER TABLE departmentdemo RENAME TO departmentcopy;
```
Delete the rows where departmentNo is greater than 2; this will delete the two rows
where departmentNo is 3 and 4:
```
delete from department where departmentNo>2;
```
Now, insert the sales department into the department table:
```
insert into department(departmentname,departmentLoc)
values('Sales','LV');
```
Delete the newly inserted Sales department:
```
delete from department where departmentNo=5;
```
 Run the ALTER TABLE statement to reset the auto_increment column to 3.
 ```
ALTER TABLE department AUTO_INCREMENT = 3;
```
Insert the Sales department:
```
insert into department(departmentname,departmentLoc)
values('Sales','LV');
select * from department;
```
Suppose Ava-May changed her name to Ava-May Rodgers, and you had to update the
table. You would use the following SQL statement:
```
UPDATE employees
SET
    Email = 'Ava-May.Rodgers@awesomenes.com'
WHERE empno = 3
```
Suppose we have a table called department
within a database. Imagine that you would like to set the modified date for each of the
departments to the current date—in other words, we are going to change the modified
date on all the rows. We do this using the following query:
```
update department set departmentEstDate=now();
```
If you query all the records within the table and see what departmentEstDate looks like
for each record:
```
select * from department;
```
In the following example, we are limiting three records where we update the salary.
These records are sorted in descending order and are getting the least commission:
```
UPDATE employees SET comm=1000
WHERE empno IN (
    SELECT empno FROM (
        SELECT empno FROM employees where comm<=500
        ORDER BY salary desc, comm ASC
        LIMIT 0, 3
    ) stg
);
```

Consider the scenario where we are providing 10% off the net retail price of all the
products in packt_online_shop:
1. Type the following query and execute the command:
```
UPDATE products
    SET
        NetRetailPrice = NetRetailPrice * 0.90;
```
We will now look at the DROP operation, to see how we can delete the schema altogether.
The syntax is as follows:
```
DROP TABLE <table_name>;
```
To drop the customers table in the packt_online_database, the query would be as
follows:
```
DROP TABLE Customers;
```
Let's look at this in the context of a primary key. When this primary key is referenced by
a column in another table, this primary key becomes the foreign key of the other table.
For example, consider the previously created database PACKT_ONLINE_SHOP:
```
DROP DATABASE IF EXISTS PACKT_ONLINE_SHOP;
CREATE DATABASE IF NOT EXISTS PACKT_ONLINE_SHOP;
USE PACKT_ONLINE_SHOP;
CREATE TABLE Customers
(
    CustomerID INT NOT NULL AUTO_INCREMENT,
    FirstName CHAR(50) NOT NULL,
    LastName CHAR(50) NOT NULL,
    Address CHAR(250) NULL,
    Email CHAR(200) NULL,
    Phone CHAR(50) NULL,
    Notes VARCHAR(750) NULL,
    BalanceNotes VARCHAR(750) NULL,
    PRIMARY KEY (CustomerID)
);
CREATE TABLE Orders
(
    OrderID INT NOT NULL AUTO_INCREMENT,
    CustomerID INT NOT NULL,
    OrderNumber CHAR(50) NOT NULL,
    OrderDate DATETIME NOT NULL,
    ShipmentDate DATETIME NULL,
    OrderStatus CHAR(10) NULL,
    Notes VARCHAR(750) NULL,
PRIMARY KEY (OrderID),
FOREIGN KEY FK_Customer_CustomerID(CustomerID) REFERENCES Customers(CustomerID)
);
```
Let's look at the OrderItems table:
```
CREATE TABLE OrderItems
(
    OrderItemID INT NOT NULL AUTO_INCREMENT,
    OrderID INT NOT NULL,
    ProductID INT NOT NULL,
    Quantity INT NOT NULL,
    UnitPrice DECIMAL(10, 2) NOT NULL,
    Discount DECIMAL(10, 2) NULL,
    Notes VARCHAR(750) NULL,
    PRIMARY KEY (OrderItemID)
);
```
Considering this, ProductID should be the primary key of the Products table as it is
unique across the store. Given that, the ProductID within the OrderItems table should be
the foreign key, referring to the ProductID within Products. Let's see how we can set this
up in the table:
```
ALTER TABLE OrderItems
ADD FOREIGN KEY (ProductID) REFERENCES Products(ProductID);
```
To drop a foreign key, you can use the ALTER TABLE statement:
```
ALTER TABLE <table_name>
DROP FOREIGN KEY <constraint_name>;
```
In the context of our example, the syntax will be as follows:
```
ALTER TABLE OrderItems
DROP FOREIGN KEY ProductID
```
Imagine that Jon Doe leaves the organization and Jim Doe replaces him. Now, imagine
that this table has 4,000 entries and Jon Doe owns 300 servers. To change the owner of
the servers, you may think of replacing the names in the table using the following query:
```
UPDATE ServerInfo SET Name='Jim Doe' WHERE employeeName='Jon Doe';
```
Now, Jim Doe joins the organization, and four servers get assigned to him. He is part
of the Network team. After you make the changes to the table, you realize that you did
not update the employee ID, designation, or the department for the entries that had Jon
Doe, and without looking at the data, someone unknowingly runs the following query:
```
UPDATE ServerInfo SET EmployeeId='79247' WHERE employeeName='Jim Doe';
```
Let's assume that our IAM application manages the second table. If Hans Doe replaces
Jim Doe, the Team Lead, at a later point, the second table will get all the necessary
information about Hans Doe when the Human Resources team processes Hans'
hiring. All you would have to do then is replace the OwnerId information in the server
information table with a single query:
```
UPDATE ServerInfo SET OwnerId='79482' WHERE OwnerId='79247';
```
What if you need to get a table that's identical to the first table, as we saw at the
beginning of this chapter? We can use the following query:
```
SELECT s.Servername, s.OperatingSystem, u.EmployeeId, u.Name, u.Designation, u.Department
FROM ServerInfo s
    JOIN EmployeeInfo u ON s.OwnerId = u.EmployeeId;
```
In your organization, you have been asked to present the employee and department
data in two tables and build the relationship between the department and employee
table.
Perform the following steps to achieve this:
1. Create a demo database called employeedemo.

```
DROP DATABASE IF EXISTS employeedemo;
CREATE DATABASE employeedemo;
```
2. Create a department table with the required data. Ensure there is referential
integrity between the department and employee tables on the dno field:
```
USE employeedemo;
CREATE TABLE department
  (
      dno INT PRIMARY KEY,
      dname VARCHAR(30) UNIQUE NOT NULL,
      dlocation VARCHAR(30) UNIQUE NOT NULL
)
```
3. Create an EMPLOYEE table with the required data, enforcing a check constraint on
the gender field and default values on the salary and commission fields:
```
CREATE TABLE employee
(
eno		 CHAR(4) PRIMARY KEY,
ename		 VARCHAR(30) NOT NULL,
job		 VARCHAR(30) NOT NULL,
manager CHAR(4),
jdate		 TIMESTAMP NOT NULL,
gender CHAR(1) CONSTRAINT gender_chk
CHECK ( gender IN('M', 'F')),
salary DECIMAL(8, 2) DEFAULT 0,
comission DECIMAL(8, 2) DEFAULT 0,
deptno INT NOT NULL,
FOREIGN KEY (deptno) REFERENCES department(dno)
)
```
The syntax of a typical SQL query is as follows:
```
SELECT [COLUMNS LIST]
FROM [TABLE NAME]
WHERE [CONDITION]
ORDER BY [COLUMN NAME] [ASC|DESC]
```

Where:
•
[COLUMNS_LIST] is replaced by the column names that you want to retrieve,
separated by commas.
•
[TABLE_NAME] is replaced by the table name in your database.
•
[CONDITION] is the condition to narrow down your result.
•
[COLUMN NAME] is the column that the result set will be ordered or sorted on.
•
[ASC | DESC] is the order option, ascending or descending.

Consider the following scenario: A store manager wants to retrieve information about
all the categories of items available in PACKT_ONLINE_SHOP in order to see where a new
product fits in best. To retrieve a list of all the product categories, along with their
details, run the following query:
```
use PACKT_ONLINE_SHOP;
SELECT * FROM ProductCategories;
```
The store manager wants to check the ProductCategoryId field of all the categories in
PACKT_ONLINE_SHOP. They need you to retrieve the relevant columns, ProductCategoryId
and ProductCategoryName. To retrieve this data from the table, we need to perform the
following steps:
1. Open a new query window.
2. Switch to the PACKT_ONLINE_SHOP database:

```
use PACKT_ONLINE_SHOP;
```
3. Enter the following query:
```
SELECT ProductCategoryID, ProductCategoryName
FROM ProductCategories;
```
Note that the columns are displayed in the exact order they were mentioned in the
SELECT statement. So, if we want to show the name of the category first followed by ID,
we use the following statement:
```
SELECT ProductCategoryName, ProductCategoryID
FROM ProductCategories;
```

When you extract data for the
purposes of a report, you'll have various people looking at it, and so you might want to
make the column heading clearer and more relatable. To provide the result set with a
column header of your choice, use the AS keyword after the column name. The syntax
for aliasing the column is as follows:
```
SELECT [Original name] AS [New name]
```
While publishing a report, we want to rename the column headings of the previous
query as CATEGORY and ID, respectively. To do this, perform the following steps:
1. Enter the following query:

```
SELECT ProductCategoryName AS CATEGORY, ProductCategoryID AS ID
FROM ProductCategories;
```
In cases where you want to use multiple words with spaces between them, use the
full name between single quotes ' ', as follows:
```
SELECT ProductCategoryName AS 'PRODUCT CATEGORY', ProductCategoryID AS ID
FROM ProductCategories;
```
Here, the rows will be sorted based on the selected column in ascending order.
Columns that contain character values will be arranged alphabetically. Let's try to apply
this to the ProductCategories table and sort the results by CATEGORY NAME, as follows:
```
SELECT ProductCategoryName AS 'CATEGORY NAME', ProductCategoryID AS ID
FROM ProductCategories
ORDER BY ProductCategoryName ASC;
```
You can observe that in the FirstName column, there are multiple entries with NULL as
their first name. So, when we order our results by FirstName in ascending order and the
CustomerID in descending order, we will notice the difference. Let's implement this as
follows:
```
SELECT FirstName, CustomerID
FROM Customers
ORDER BY FirstName, CustomerID DESC;
```
A useful tip when using the ORDER BY clause is to use an integer abbreviation instead of
the complete column name. Column abbreviations start with 1, which is given to the
first column in your statement. 2 is given to the second column, and so on. Let's try
to perform the same query as before, but we will now order the columns using their
abbreviations and, this time, the second ordering column will be sorted in ascending
order instead:
```
SELECT FirstName, CustomerID
FROM Customers
ORDER BY 1, 2;
```

We can limit the number of records displayed in the results by providing a specific
number of records to be retrieved using the LIMIT keyword. It is an optional keyword
and is used after the SELECT keyword in the following form:
```
SELECT [COLUMNS LIST]
FROM [TABLE NAME]
LIMIT [n];
```
The store manager wants to identify the five most expensive items from the product
catalog. To obtain this report, we will need to do the following:
1. Type the following query:

```
SELECT ProductName, NetRetailPrice
FROM Products
ORDER BY NetRetailPrice DESC
LIMIT 5;
```
Whenever we want to make sure we always retrieve distinct records (records with no
duplication), we can use the DISTINCT keyword. The DISTINCT is an optional keyword that
is used after the SELECT keyword in the following form:
```
SELECT DISTINCT [COLUMNS LIST]
FROM [TABLE NAME]
```
In the OrderItems table, there is a Discount field. We will use this field along with our last
expression to get the line item price after the discount. Perform the following steps:
1. Write the following query:

```
SELECT ProductID, Quantity, UnitPrice, (Quantity*UnitPrice)
AS 'Line Item Total', Discount,
((Quantity*UnitPrice)-(Quantity*Discount))
AS 'Price After Discount'
FROM OrderItems;
```
The WHERE clause is optional and can be added to any SELECT statement, usually after the
FROM clause, as follows:
```
SELECT [COLUMNS LIST]
FROM [TABLE NAME]
WHERE [CONDITION]
ORDER BY [COLUMN NAME] [ASC|DESC]
```
A simple implementation of a WHERE clause is as follows:
```
USE studentdemo;
SELECT *
FROM Student;
```
The store manager wants a list of all the items that are priced over $14.99 and wants to
label them as high-value products. To retrieve the list of all the products that are priced
over $14.99, perform the following steps:
1. Open a new query window.
2. Switch to PACKT_ONLINE_SHOP:

```
use PACKT_ONLINE_SHOP;
```
Write a query to filter the products that are priced over $14.99:
```
SELECT ProductName AS 'High-value Products', NetRetailPrice
FROM Products
WHERE NetRetailPrice > 14.99
```

To include products that have a NetRetailPrice of $14.99 in the previous results,
use the >= operator as follows:
```
USE PACKT_ONLINE_SHOP;
SELECT ProductName AS 'High-value Products', NetRetailPrice
FROM Products
WHERE NetRetailPrice >= 14.99
```
We can control our results further by limiting our search to a specific range. We do
this by using the BETWEEN operator. For example, if we were to filter students who have
scored between 75 and 90, our syntax for the WHERE clause would be:
```
WHERE SCORE BETWEEN 75 AND 90
```
The store manager now wants to list all the items in the range of $14.99 to $50 as
mid-priced items. To derive a list of all items that are priced between $14.99 and $50, we
will need to perform the following steps:
1. In a new query window, write the following query:

```
SELECT ProductName,NetRetailPrice
FROM Products
WHERE NetRetailPrice BETWEEN 14.99 AND 50
ORDER BY NetRetailPrice;
```

The store manager realizes that the tomato sauce received has gone bad, so he does
not want to present it in the list of available items. To write a query to display all the
products except the tomato sauce, perform the following steps:
1. Enter the SELECT statement, using the WHERE clause and the != operator:
```
SELECT ProductName,NetRetailPrice
FROM Products
WHERE ProductName != 'tomato sauce'
ORDER BY NetRetailPrice;
```
 As an alternative, now replace the != symbol with the <> operator:
 ```
SELECT ProductName,NetRetailPrice
FROM Products
WHERE ProductName <> 'tomato sauce'
ORDER BY NetRetailPrice;
```
Often, we come across situations where we need to retrieve data with a certain pattern.
For example, you may want to get all customer names that start with an "A", or any
customers with "Joe" in their name. This is where the LIKE operator comes in handy.
Similar to the other operators we've seen in this chapter, the LIKE operator is used with
the WHERE clause.
Let's implement it in our syntax:
```
SELECT [COLUMNS LIST]
FROM [TABLE NAME]
WHERE [COLUMN NAME] LIKE
```

<img width="524" alt="Screenshot 2024-12-15 at 9 52 46 PM" src="https://github.com/user-attachments/assets/59b43aec-3545-43b3-908f-5885c5b3efa4" />
 '[PATTERN]'

Let's see an example. To search for first names that have o in the second position, the
following query can be run:
```
SELECT FirstName, LastName, Phone
FROM Customers
WHERE FirstName LIKE '_o%';
```
To increase area-wide sales in LA, we want a list of customers from LA. We don’t
currently have any field specifically mentioning the state/country, but since we record
the customers’ phone details, we can filter the phone numbers that start with the code
for LA (310), as follows:
1. Write a query implementing the LIKE operator in the WHERE clause to match the
phone numbers that begin with (310):
```
SELECT FirstName AS 'Customers from LA', Phone
FROM Customers
WHERE Phone LIKE '(310)%';
```
We want to provide usernames to our customers so they can log into our system. We
want to create each username from the customer's first name. However, our system
does not allow three-letter usernames. The store manager will have to pull up a report
on all the customers with three-letter usernames. To do so, perform the following
steps:
1. Write the following query in a new query window:
```
SELECT FirstName, LastName, Phone
FROM Customers
WHERE FirstName LIKE '___';
```
Checking NULL values can be done using the following two special keywords, as it cannot
be done using the logical operators:
•
IS NULL
•
IS NOT NULL


On many occasions, we may need to combine multiple conditions at the same time. The
best way to do this in SQL is by using the following three operators, which can be used
between conditions in the WHERE clause:
•
AND: This operator makes sure both sides of the operator (both conditions) are true.
•
OR: This operator makes sure one side at least of the operator is true.
•
NOT: This operator makes sure that the condition following this operator is false.


Joe, a customer from LA, has requested to speak to the store manager regarding a
complaint. We are going to write a query to retrieve all of this customer's details. This
will allow the manager to have all the required information to best help resolve the
customer's complaint.
The state code for LA is (310). To pull the required information, perform the following
steps:
1. Enter the query as follows:

```
SELECT *
FROM Customers
WHERE FirstName = 'Joe' AND Phone LIKE '(310)%';
```
For clarity, we're also going to do a search for all customers who are either named Joe
or who live in LA. This will help us to verify that we've got the right customer, rather
than the wrong Joe, or the wrong person from LA. We will do this by using the OR
operator on the same example:
```
SELECT FirstName, LastName, Phone
FROM Customers
WHERE FirstName = 'Joe' OR Phone LIKE '(310)%';
```
Now, say we have a scenario where we need to list all customers that have a first name
starting with Jo and a phone number that starts with (310) or (210), but who don't have a
last name of Carter. This is a perfect scenario to use all operators in one query:
```
SELECT FirstName, LastName, Phone,Notes
FROM Customers
WHERE FirstName LIKE 'Jo%' AND (Phone LIKE '(310)%' OR Phone LIKE '(210)%') AND NOT
LastName = 'Carter';
```
### INNER JOIN
The INNER JOIN is the default type of join that is used to select data with matching
values in both tables. It can be represented with the following Venn diagram:
<img width="385" alt="Screenshot 2024-12-15 at 10 03 17 PM" src="https://github.com/user-attachments/assets/8370e836-ae16-41d5-8e45-cf75da8de385" />

The INNER JOIN represents the highlighted section, which is the intersection between
these two tables. Let's have a look at the INNER JOIN syntax:
```
SELECT [Column List]
  FROM [Table 1] INNER JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```
The syntax can also be written as follows:
```
SELECT [Column List]
  FROM [Table 1] JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```
### RIGHT JOIN
This type of join is used when you want to select records that are available in the
second table and matching records in the first one. This can be visualized with the following Venn diagram:
<img width="423" alt="Screenshot 2024-12-15 at 10 06 00 PM" src="https://github.com/user-attachments/assets/3f71c12b-9725-4f82-b1cf-0e9f70e56a1e" />

```
SELECT Customers.FirstName,
Customers.LastName,
Customers.Email ,
Orders.OrderNumber,
Orders.OrderStatus
FROM Orders RIGHT JOIN Customers ON
Orders.CustomerID = Customers.CustomerID
```
```
To extract a list of customers who haven't placed any orders from the store, enter
the following query:
SELECT Customers.FirstName,
Customers.LastName,
Customers.Email ,
Orders.OrderNumber,
Orders.OrderStatus
FROM Orders RIGHT JOIN Customers ON
Orders.CustomerID = Customers.CustomerID
WHERE Orders.OrderNumber IS NULL
```

As we can see, the RIGHT JOIN represents the highlighted section, that is, TABLE B, and
the intersected section of TABLE A. Let's look at the syntax for the RIGHT JOIN:
```
SELECT [Column List]
  FROM [Table 1] RIGHT OUTER JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```
The syntax can also be written as follows:
```
SELECT [Column List]
  FROM [Table 1] RIGHT JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```

### LEFT JOIN
This type of JOIN is used when you want to select records that are available in the first
table and match records in the second one. It can be represented with the following
Venn diagram:

<img width="487" alt="Screenshot 2024-12-15 at 10 09 38 PM" src="https://github.com/user-attachments/assets/b146755d-d4c0-4b3e-9f3c-2576ba3d762b" />

The LEFT JOIN represents the highlighted section from TABLE A and the intersected
section from TABLE B. Let's look at the syntax:
```
SELECT [Column List]
  FROM [Table 1] LEFT OUTER JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```
The syntax can also be as follows:
```
SELECT [Column List]
  FROM [Table 1] LEFT JOIN [Table 2]
    ON [Table 1 Column Name] = [Table 2 Column Name]
WHERE [Condition]
```

### CROSS JOIN
This type of join is used when you want to combine the elements of a particular column
with the elements of another column. This implies that each record from the first table
and each record from the second table are laid out in all possible combinations in one
single table, just like in the case of a cartesian product. Here is how we can perform this
task using the CROSS JOIN syntax:
```
SELECT [Column List]
  FROM [Table 1] CROSS JOIN [Table 2]
WHERE [Condition]
```

### UNION JOIN
The UNION operation is used to combine two queries. Let's look at the syntax:
```
SELECT [COLUMNS LIST] FROM [TABLE NAME]
UNION
SELECT [COLUMNS LIST] FROM [TABLE NAME]
```


