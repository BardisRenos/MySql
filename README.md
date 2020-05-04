# MySql

This repository has a number of Sql queries examples. 

### Creating the database

Firstly, it is necessary to create a database. In our case I create the ***Test_MySql*** database.

```sql
  create database Test_MySql;
```

The console can shows us the result.
``
mysql> create database Test_MySql;
Query OK, 1 row affected (0.00 sec)
``
### How to show the databases

```sql
  show databases;
```

|Databases|
|---------|
| information_schema |
| Test_MySql         |
| mysql              |
| performance_schema |
| sys  |


### Create the tables into the new database

After creating the database table, I have to build the tables inside of the Test_MySql database.

```sql
  use Test_MySql;
```
The database is activated and I can create tables into it.

```sql
mysql> use Test_MySql;

Database changed
```

### Create the tables


```sql
  mysql> CREATE TABLE IF NOT EXISTS `agents` (
    ->   `AGENT_CODE` varchar(6) NOT NULL DEFAULT '',
    ->   `AGENT_NAME` varchar(40) DEFAULT NULL,
    ->   `WORKING_AREA` varchar(35) DEFAULT NULL,
    ->   `COMMISSION` decimal(10,2) DEFAULT NULL,
    ->   `PHONE_NO` varchar(15) DEFAULT NULL,
    ->   `COUNTRY` varchar(25) DEFAULT NULL,
    ->   PRIMARY KEY (`AGENT_CODE`)
    -> ) ENGINE=MyISAM DEFAULT CHARSET=latin1;

```

### SELECT statement 

With the select statement, can shows the column what containce..

```sql
  SELECT column_name FROM table_name
  
```

If want to show all the columns then.

```sql
  SELECT * FROM table_name
```

### TOP, PERCENT or LIMIT 

The limit statement shows the

```sql
  SELECT * FROM company limit 7;
```
The same patter follows 

```sql
  SELECT TOP 3 * FROM company
```

```sql
  SELECT TOP 50 PERCENT * FROM company
```


### DISTINCT statement

The distinct statement selects only the unique values from the given column in the database table.

```sql
  SELECT DISTINCT(COMPANY_CITY) FROM company
```

If you want to show show many unuique values are then:

```sql
  SELECT COUNT(DISTINCT(COMPANY_CITY)) FROM company
```
Lastly, if you want to show how many elements where duplicate, then:

```sql
  SELECT COUNT(*) - COUNT(DISTINCT(COMPANY_CITY)) FROM company
```


### Where statement

The where statement is like filter in the SQL query. 

```sql
  SELECT * FROM company WHERE COMPANY_ID = 18
```

It is also possible to filter with string

```sql
  SELECT * from company WHERE COMPANY_NAME = 'Akas Foods'
```

Also the where statement can be used with a range of values with the **BETWEEN**

```sql
  SELECT * from company WHERE COMPANY_ID BETWEEN 16 AND 19
```

If you want to filter a column name by the starting letter. Then you can use the statement **LIKE** and the **%** to indicate if you search regarding the first letter, the last letter or in between. 

```sql
  SELECT * FROM company WHERE COMPANY_CITY LIKE 'B%'
```

Filtering the column by the last letter.

```sql
  SELECT * FROM company WHERE COMPANY_NAME LIKE '%s'
```

Filtering the column by the letter in any position. 

```sql
  SELECT * FROM company WHERE COMPANY_NAME LIKE '%s%'
```

If you want to specify the position of the letter that you are searching. In this case the query is searching ***k*** letter in the 4th position.

```sql
  SELECT * FROM company WHERE COMPANY_NAME LIKE '___k%'
```

If you want to search any values that start with ***F*** and are at least 3 characters in length.

```sql
  SELECT * FROM company WHERE COMPANY_NAME LIKE 'F__%'
```

Searching any values that start from **J** and ends with **d**

```sql
  SELECT * FROM company WHERE COMPANY_NAME LIKE 'J%d'
```

The **IN** operator allows you to specify multiple values in a WHERE clause. The IN operator is a shorthand for multiple OR conditions. This query shows all the columns when the working_area column has 'London' or 'New York' 

```sql
  SELECT * from agents WHERE WORKING_AREA IN ('London', 'New York') 
```

In this case the query shows all the columns from company that are also in the column WORKING_AREA in agent table.

