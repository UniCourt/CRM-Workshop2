# Session 1 - Creating tables with constraints
## Create database
Let's create a new database for this workshop handson called 'Bank'

Syntax:

    CREATE DATABASE Bank;

## Create tables
Let's create two new tables 'Account' and 'Transaction'.

| Table Name | Columns |
| --- | --- |
| Account | Account number, Account holder name, Address, Balance, Account status |
| Transaction | Transaction id, Account number, Transaction type, Amount, date, Status |

Syntax:

    CREATE TABLE table_name (
        column1 datatype,
        column2 datatype,
        column3 datatype,
        ....
    );

Example:

    CREATE TABLE account(
        account_number VARCHAR(10),
        name VARCHAR(20),
        address VARCHAR(25),
        balance FLOAT(5),
        account_status VARCHAR(10)
    );

    CREATE TABLE transaction(
        transaction_id INT,
        account_number VARCHAR(10),
        transaction_type VARCHAR(10),
        amount FLOAT(5),
        transaction_date DATETIME,
        status VARCHAR(10)
    );

## View the table

Syntax:

    DESC table_name;

Example:

    DESC account;
    DESC transaction;

## Create table with constraints
Constraints are used to limit the type of data that can go into a table to ensures the accuracy and reliability of data. 

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

---

Let's now drop the table we just created and create new tables with constraints.
Syntax:

    DROP TABLE table_name;

Example:

    DROP TABLE account;
    DROP TABLE transaction;

Account table will have following constraints on the columns,
- Primary key
- Default

Transaction table will have following constraints on the columns
- Auto increment
- Foreign key
- Primary key


Example:

    CREATE TABLE account(
        account_number VARCHAR(10) PRIMARY KEY,
        name VARCHAR(20),
        address VARCHAR(25),
        balance FLOAT(5) DEFAULT 500,
        account_status VARCHAR(10)
    );   

Let's view the tables again and see the constraints we just added.

Example:

    DESC account;
    DESC transaction;

## Excercise

Let's create another table called transaction with following fields with the constraints. Fill the missing gaps to complete the query.

Transaction table will have following constraints on the columns
- Auto increment
- Foreign key
- Primary key

Query:

    CREATE TABLE transaction(
        transaction_id INT PRIMARY KEY  _____________,
        account_number VARCHAR(10),
        transaction_type VARCHAR(10),
        amount __________,
        transaction_date ___________,
        status VARCHAR(10),
        FOREIGN KEY (_____________) REFERENCES __________(______________)
    );