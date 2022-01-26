- [MariaDB Cheat Sheet](#mariadb-cheat-sheet)
  - [Basics](#basics)
  - [SELECT](#select)
  - [DATABASES](#databases)
  - [PROCEDURES / FUNCTIONS](#procedures--functions)
  - [TABLES](#tables)
  - [COLUMNS](#columns)
  - [INDEXES](#indexes)
  - [ACCOUNTS](#accounts)
  - [SHOW](#show)
  - [OPTIMIZE](#optimize)

# MariaDB Cheat Sheet

Everything you need for your daily with with MariaDB.

© Louis Brauer, 2022. License: see `LICENSE`.

## Basics

Use `mariadb` CLI for the best experience. List of all client commands:

```
Note that all text commands must be first on line and end with ';'

?         (\?) Synonym for `help'.
clear     (\c) Clear the current input statement.
connect   (\r) Reconnect to the server. Optional arguments are db and host.
delimiter (\d) Set statement delimiter.
ego       (\G) Send command to MariaDB server, display result vertically.
exit      (\q) Exit mysql. Same as quit.
go        (\g) Send command to MariaDB server.
help      (\h) Display this help.
notee     (\t) Don't write into outfile.
print     (\p) Print current command.
prompt    (\R) Change your mysql prompt.
quit      (\q) Quit mysql.
rehash    (\#) Rebuild completion hash.
source    (\.) Execute an SQL script file. Takes a file name as an argument.
status    (\s) Get status information from the server.
tee       (\T) Set outfile [to_outfile]. Append everything into given outfile.
use       (\u) Use another database. Takes database name as argument.
charset   (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.
warnings  (\W) Show warnings after every statement.
nowarning (\w) Don't show warnings after every statement.
```

Switch to a database

```sql
USE db1
```

To output result in columnar format (default), use default delimiter`;`

```sql
SHOW TABLES;
```

To output results in record format, use ` \G` delimiter:`

```sql
SHOW CREATE TABLE tab1\G
```

Temporarely change default delimiter (used to create procedures, functions, events etc.) 

```sql
DELIMITER $$

// do your stuff here
// CREATE PROCEDURE .... END;
$$

DELIMITER ;
```

## SELECT

## DATABASES

List of all databases

```sql
SHOW DATABASES
```

Create database

```sql
CREATE DATABASE db1
```

Drop database

```sql
DROP DATABASE db1
```

## PROCEDURES / FUNCTIONS

Create stored procedure

```sql
CREATE PROCEDURE proc1 ()
BEGIN
    // do something here
END;
```

## TABLES

List all tables

```sql
SHOW TABLES
```

Show table columns in tabular format

```sql
DESC t1
```

Show CREATE defintion of table

```sql
SHOW CREATE TABLE t1 \G
```

## COLUMNS

Drop one or more columns

```sql
ALTER TABLE t1 DROP COLUMN col1, DROP COLUMN col2
```

Rename column and/or modify column definition

```sql
ALTER TABLE t1 CHANGE col1old col1new VARCHAR(50) NOT NULL
```

Modify column definition

```sql
ALTER TABLE t1 MODIFY col1 VARCHAR(50) NOT NULL
```

## INDEXES

Add primary key to an existing table

```sql
ALTER TABLE t1 ADD PRIMARY KEY (col1, col2)
```

## ACCOUNTS

Grant execute procedure to user/role

```sql
GRANT EXECUTE ON PROCEDURE sp1 TO user1@%;
GRANT EXECUTE ON PROCEDURE sp1 TO role1;
```

## SHOW

Running queries / Open connections

```sql
SHOW PROCESSLIST
SHOW FULL PROCESSLIST
```

## OPTIMIZE

Analyze columns of a table and get optimal field recommendations

```sql
SELECT col1, col2 FROM t1 PROCEDURE ANALYZE()
```
