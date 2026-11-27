# Experiment 2: DDL Commands
## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

```
CREATE TABLE Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
);

```

**Output:**

<img width="1273" height="782" alt="Screenshot 2026-11-19 211914" src="https://github.com/user-attachments/assets/cbb8b5ff-c9c6-4272-855a-5b2670797135" />


**Question 2**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'
```
ALTER TABLE Student_details
ADD COLUMN email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**

<img width="1298" height="681" alt="Screenshot 2026-11-19 212046" src="https://github.com/user-attachments/assets/f4830a01-b3f2-4683-956d-13d4c1d96ebd" />

**Question 3**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```
CREATE TABLE Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
FOREIGN KEY(SupplierID)REFERENCES Suppliers(SupplierID)
FOREIGN KEY(OrderID)REFERENCES Orders(OrderID)
);



```

**Output:**

<img width="1282" height="693" alt="Screenshot 2026-11-19 212311" src="https://github.com/user-attachments/assets/21eaec99-ce08-447f-b42b-fe4f3779ba0d" />


**Question 4**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```
alter table Student_details
add Date_of_birth  Date;
```

**Output:**

<img width="1302" height="787" alt="Screenshot 2026-11-19 212441" src="https://github.com/user-attachments/assets/cf4c1b9e-597c-42a6-9bf9-43f2682d5056" />


**Question 5**
---
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000

```
INSERT INTO Employee
(EmployeeID,Name,Position,Department,Salary)
values('2','John Smith','Developer','IT','75000'),
      ('3','Anna Bell','Designer','Marketing','68000');

```

**Output:**

<img width="1276" height="782" alt="Screenshot 2026-11-19 212610" src="https://github.com/user-attachments/assets/f45f0c96-62b7-44fd-ae1b-42edcb8c639c" />

**Question 6**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

```
INSERT into Student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES(201,'David Lee','M','Physics',92);
```

**Output:**

<img width="1291" height="676" alt="Screenshot 2026-11-19 212748" src="https://github.com/user-attachments/assets/b8f567d8-6326-4e66-8344-573a642bdad1" />


**Question 7**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
```
CREATE TABLE Products(
ProductID primary key,
ProductName NOT NULL,
Price real check(Price>0),
Stock integer check(Stock>=0)
);


```

**Output:**

<img width="1250" height="700" alt="Screenshot 2026-11-19 213002" src="https://github.com/user-attachments/assets/ad94963a-32f7-45c1-8081-8f004482f7ea" />


**Question 8**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL CHECK((list_price>=discount) and (list_price>=0)),
discount DECIMAL(10,2) DEFAULT 0 NOT NULL CHECK(discount>=0));

```

**Output:**

<img width="1300" height="730" alt="Screenshot 2026-11-19 213207" src="https://github.com/user-attachments/assets/5f532fa6-c601-412d-ad92-bc004a7e8c9b" />

**Question 9**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```
CREATE TABLE Orders(
OrderID INTEGER PRIMARY KEY,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY(CustomerID)REFERENCES Customers(CustomerID)
);

```

**Output:**

<img width="1276" height="717" alt="Screenshot 2026-11-19 213358" src="https://github.com/user-attachments/assets/3194401c-5aca-4849-8cb1-0076c42c497c" />


**Question 10**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```
INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;

```

**Output:**

<img width="1246" height="712" alt="Screenshot 2026-11-19 213601" src="https://github.com/user-attachments/assets/38887bdc-7397-4f36-be9a-9b72c6933512" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
