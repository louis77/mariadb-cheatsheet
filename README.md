# MariaDB SQL Cheat Sheet

Everything you need for your daily work with MariaDB.
Tested with MariaDB version 10.6.5, but should work with most versions.

- [MariaDB SQL Cheat Sheet](#mariadb-sql-cheat-sheet)
  - [Use the CLI](#use-the-cli)
      - [Switch to database](#switch-to-database)
  - [DATABASES](#databases)
      - [List all databases](#list-all-databases)
      - [Show database definition](#show-database-definition)
      - [Create database](#create-database)
      - [Re-create (drop + create) database (>= 10.1.3)](#re-create-drop--create-database--1013)
      - [Drop database](#drop-database)
  - [PROCEDURES / FUNCTIONS](#procedures--functions)
      - [Create stored procedure](#create-stored-procedure)
      - [Alter stored procedure's characteristics](#alter-stored-procedures-characteristics)
      - [Replace stored procedure (>= 10.1.3)](#replace-stored-procedure--1013)
  - [TABLES](#tables)
      - [List all tables](#list-all-tables)
      - [Show tables columns](#show-tables-columns)
      - [Show CREATE defintion of table](#show-create-defintion-of-table)
    - [COLUMNS](#columns)
      - [Drop one or more columns](#drop-one-or-more-columns)
      - [Rename column and/or modify column definition](#rename-column-andor-modify-column-definition)
      - [Modify column definition](#modify-column-definition)
    - [INDEXES](#indexes)
      - [Add primary key to an existing table](#add-primary-key-to-an-existing-table)
  - [SECURITY](#security)
      - [List grants for current user](#list-grants-for-current-user)
      - [Grant execute procedure to user/role](#grant-execute-procedure-to-userrole)
  - [MONITOR](#monitor)
      - [List open connections and running queries](#list-open-connections-and-running-queries)
  - [OPTIMIZE](#optimize)
      - [Analyze columns of table and get optimal field recommendations](#analyze-columns-of-table-and-get-optimal-field-recommendations)
- [LICENSE](#license)



## Use the CLI

Use `mariadb` CLI for the best experience. List of all client commands:

```
MariaDB [(none)] help

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

#### Switch to database

```sql
USE db1
```

To output result in columnar format (default), use default delimiter`;

```sql
SHOW TABLES;
```

To output results in record format, use ` \G` delimiter:`

```sql
SHOW CREATE TABLE tab1\G
```

Temporarly change default delimiter (used to create procedures, functions, events etc.) 

```sql
DELIMITER $$

// do your stuff here
// CREATE PROCEDURE .... END;
$$

DELIMITER ;
```

## DATABASES

#### List all databases

```sql
SHOW DATABASES
```

#### Show database definition 
(use `\G`)

```sql
SHOW CREATE DATABASE db1
```

#### Create database 
(in MariaDB databases and schemas are the same thing)

```sql
CREATE DATABASE [IF NOT EXISTS] db1
	-- optional
	CHARACTER SET = 'utf8mb4'
	COLLATE = 'utf8_general_bin'
	COMMENT = 'my new database'
```

#### Re-create (drop + create) database (>= 10.1.3)

```sql
CREATE OR REPLACE DATABASE db1
``` 

#### Drop database

```sql
DROP DATABASE [IF EXISTS] db1
```

## PROCEDURES / FUNCTIONS

#### Create stored procedure

```sql
CREATE PROCEDURE proc1 ()
BEGIN
    // do something here
END;
```

#### Alter stored procedure's characteristics

```sql
ALTER PROCEDURE proc1
  { CONTAINS SQL | NO SQL | READS SQL DATA | MODIFIES SQL DATA }
  | SQL SECURITY { DEFINER | INVOKER }
  | COMMENT 'string'
```

#### Replace stored procedure (>= 10.1.3)
Using this will keep privileges granted for this procedure.

```
CREATE OR REPLACE PROCEDURE proc1 ()
BEGIN
    // do something new here
END;
```


## TABLES

#### List all tables

```sql
SHOW TABLES
```

#### Show tables columns

```sql
DESC t1
```

#### Show CREATE defintion of table 
(use `\G`)

```sql
SHOW CREATE TABLE t1
```

### COLUMNS

#### Drop one or more columns

```sql
ALTER TABLE t1 DROP COLUMN col1, DROP COLUMN col2
```

#### Rename column and/or modify column definition

```sql
ALTER TABLE t1 CHANGE col1old col1new VARCHAR(50) NOT NULL
```

#### Modify column definition

```sql
ALTER TABLE t1 MODIFY col1 VARCHAR(50) NOT NULL
```

### INDEXES

#### Add primary key to an existing table

```sql
ALTER TABLE t1 ADD PRIMARY KEY (col1, col2)
```

## SECURITY

#### List grants for current user

```sql
// for current user
SHOW GRANTS

// for user
SHOW GRANTS FOR user1
SHOW GRANTS FOR user1@host1
```

#### Grant execute procedure to user/role

```sql
GRANT EXECUTE ON PROCEDURE sp1 TO user1@%;
GRANT EXECUTE ON PROCEDURE sp1 TO role1;
```

## MONITOR

#### List open connections and running queries

```sql
SHOW PROCESSLIST
SHOW FULL PROCESSLIST
```

## OPTIMIZE

#### Analyze columns of table and get optimal field recommendations

```sql
SELECT col1, col2 FROM t1 PROCEDURE ANALYZE()
```

# LICENSE

© Louis Brauer, 2022. License: see `LICENSE`.

