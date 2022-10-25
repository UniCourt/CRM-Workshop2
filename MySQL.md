# MySQL Hands on:

# Creating tables with constraints
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

## Create table with constraints
Account table will have following constraints on the columns,
- 

Example:

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

    DESC transaction;

## MySQL Constraints
