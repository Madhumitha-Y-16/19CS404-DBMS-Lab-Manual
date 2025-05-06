# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
```
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8
```
```sql
SELECT COUNT(customer_id) AS COUNT FROM customer;
```

**Output:**

![image](https://github.com/user-attachments/assets/b9fb1c22-cd1f-42a6-9a87-1451cce9ea6a)


**Question 2**
---
```
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15

```

```sql
SELECT name as fruit_name, min(inventory) as lowest_quantity from fruits;
```

**Output:**

![image](https://github.com/user-attachments/assets/79db83e5-65c9-432f-8e26-3a267c18c33e)


**Question 3**
---
```
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
COUNT
----------
6

```

```sql
select  count( distinct salesman_id ) as COUNT FROM orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/3fc4e20c-5e34-4878-b61d-4d3ba95ad5f8)


**Question 4**
```
Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name        email           min_email_length
----------  --------------  ----------------
Ravi Kumar  ravi@gmail.com  14

```

```sql
select name,email, min(length(email)) as min_email_length from customer;
```

**Output:**

![image](https://github.com/user-attachments/assets/b0518f41-cfaf-4e22-8dbf-021bc1be57d5)


**Question 5**

```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1
```
![image](https://github.com/user-attachments/assets/98725ead-209f-434c-9d60-a8f1977af9d6)

```
```
For example:

Result
jdate       MIN(workhour)
----------  -------------
2002.0      9
2004.0      9
2006.0      9

```
select jdate, MIN(workhour) from employee1 
group by jdate having MIN(workhour) < 10;
```

**Output:**

![image](https://github.com/user-attachments/assets/be2717a1-2ee6-4a84-858a-4ca7f3d5a17c)


**Question 6**
---
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 
Note: Inventory attribute contains amount of fruits

Table: fruits
```
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
```

```sql
SELECT SUM(inventory) 
AS total_available_amount 
FROM fruits
WHERE price > 0.5;
```

**Output:**

![image](https://github.com/user-attachments/assets/4e2baf2c-03c1-478e-ab96-78bb52bdf718)

**Question 7**
---
Write a SQL query to find the youngest employee in the company?

Table: employee
```
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```

```sql
SELECT name AS Employee_Name,
age AS Age
FROM employee
ORDER BY age ASC
LIMIT 1;

```

**Output:**

![image](https://github.com/user-attachments/assets/f795fa76-00d4-4910-9486-0fa8eed5b3f0)

**Question 8**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products
![image](https://github.com/user-attachments/assets/d31e75af-762b-4bc9-b695-a4801d30f3e4)

```sql
SELECT category_id,
COUNT(product_name) AS 'count(product_name)'
FROM products
WHERE category_id < 3
GROUP BY category_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/9f3ddca8-edb6-471c-ae5c-1a5d0866895c)

**Question 9**
---
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1
![image](https://github.com/user-attachments/assets/1bb42ba1-861f-4a2e-85fb-996909595b8e)

```sql
SELECT 
(age/5) * 5 AS age_group,
MIN(salary) AS 'MIN(salary)'
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(salary) < 2000
```

**Output:**

![image](https://github.com/user-attachments/assets/0c8b928d-ecfa-4d41-bcd8-d02bd6d54349)

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1
![image](https://github.com/user-attachments/assets/94c39ded-93b2-444c-b087-ee607c875d49)

 ```sql
SELECT jdate,
   SUM(workhour) AS 'SUM(workhour)'
FROM employee1
GROUP BY jdate
HAVING SUM(workhour) > 40
ORDER BY jdate;
```

**Output:**

![image](https://github.com/user-attachments/assets/76bdd1a0-44a9-4517-944f-135e00bc50a7)

### SCREENSHOT OF SEB MODULE COMPLETION:
![{5B56F494-9583-452E-97AE-21ED044FEE82}](https://github.com/user-attachments/assets/d0a86b8d-d40d-4b8f-a4d6-055a0b0cb45a)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
