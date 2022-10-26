# Session 4 - ACID properties
The ACID properties, provide a mechanism to ensure the correctness and consistency of a database.
- Automicity
- Consistency
- Isolation
- Durability

Let's try to break each properties to learn about them in detail.

We'll make a transaction, by sending amount from Anna's account to Bob's account.

Note total balance of both the accounts for future verification.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

Let's disable the autocommit feature for this experiment.

    SET autocommit = 0;


Let's check **automicity** by executing transaction with the following sub tasks,

**Step 1**: Deduct Rs.500 from Anna's account
  
    UPDATE account SET balance = balance - 500
    WHERE account_number='SB001';

**Step 2**: Create a debit transaction record for Anna

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Debit', '500', '2022-10-27 03:00:00', 'Success');

Let's say the database failed in the step 2. The money is deducted from Anna's account but not added to Bob's account.

Let's now check the **consistency** of our database.

Consistency in this transaction ensures that the sum of account balances before and after transaction remains same.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

Let's manually correct this problem by adding back the lost money and start the transaction again. 

    UPDATE account SET balance = balance + 500
    WHERE account_number='SB001';

Execute step 1 and step 2 again

**Step 1**: Deduct Rs.500 from Anna's account
  
    UPDATE account SET balance = balance - 500
    WHERE account_number='SB001';

**Step 2**: Create a debit transaction record for Anna

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Debit', '500', '2022-10-27 03:00:00', 'Success');

Now when we are in the middle of the transaction, Bob wants to add more money to his account say Rs.1000 (Terminal 2)

    UPDATE account SET balance = balance + 1000
    WHERE account_number='SB002';

Check Bob's account balance in both the terminals

    SELECT * from account
    WHERE account_number = 'SB002';

Let's continue the transaction.

**Step 3**: Add Rs.500 to Bob's account
 
    UPDATE account SET balance = balance + 500
    WHERE account_number='SB002';

**Step 4**: Create a credit transaction record for Bob

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB102', 'Credit', '500', '2022-10-27 03:00:00', 'Success');

Once the execution is complete, let's end the mysql transaction and store the data permanently.

    COMMIT;

Verify the account balances

    SELECT * FROM account
    WHERE account_number IN ('SB001','SB002');    

## Using MySQL Transactions
Let's look at our balance details of two accounts before we start tranfering the money.

    SELECT * FROM account
    WHERE account_number IN ('SB001','SB002');

Let's note the total balance of both the accounts for future verification.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

Now let's begin the mySQL transaction

    START TRANSACTION READ WRITE;

Open two mysql terminals in parallel and let's do a money transaction by executing following sub tasks,

**Step 1**: Deduct Rs.500 from Anna's account (Terminal 1)

    UPDATE account SET balance = balance - 500
    WHERE account_number='SB001';

**Step 2**: Create a debit transaction record for Anna (Terminal 1)
 
    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Debit', '500', '2022-10-27 03:00:00', 'Success');
 
Lets say our database crashed after deducting money from Anna. We can now do a rollback. (Terminal 1)
    
    ROLLBACK;

Check if your database now has old data i.e the money is not deducted from Anna's account. (Terminal 1)

    SELECT * FROM account
    WHERE account_number='SB001';
 
Let's now redo the steps 1 and 2 to start the transaction again after our database is up running.

**Step 1**: Deduct Rs.500 from Anna's account (Terminal 1)

    UPDATE account SET balance = balance - 500
    WHERE account_number='SB001';

**Step 2**: Create a debit transaction record for Anna (Terminal 1)
 
    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB101', 'Debit', '500', '2022-10-27 03:00:00', 'Success');

Let's say we reached step 2 and Bob tries to add money to his account. Let's try adding Rs.1000 to Bob's account in the other window (Terminal 2)

    UPDATE account SET balance = balance + 1000
    WHERE account_number='SB002';

Let's continue our pending transaction

**Step 3**: Add Rs.500 to Bob's account (Terminal 1)

    UPDATE account SET balance = balance + 500
    WHERE account_number='SB002';

**Step 4**: Create a credit transaction record for Bob (Terminal 1)

    INSERT INTO transaction (account_number, transaction_type, amount, transaction_date, status)
    VALUES ('SB102', 'Credit', '500', '2022-10-27 03:00:00', 'Success');

Once the transaction is complete, let's complete the transaction and store the data permanently.

    COMMIT;

After you commit the changes, the operation in Terminal 2 will complete its execution.

Now check the consistency of the database without considering the amount that Bob deposited in the middle of the transaction.

    SELECT SUM(balance) FROM account
    WHERE account_number IN ('SB001','SB002');

T verify the balances in both mysql instances, run the following command in both the terminals.

    SELECT * FROM account
    WHERE account_number IN ('SB001','SB002');

    SELECT * FROM transaction
    WHERE account_number IN ('SB001','SB002');



