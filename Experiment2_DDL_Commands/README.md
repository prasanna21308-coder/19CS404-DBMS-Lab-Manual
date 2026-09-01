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
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments(
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
    );
```

**Output:**
<img width="1241" height="323" alt="image" src="https://github.com/user-attachments/assets/47fe7195-9def-49f8-aad3-5c78eab7657c" />


**Question 2**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

```sql
INSERT INTO Student_details (RollNo,Name,Gender,Subject,MARKS) VALUES (201,'David Lee','M','Physics',92)
```

**Output:**

<img width="1243" height="340" alt="image" src="https://github.com/user-attachments/assets/6d82878a-0422-4f0a-aba9-7c9f10bf53f3" />

**Question 3**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

 

 

```sql
ALTER TABLE employees ADD COLUMN salary INTEGER CHECK (salary>0)
```

**Output:**

<img width="1233" height="368" alt="image" src="https://github.com/user-attachments/assets/de56ec1e-a078-4ed3-b7f5-fc627ca1d41d" />


**Question 4**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE
 

 

```sql
ALTER TABLE Companies ADD COLUMN designation varchar(50);
ALTER TABLE Companies ADD COLUMN net_salary number;
ALTER TABLE Companies ADD COLUMN dob date;
```

**Output:**
<img width="1232" height="513" alt="image" src="https://github.com/user-attachments/assets/50ec5d45-4f48-4e24-9cc0-c1b91bcf1658" />



**Question 5**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
```sql
CREATE TABLE Orders(
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**
 <img width="1228" height="376" alt="image" src="https://github.com/user-attachments/assets/e3dcbc92-10d1-4ad8-a51b-a9248a55550d" />


**Question 6**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present','Absent','Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    );
```

**Output:**

<img width="1231" height="377" alt="image" src="https://github.com/user-attachments/assets/e91e8c64-ee8a-4761-8347-860e6c32959b" />


**Question 7**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```sql
INSERT INTO Employee SELECT * FROM Former_employees;
```

**Output:**

<img width="1233" height="365" alt="image" src="https://github.com/user-attachments/assets/eac9b55d-0630-447c-961d-19f49916bb5e" />


**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
```sql
CREATE TABLE Products(
    ProductID PRIMARY KEY,
    ProductName NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK(Stock>=0)
);
```

**Output:**

<img width="1247" height="366" alt="image" src="https://github.com/user-attachments/assets/bfde3564-c70b-4f67-9fe6-892b2fced42f" />


**Question 9**
---
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000

```sql
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary) VALUES (2,'John Smith','Developer','IT',75000);
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary) VALUES (3,'Anna Bell','Designer','Marketing',68000);
```

**Output:**
<img width="1240" height="447" alt="image" src="https://github.com/user-attachments/assets/26da3683-633a-48c4-9609-b6e5ef235bf2" />


**Question 10**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT

```sql
CREATE TABLE Departments(
    DepartmentID INTEGER,
    DepartmentName TEXT


);
```

**Output:**

<img width="1238" height="447" alt="image" src="https://github.com/user-attachments/assets/1028a1cd-5153-4399-8626-791da52b3caa" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
