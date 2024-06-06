# Create Database

```sql
CREATE DATABASE databasename;
```

# Drop database

```sql
DROP DATABASE databasename;
```

# Backup Database

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak';
```

# Create Table

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

# Create Table Using Another Table

```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```

```sql
CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers;
```

# Drop Table

```sql
DROP TABLE table_name;
```

# Truncate Table

> The TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself.

```sql
TRUNCATE TABLE table_name;
```

# Alter Table

> The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.

> The ALTER TABLE statement is also used to add and drop various constraints on an existing table.

## ADD Column

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

```sql
ALTER TABLE Customers
ADD Email varchar(255);
```

## Drop Column

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

```sql
ALTER TABLE Customers
DROP COLUMN Email;
```

## Rename Column
