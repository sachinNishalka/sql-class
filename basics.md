# 😀 Hi! HND Guys Let` s have fun with SQL 😉

## Plz don`t 😴😴😴 👩‍💻 with 🤓

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

# The SQL INSERT INTO Statement

> The INSERT INTO statement is used to insert new records in a table.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```

# SQL SELECT Statement

> The SELECT statement is used to select data from a database.

```sql
SELECT CustomerName, City FROM Customers;
```

```sql
SELECT * FROM Customers;
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

```sql
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;
```

### SQL Server

```sql
EXEC sp_rename 'table_name.old_name',  'new_name', 'COLUMN';
```

## Modify Data Type

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

# SQL Constraints

> SQL constraints are used to specify rules for data in a table.

> Constraints can be specified when the table is created with the CREATE TABLE statement, or after the table is created with the ALTER TABLE statement.

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);
```

- NOT NULL - Ensures that a column cannot have a NULL value

- UNIQUE - Ensures that all values in a column are different

- PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table

- FOREIGN KEY - Prevents actions that would destroy links between tables

- CHECK - Ensures that the values in a column satisfies a specific condition

- DEFAULT - Sets a default value for a column if no value is specified

- CREATE INDEX - Used to create and retrieve data from the database very quickly

## SQL NOT NULL Constraint

> By default, a column can hold NULL values.

> The NOT NULL constraint enforces a column to NOT accept NULL values.

> This enforces a field to always contain a value, which means that you cannot insert a new record, or update a record without adding a value to this field.

### SQL NOT NULL on CREATE TABLE

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

### SQL NOT NULL on ALTER TABLE

```sql
ALTER TABLE Persons
ALTER COLUMN Age int NOT NULL;
```

## SQL UNIQUE Constraint

> The UNIQUE constraint ensures that all values in a column are different.

> Both the UNIQUE and PRIMARY KEY constraints provide a guarantee for uniqueness for a column or set of columns.

> A PRIMARY KEY constraint automatically has a UNIQUE constraint.

> However, you can have many UNIQUE constraints per table, but only one PRIMARY KEY constraint per table.

### SQL UNIQUE Constraint on CREATE TABLE

```sql
CREATE TABLE Persons (
    ID int NOT NULL UNIQUE,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

> To name a UNIQUE constraint, and to define a UNIQUE constraint on multiple columns, use the following SQL syntax.

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);
```

### SQL UNIQUE Constraint on ALTER TABLE

```sql
ALTER TABLE Persons
ADD UNIQUE (ID);
```

```sql
ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);
```

### DROP a UNIQUE Constraint

```sql
ALTER TABLE Persons
DROP CONSTRAINT UC_Person;
```

## SQL PRIMARY KEY Constraint

> The PRIMARY KEY constraint uniquely identifies each record in a table.

> Primary keys must contain UNIQUE values, and cannot contain NULL values.

> A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields).

### SQL PRIMARY KEY on CREATE TABLE

```sql
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);
```

> In the example above there is only ONE PRIMARY KEY (PK_Person). However, the VALUE of the primary key is made up of TWO COLUMNS (ID + LastName).

### SQL PRIMARY KEY on ALTER TABLE

```sql
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

> To allow naming of a PRIMARY KEY constraint, and for defining a PRIMARY KEY constraint on multiple columns, use the following SQL syntax.

```sql
ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);
```

> If you use ALTER TABLE to add a primary key, the primary key column(s) must have been declared to not contain NULL values (when the table was first created).

### DROP a PRIMARY KEY Constraint

```sql
ALTER TABLE Persons
DROP CONSTRAINT PK_Person;
```

## SQL FOREIGN KEY Constraint

> The FOREIGN KEY constraint is used to prevent actions that would destroy links between tables.

> A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.

> The table with the foreign key is called the child table, and the table with the primary key is called the referenced or parent table.

### SQL FOREIGN KEY on CREATE TABLE

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);
```

> To allow naming of a FOREIGN KEY constraint, and for defining a FOREIGN KEY constraint on multiple columns, use the following SQL syntax

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```

### SQL FOREIGN KEY on ALTER TABLE

```sql
ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

```sql
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

### DROP a FOREIGN KEY Constraint

```sql
ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

## SQL CHECK Constraint

> The CHECK constraint is used to limit the value range that can be placed in a column.

> If you define a CHECK constraint on a column it will allow only certain values for this column.

> If you define a CHECK constraint on a table it can limit the values in certain columns based on values in other columns in the row.

### SQL CHECK on CREATE TABLE

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int CHECK (Age>=18)
);
```

> To allow naming of a CHECK constraint, and for defining a CHECK constraint on multiple columns, use the following SQL syntax

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

### SQL CHECK on ALTER TABLE

```sql
ALTER TABLE Persons
ADD CHECK (Age>=18);
```

```sql
ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');
```

### DROP a CHECK Constraint

```sql
ALTER TABLE Persons
DROP CONSTRAINT CHK_PersonAge;
```

## SQL DEFAULT Constraint

> The DEFAULT constraint is used to set a default value for a column.

> The default value will be added to all new records, if no other value is specified.

### SQL DEFAULT on CREATE TABLE

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);
```

```sql
CREATE TABLE Orders (
    ID int NOT NULL,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);
```

### SQL DEFAULT on ALTER TABLE

```sql
ALTER TABLE Persons
ADD CONSTRAINT df_City
DEFAULT 'Sandnes' FOR City;
```

### DROP a DEFAULT Constraint

```sql
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT;
```

# SQL AUTO INCREMENT Field

> Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table.

> Often this is the primary key field that we would like to be created automatically every time a new record is inserted.

```sql
CREATE TABLE Persons (
    Personid int IDENTITY(1,1) PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

> The MS SQL Server uses the IDENTITY keyword to perform an auto-increment feature.

> In the example above, the starting value for IDENTITY is 1, and it will increment by 1 for each new record.

> To specify that the "Personid" column should start at value 10 and increment by 5, change it to IDENTITY(10,5)

# SQL Dates

- DATE - format YYYY-MM-DD
- DATETIME - format: YYYY-MM-DD HH:MI:SS
- SMALLDATETIME - format: YYYY-MM-DD HH:MI:SS
- TIMESTAMP - format: a unique number

```sql
SELECT * FROM Orders WHERE OrderDate='2008-11-11'
```
