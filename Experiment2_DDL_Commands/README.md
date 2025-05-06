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
```
Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           name        varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           designatio  varchar(50  0                       0
6           net_salary  number      0                       0
```

```sql
ALTER TABLE Companies
ADD COLUMN designation varchar(50);

alter table Companies
ADD COLUMN net_salary number;
```

**Output:**
![image](https://github.com/user-attachments/assets/ff09cad4-26d9-4feb-89c3-0eeb14bf4831)


**Question 2**
```
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1
```

```sql
create table Invoices(
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK(Amount > 0),
    DueDate DATE CHECK(DueDate > InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID));
```

**Output:**
![image](https://github.com/user-attachments/assets/e60b88da-d247-4ac8-8e2f-d4690e55fcd9)


**Question 3**
```
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	Result
INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
SELECT * FROM contacts;

```

```sql
create table contacts(
        contact_id INTEGER PRIMARY KEY,
        first_name TEXT NOT NULL,
        last_name TEXT NOT NULL,
        email TEXT,
        phone TEXT NOT NULL CHECK(length(phone)= 10));
```

**Output:**
![image](https://github.com/user-attachments/assets/f8426231-418a-4aa8-8722-2468b30b0c68)


**Question 4**
```
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
 
For example:

Test	Result
SELECT RollNo, Name, Gender 
FROM Student_details 
WHERE RollNo = 204;


RollNo      Name          Gender
----------  ------------  ----------
204         Samuel Black  M

```
```sql
INSERT INTO Student_details(RollNo, Name, Gender)
values (204, 'Samuel Black', 'M');
```

**Output:**
![image](https://github.com/user-attachments/assets/8cd408c1-2f34-4147-9de3-b3e236fb2b4d)


**Question 5**
```
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10
```

```sql
CREATE TABLE Products(
        ProductID INTEGER PRIMARY KEY,
        ProductName TEXT UNIQUE NOT NULL,
        Price REAL CHECK(Price > 0),
        StockQuantity INTEGER CHECK(StockQuantity >= 0));
```

**Output:**

![image](https://github.com/user-attachments/assets/57e2de1f-7f6d-454a-a718-799b2b5221c8)

**Question 6**
```
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5

```

```sql
INSERT INTO Products(ProductID, ProductName, Price, Stock)
select * from Discontinued_products;
```

**Output:**


**Question 7**
```
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER
For example:

Test	Result
pragma table_info('Orders');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     OrderID     INTEGER     0                       0
1     OrderDate   TEXT        0                       0
2     CustomerID  INTEGER     0                       0

```

```sql
CREATE TABLE Orders(
        OrderID INTEGER,
        OrderDate TEXT,
        CustomerID INTEGER);
```

**Output:**
![image](https://github.com/user-attachments/assets/27739b56-4b83-40e2-ba82-4fe8922cde90)


**Question 8**
```
Write an SQL command can to add a column named email of type TEXT to the customers table

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0

```

```sql
ALTER TABLE Customers
add column email TEXT;
```

**Output:**
![image](https://github.com/user-attachments/assets/dbd2adf0-707b-476b-a508-28d3505438db)


**Question 9**
```
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021
For example:

Test	Result
SELECT * FROM Books;
ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```

```sql
INSERT INTO Books(ISBN,Title,Author,Publisher,Year)
values ('978-1234567890','Introduction to AI','John Doe','',''),
        ('978-9876543210','Deep Learning','Jane Doe','TechPress','2022'),
        ('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith','', '2021');
```

**Output:**
![image](https://github.com/user-attachments/assets/03b615fc-fe25-46e2-b6ad-628414db6a9f)


**Question 10**
```
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1
```
```sql
CREATE TABLE Orders(
        OrderID INTEGER PRIMARY KEY,
        OrderDate DATE NOT NULL,
        CustomerID INTEGER,
        FOREIGN KEY(CustomerID) REFERENCES Customers(CustomerID));
```

**Output:**
![image](https://github.com/user-attachments/assets/d7b4a873-8f2f-4c1f-be6d-c297d1aa9ad9)

### SCREENSHOT OF SEB MODULE COMPLETION:
![Screenshot (60)](https://github.com/user-attachments/assets/4224b851-ca81-4284-a325-f2da403f5252)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
