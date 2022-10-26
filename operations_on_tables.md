# Operations on tables

Let's start by viewing the tables we created.

Example:

    DESC account;
    DESC transaction;

## Add new columns to the table

Let's add a new column called phone_number to the account table.

Syntax:

    ALTER TABLE table_name
    ADD column_name datatype;

Example,

    ALTER TABLE account
    ADD phone_number INT(10);

## Insert records

Let's insert some data to the tables now.

Syntax:

    INSERT INTO account (account_number, name, address, account_status, phone_number)
    VALUES ('SB101', 'Anna', 'M.G Road, Bangalore', 'Active', '9113456578');

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Credit', '2000', '2022-10-27 03:00:00', 'Success');

## View the records in the table

We make use of SELECT command to view the data present in any table. Let's write a simple SELECT query to find out what's in our tables.

Syntax:

    SELECT * FROM table_name;

Example:

    SELECT * FROM account;
    SELECT * FROM transaction;

## Update records
Let's update value of phone_number column for Anna.

Syntax:

    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    WHERE condition;

Example,

    UPDATE account
    SET phone_number = '8879956746'
    WHERE account_number='SB101';

View the updated rows,

    SELECT * FROM account;

## Excercise

Anna decide to close the account so we need to update the account_status for her now.

Query:

    UPDATE _________
    SET ________ = 'Closed'
    WHERE _________=_________;

View the updated rows

    SELECT * FROM account;

## Delete records from table

Let's delete all the closed accounts in the bank.

Syntax:

    DELETE FROM table_name WHERE condition;

Example:

    DELETE FROM account WHERE status='Closed';

We get an reference error, why?

## Using ON DELETE CASCADE

Let's drop our foreign key constraint on the transaction table.

Syntax:

    ALTER TABLE table_name
    DROP contraint_name;

Example:

    ALTER TABLE transaction
    DROP FOREIGN KEY;

Now, recreate the constraint with ON DELETE CASCADE

Syntax:

    ALTER TABLE transaction
    ADD CONSTRAINT foriegn_key FOREIGN KEY (account_number) REFERENCES account(account_number)
    ON DELETE CASCADE;

Now let's try deleting all closed accounts from account table.

    DELETE FROM account WHERE status='Closed';