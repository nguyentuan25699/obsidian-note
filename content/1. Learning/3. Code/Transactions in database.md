## 1. Introduction
- Database systems are normally being accessed by many users or processes at the same time (both queries and modifications).
- Unlike operation systems, which support interaction of processes, a DMBS needs to keep processes from trouble some interactions.
___

## 2. ACID in database
- ACID is an acronym that stands for :
	- Atomicity : Either the whole process is done or none is
	- Consistency: Database constraints are preserved
	- Isolation : It appears to the user as if only one process executes at a time
	- Durability : Effects of a process do not get lost if the system crashes. 
- Together, these ACID properties ensure that a set of database operations (grouped together in a transaction) leave the database in a valid state even in the event of unexpected errors.
___

## 3. Transactions
### Transactions in SQL
- A database transaction is a sequence of multiple operations performed on a database, and all served as a single logical unit of work — taking place wholly or not at all
- Every transaction executed requires the ACID attribute to be guaranteed

Example :
```sql
SELECT * FROM Users
SELECT * FROM Blogs Where user_id = 1
```

```sql
INSERT INTO Users (id,name) VALUES (1, ‘Peter');
```

- Register account A
- Register account B
- A transfers money to B's bank account
___

## 4. How transactions works?
### Transaction States
- **Active**: It is the first state during the execution of a transaction.
- **Partially committed**: A change has been executed in this state, but the database has not yet committed the change on disk.
- **Committed**: In this state, all the transaction updates are permanently stored in the database
- **Failed**: If a transaction fails or has been aborted in the active state or partially committed state, it enters into a failed state.
- **Terminated**: This is the last and final transaction state after a committed or aborted state.

![[Pasted image 20260707221314.png]]
___

- The SQL statement `commit` causes a transaction to complete. It’s database modifications are now permanent in the database.
- The SQL statement `rollback` also causes the transaction to end but by `aborting`, no effects on the database.
![[Pasted image 20260707221423.png]]
___

## 5. Advantages and Disadvantages
![[Pasted image 20260707221506.png]]
___

## 6. Transaction Control
The following commands are used to control transactions.
- COMMIT − to save the changes.
- ROLLBACK − to roll back the changes : `ROLLBACK TO SAVEPOINT_NAME`;
- SAVEPOINT − creates points within the groups of transactions in which to `ROLLBACK`. 
	`SAVEPOINT SAVEPOINT_NAME; `
	`RELEASE SAVEPOINT TEN_SAVEPOINT;`
- SET TRANSACTION − Places a name on a transaction.
	`SET TRANSACTION [ READ WRITE | READ ONLY ]; `
- BEGIN TRANSACTION - Begin a transaction : `BEGIN TRANSACTION || BEGIN WORK`
- END TRANSACTION - End a transaction : `END TRANSACTION || END WORK`
