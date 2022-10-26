# Session 3 - Select queries and MySQL joins

## Data for SELECT opertaions

Run the following insert queries to add data to tables for the following experiments.

Account Table:

    INSERT INTO account (account_number, name, address, account_status, balance, phone_number)
    VALUES ('SB101', 'Anna', 'M.G Road, Bangalore', 2000 'Active', '9113456578');
    VALUES ('SB102', 'Bob', 'Alevoor, Manipal', 'Active', 1000, '7144556578');
    VALUES ('SB103', 'Alice', 'Peenya, Bangalore', 'Active', 200, '8333456578');
    VALUES ('SB103', 'June', 'Kavoor, Mangalore', 'Active', 150, '8333456578');

Transaction Table:

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Credit', '2000', '2022-09-18 03:00:00', 'Success');
    VALUES ('SB101', 'Credit', '500', '2022-09-27 03:00:00', 'Success');
    VALUES ('SB101', 'Debit', '500', '2022-10-24 03:00:00', 'Success');
    VALUES ('SB101', 'Debit', '100', '2022-10-20 03:00:00', 'Success');
    VALUES ('SB102', 'Credit', '2000', '2022-09-22 03:00:00', 'Success');
    VALUES ('SB102', 'Debit', '1400', '2022-10-21 03:00:00', 'Success');
    VALUES ('SB102', 'Credit', '400', '2022-10-26 03:00:00', 'Success');
    VALUES ('SB103', 'Credit', '4200', '2022-06-27 03:00:00', 'Success');
    VALUES ('SB103', 'Debit', '4000', '2022-17-24 03:00:00', 'Success');
    VALUES ('SB103', 'Credit', '7000', '2022-09-08 03:00:00', 'Success');
    VALUES ('SB103', 'Debit', '6850', '2022-10-25 03:00:00', 'Success');



## Simple SELECTs

Let's select all transactions of one particular account 'SB001'

    SELECT * FROM transaction 
    WHERE account_number='SB001';

Select all account_number, name and phone_number of customers who's balance is below minimum balance of Rs.500

    SELECT account_number, name, phone_number FROM account 
    WHERE balance < 500;

Now let's view all the transactions happend on the account 'SB001' in last one week.

    SELECT * FROM transaction 
    WHERE transaction_date 
    BETWEEN '2022-10-20 00:00:00' AND '2022-10-27 00:00:00';

## SELECTs with MySQL functions
Let's find total number of accounts in the bank.

    SELECT COUNT(*) AS 'Total Accounts' FROM account;

Let's find out total amount in the bank i.e the sum of all account balances.

    SELECT SUM(balance) AS 'Total Balance' FROM account;

Select all account numbers who had maximum transactions in last week

    SELECT DISTINCT account_number FROM transaction
    WHERE amount = MAX(amount);

## Excercise

Select the total number of transactions that happend on the Anna's account.

    SELECT _________ AS 'Total Transactions' FROM ______
    WHERE _________='SB001';

## Normalization

It is the process of eliminating data redundency and enhancing data integrity in the database tables.

| | account_number | customer_name | balance | account_status | transaction_id | transaction_type | transaction_amount | transaction_status |
| --- |---|---|---|-----|---|---|---|---|
|1| SB1001 | Anna S | 500 | Active | T1 | Debit | 200 | Success |
|2| SB1001 | Anna S | 350 | Active | T2 | Debit | 150 | Success |
|3| SB1001 | Anna D | 3500 | Active | T3 | Credit | 3000 | Success |
|4| SB1002 | Bob | 5000 | Active | T4 | Debit | 200 | Success |

The data here is redundant and lacks consistency.

- Row number 3 has a typo in the customer_name field, which makes the table inconsistent i.e if we retrieve customer_name based on the account number we get two values 'Anna S' and 'Anna D'.
- All the account related information in the table is redundent i.e account information is repeated for each transaction made by Anna.

Therefore we normalize the data and split it into two tables 'Account' and 'Transaction'.

| | account_number | customer_name | balance | account_status |
| --- |---|---|---|-----|
|1| SB1001 | Anna S | 500 | Active |
|2| SB1001 | Anna S | 350 | Active |
|3| SB1001 | Anna D | 3500 | Active |
|4| SB1002 | Bob | 5000 | Active |

| | account_number | transaction_id | transaction_type | transaction_amount | transaction_status |
| --- |---|---|---|-----|---|
|1| SB1001 | T1 | Debit | 200 | Success |
|2| SB1001 | T2 | Debit | 150 | Success |
|3| SB1001 | T3 | Credit | 3000 | Success |
|4| SB1002 | T4 | Debit | 200 | Success |

If we normalize the tables like this and just add a common field as a reference, we avoid both consistency and redundency problem.

To get the data from these related tables we can either make use of table JOINS or subqueries. As table JOINS are more cost effective they are widely used.
## SELECTs with joins

Let's get the account details of all the failed transactions.

    SELECT acc.* FROM account AS acc
    INNER JOIN transaction AS trans
    ON acc.account_number=trans.account_number
    WHERE trans.status='Failed';

Let's get all Debit transaction details for Anna's account.

    SELECT tans.* FROM account AS acc
    INNER JOIN transaction AS trans
    ON acc.account_number=trans.account_number
    WHERE trans.transaction_type='Debit';

## Excercise
Select account number and name of customers who made transactions above Rs.1000.

    SELECT ___________, _______ FROM ________ AS acc
    ___________ transaction AS ________
    ON __________=___________
    WHERE ____________ > 1000;