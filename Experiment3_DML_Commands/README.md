# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
```
Write a SQL statement to double the availability of the product with product_id 1.

products table

---------------
product_id
product_name
category_id
availability
```

```sql
update products
set availability = 2 * availability
where product_id = 1;
```

**Output:**

![Screenshot_30-4-2025_104615_lms2 cse saveetha in](https://github.com/user-attachments/assets/441d7c88-5317-4f3f-8b9d-ce8710861443)


**Question 2**
---
```Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE department_id = 20;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
201          Michael     MHARTSTE    26000       MK_MAN
202          Pat         PFAY        6000        MK_REP
```

```sql
update Employees
set salary = salary * 2
where department_id = 20 and job_id like '%MAN';
```

**Output:**

![image](https://github.com/user-attachments/assets/7925960e-0721-4f2b-af2c-177957da7b66)


**Question 3**
---
```
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test	Result
select changes();
changes()
----------
1

```
```sql
update Suppliers
set address = '58 Lakeview, Magnolia'
where supplier_id = 5;
```

**Output:**

![image](https://github.com/user-attachments/assets/01d3590d-87d8-4a0f-a0db-067bc3a9c4b3)


**Question 4**
---
```
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability
```

```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**

![image](https://github.com/user-attachments/assets/698ae9f9-c6ee-4ae7-989a-5cecec2b1c17)

**Question 5**
---
```Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
```

```sql
delete from Surgeries where surgery_id = 3;
```

**Output:**

![image](https://github.com/user-attachments/assets/fc7924c0-f735-4b75-8ef7-98c8f9097ff0)


**Question 6**
---
```
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' has exactly 6 characters.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00012      Steven      San Jose    San Jose      USA           1           5000         7000         9000         3000             KRFYGJK     A012
C00003      Martin      Torento     Torento       Canada        2           8000         7000         7000         8000             MJYURFD     A004
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
changes()
----------
6
```

```sql
delete from Customer where LENGTH(CUST_NAME )=6;
```

**Output:**

![image](https://github.com/user-attachments/assets/bac8c5ea-bc01-4227-ac06-cdbe9df8e8f1)


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.
Sample table: Customer
```
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM Customer
WHERE CUST_NAME LIKE '%Holmes%';
```

**Output:**

![image](https://github.com/user-attachments/assets/5c6cc0a6-ba4d-4d87-8220-96e1f5494358)

**Question 8**
---
Write a SQL query to Delete All Doctors with a NULL Last Name.
- Sample table: Doctors
- attributes : doctor_id, first_name, last_name, specialization

```sql
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/d679c15a-f249-49da-9400-cf84fc44206d)

**Question 9**
---
```
Write a SQL query to Select all patients who were admitted during the year 2023.

Table: Patients

name                  type
--------------------  ----------
patient_id            INT
first_name            VARCHAR(50)
last_name             VARCHAR(50)
date_of_birth         DATE
admission_date        DATE
discharge_date        DATE
doctor_id             INT
For example:

Result
patient_id  first_name  admission_date
----------  ----------  --------------
4           Abhishek    2023-02-10
5           Alice       2023-08-02

```


```sql
select patient_id, first_name, admission_date from Patients where STRFTIME('%Y',admission_date) = '2023';
```

**Output:**

![image](https://github.com/user-attachments/assets/e3804fab-f3d4-4224-b500-4d48c5c2e373)


**Question 10**
---
```
Write a SQL query to calculate the absolute value of the value1 column from the Calculations table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          value1      absolute_value
----------  ----------  --------------
1           -87.65      87.65
2           45.78       45.78
3           89.99       89.99
4           -0.005      0.005

```

```sql
select id,value1, abs(value1) as absolute_value
from Calculations;
```

**Output:**

![image](https://github.com/user-attachments/assets/7545d60d-27c6-4a54-91ca-6048ffe6d31d)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
