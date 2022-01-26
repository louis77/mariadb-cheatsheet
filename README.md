# MariaDB Cheat Sheet

 © Louis Brauer, 2022

## 

## DATA

### SELECT



## DEFINITIONS

#### DATABASES

Create database

```sql
CREATE DATABASE db1
```

#### PROCEDURES / FUNCTIONS

Create stored procedure

```sql
CREATE PROCEDURE proc1 ()
BEGIN
    // do something here
END;
```



### TABLES

Show table columns in tabular format

```sql
DESC t1
```

Show CREATE defintion of table

```sql
SHOW CREATE TABLE t1 \G
```



#### COLUMNS

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

#### INDEXES

Add primary key to an existing table

```sql
ALTER TABLE t1 ADD PRIMARY KEY (col1, col2)
```

#### ACCOUNTS

Grant execute procedure to user/role

```sql
GRANT EXECUTE ON PROCEDURE sp1 TO user1@%;
GRANT EXECUTE ON PROCEDURE sp1 TO role1;
```



### SHOW

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
