# MySQL Cheatsheet:
# General Queries:
## Create database
The CREATE DATABASE statement is used to create a new SQL database.

Syntax:

    CREATE DATABASE databasename;
## Create table
The CREATE TABLE statement is used to create a new table in a database.

    CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
    ....
    );

## Insert records to table
The INSERT INTO statement is used to insert new records in a table.

Syntax:

    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...);

## Update records
The UPDATE statement is used to modify the existing records in a table.

Syntax:

    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    WHERE condition;

## Delete records
The DELETE statement is used to delete existing records in a table. The WHERE clause specifies which record(s) should be deleted. If you omit the WHERE clause, all records in the table will be deleted!

Syntax:

    DELETE FROM table_name WHERE condition;

## Select records
The SELECT statement is used to select data from a database. The data returned is stored in a result table, called the result set.

Syntax:

    SELECT column1, column2, ...
    FROM table_name;

If you want to select all the fields available in the table, we use * instead of column names in the syntax.

Syntax:

    SELECT * FROM table_name;

## Alter table
The ALTER TABLE statement is used to,
- add, delete, or modify columns in an existing table.
- add and drop various constraints on an existing table.

## Alter table - Add column

Syntax:

    ALTER TABLE table_name
    ADD column_name datatype;

## Alter table - Drop column

Syntax:

    ALTER TABLE table_name
    DROP COLUMN column_name;

## Alter table - Modify column

Syntax:

    ALTER TABLE table_name
    MODIFY COLUMN column_name datatype;

## Alter table - Change data type

Syntax:

    ALTER TABLE Persons
    MODIFY COLUMN DateOfBirth year;

## Alter table - Add new constraint

Syntax:

    ALTER TABLE table_name
    ADD CONSTRAINT constraint_name contraint_type (column1, column2, ... column_n);

## Drop table
The DROP TABLE statement is used to drop an existing table in a database.

Syntax:

    DROP TABLE table_name;

# MySQL Constraints
Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

The following constraints are the commonly used ones,

| Constraints | Description |
| --- | ----------- |
| PRIMARY KEY | A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table |
| FOREIGN KEY | Prevents actions that would destroy links between tables|
| NOT NULL | Ensures that a column cannot have a NULL value|
| UNIQUE | Ensures that all values in a column are different |
| CHECK | Ensures that the values in a column satisfy a specific condition |
| DEFAULT | Sets a default value for a column if no value is specified |
| CREATE INDEX | Used to create and retrieve data from the database very quickly |

## Adding Constraints
There are two ways to add the constraints,
- Adding constraints while creating tables
- Adding constraints to existing columns in tables

## Adding constraints - create table
Syntax:

    CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
    ....
    constraint (column)
    );

## Adding constraints - alter table
Syntax:
    
    ALTER TABLE table_name
    ADD CONSTRAINT constraint_name contraint_type (column1, column2, ... column_n);

# MySQL Logical Operators

| Operator | Description |
| --- | ----------- |
| ALL | TRUE if all of the subquery values meet the condition |
| AND | TRUE if all the conditions separated by AND is TRUE |
| ANY | TRUE if any of the subquery values meet the condition |
| BETWEEN | TRUE if the operand is within the range of comparisons |
| EXISTS | TRUE if the subquery returns one or more records |
| IN | TRUE if the operand is equal to one of a list of expressions |
| LIKE | TRUE if the operand matches a pattern |
| NOT | Displays a record if the condition(s) is NOT TRUE |
| OR | TRUE if any of the conditions separated by OR is TRUE |
| SOME | TRUE if any of the subquery values meet the condition |