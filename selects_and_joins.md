# Session 3 - Select queries and MySQL joins

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

    SELECT account_number FROM account AS acc
    INNER JOIN transaction AS trans
    ON acc.account_number=trans.account_number
    WHERE trans.amount = MAX(tans.amount);

## Excercise

Select the total number of transactions that happend on the Anna's account.

    SELECT _________ AS 'Total Transactions' FROM ______
    WHERE _________='SB001';

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