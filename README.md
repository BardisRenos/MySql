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
