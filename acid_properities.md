# ACID properties
The ACID properties, provide a mechanism to ensure the correctness and consistency of a database.
- Automicity
- Consistency
- Isolation
- Durability

Let's try to break each properties to learn about them in detail.

Let's make a transaction, let's send amount from Anna's account to Bob's account.

Let's note total balance of both the accounts for future verification.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

Let's start database transaction before we begin transfering the money

    SET autocommit = 0;
    START TRANSACTION;

## Automicity

Transaction will have the following sub tasks,
1. Deduct Rs.500 from Anna's account
    ```
    UPDATE account SET balance = balance - 500
    WHERE account_number='SB001';
    ```
2. Create a debit transaction record for Anna
    ```
    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Debit', '500', '2022-10-27 03:00:00', 'Success');
    ```
    What happens if the database fails in step 2?

3. Add Rs.500 to Bob's account
    ```
    UPDATE account SET balance = balance + 500
    WHERE account_number='SB002';
    ```
4. Create a credit transaction record for Bob
    ```
    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB102', 'Credit', '500', '2022-10-27 03:00:00', 'Success');

## Consistency 
Let's now check the consistency of our database.

Consistency in this transaction ensures that the sum of account balances before and after transaction remains same.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

## Isolation

Let's say we are in the middle of the transaction, Bob tries to add more amount to his account say Rs.1000

    UPDATE account SET balance = balance + 1000
    WHERE account_number='SB002';

Bob will add Rs.1000 to his old balance i.e balance before transaction.

Check Bob's account balance

    SELECT balance FROM account
    WHERE account_number='SB001';

## Durability
Whatever updates we make, they should reflect on the database for other users of our database permanently.

    COMMIT;

## Proper transaction to solve the issue

- begin transaction
- modify table access
- rollback
- begin transaction
- modify table access
- commit