```sql
  SELECT * FROM company WHERE COMPANY_CITY IN (SELECT WORKING_AREA FROM agents)
```

The SQL **AND**, **OR** and **NOT** Operators. The WHERE clause can be combined with AND, OR, and NOT operators.

For example:

```sql
  SELECT * FROM company WHERE COMPANY_NAME = 'Foodies.' OR COMPANY_NAME = 'Order All'
```

```sql
  SELECT * FROM company WHERE COMPANY_NAME = 'Foodies.' AND COMPANY_ID = 17
```

```sql
  SELECT * FROM company WHERE NOT COMPANY_NAME = 'Foodies.'
```

### ORDER BY

The ORDER BY keyword is used to sort the result-set in ascending or descending order. For example:

```sql
  SELECT * FROM company ORDER by COMPANY_CITY 
```

```sql
  SELECT * FROM company ORDER by COMPANY_CITY ASC
```

```sql
  SELECT * FROM company ORDER by COMPANY_CITY DESC
```

```sql
  SELECT * FROM company ORDER by COMPANY_CITY ASC, COMPANY_NAME DESC
```


### How to check for NULL Values ?

It is common that inside to a sql database table will be NULL values.

```sql
  SELECT * from customer WHERE GRADE is NULL
```

```sql
  SELECT * from customer WHERE GRADE is not NULL
```

### MIN & MAX 

The MIN() function returns the smallest value of the selected column. Whereas, the MAX() function returns the largest value of the selected column.

```sql
  SELECT MAX(GRADE) from customer; 
```

```sql
  SELECT MIN(GRADE) from customer; 
```

### The SQL COUNT(), AVG() and SUM() functions

The COUNT() returns the number of rows that matches a specified criteria. The AVG() returns the average value of a numeric column. The SUM() returns the total sum of a numeric column. 

```sql
  SELECT AVG(OPENING_AMT) FROM customer
```

```sql
  SELECT SUM(OPENING_AMT) FROM customer
```

```sql
  SELECT COUNT(*) FROM customer
```

### SQL Wildcards

A wildcard character is used to substitute one or more characters in a string. Wildcard characters are used with the SQL LIKE operator. The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

This query show all the rows where the CUST_CITY starts with ***lon*** characters.

```sql
  SELECT * FROM customer where CUST_CITY LIKE 'lon%'
```

This query shows all the columns from **customer** when the **CUST_CITY** has the ***ga*** pattern.

```sql
  SELECT * from customer WHERE CUST_CITY LIKE '%ga%'
```

This query shows all the columns from **customer** when the **CUST_CITY** starts with the *L* as a first letter then followed from any letter as a third character has ***n*** and the fourth any letter. Last two letters end with ***on***

```sql
  SELECT * FROM customer WHERE WORKING_AREA LIKE 'L_n_on'
```



### The IN statement 

The IN operator allows you to specify multiple values in a WHERE clause. The IN operator is a shorthand for multiple OR conditions.


This query shows all the columns when the ***WORKING_AREA*** equals with *New York* or with *London*

```sql
  SELECT * FROM agents WHERE WORKING_AREA IN ('New York', 'London')
```

Whereas, the second sql query shows all column when ***WORKING_AREA*** is not equals with *New York* or with *London*

```sql
  SELECT * FROM agents WHERE WORKING_AREA NOT IN ('New York', 'London')
```

In this case the query shows all the columns only if the ***WORKING_AREA*** values are the same  
with the ***WORKING_AREA*** column on the customer table.

```sql
  SELECT * FROM agents WHERE WORKING_AREA IN (SELECT WORKING_AREA FROM customer)
```

### The JOIN statement

A JOIN clause is used to combine rows from two or more tables, based on a related column between them. There are 4 types of joins. Like,
- (INNER) JOIN: Returns records that have matching values in both tables
- LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table
- RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table
- FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table

This query shows INNER join
```sql
  SELECT agents.AGENT_NAME, customer.CUST_NAME FROM agents
  INNER JOIN customer ON agents.AGENT_CODE = customer.AGENT_CODE ORDER BY AGENT_NAME
```

The right join query.
```sql
```

### The self join 

A self JOIN is a regular join, but the table is joined with itself.

### Having statement 

The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.

```sql
  SELECT CUST_CITY, count(GRADE) from customer GROUP BY CUST_CITY HAVING COUNT(GRADE) >2 order by CUST_CITY desc

```

