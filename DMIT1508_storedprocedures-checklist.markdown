---
layout: page
title: Stored Procedures Checklist
permalink: /dmit1508/storedprocedures-checklist
---

## Checklist
There are a few things we will always do when creating a stored procedure.

1. Initialize *all* parameters to `NULL`.
1. Check for **missing parameters** before doing any other logic.
1. Make sure to assign a value to variables before using them.
1. Check `@@error` after *every* DML statement.
1. If you have more than one DML statement that needs to run, you need a `TRANSACTION`. 
    + `BEGIN` the transaction before the 1st DML statement, `ROLLBACK` if any branch fails, and `COMMIT` if they all worked.


## Testing your SP
1.  Make sure you test **every** branch of your flow.
    +  Test with "good" parameters, missing parameters, AND some weird parameters.
    + The next section has examples of weird parameters that will break DML statements, or you could enter parameters of the wrong data type, or a nonsense value like a negative grade.
1. If you make *any* changes to your code, run all your tests again! Sometimes fixing one thing will break something else.
1.  Remember: testing isn't about proving it works. Testing is about trying to break your code! Then we fix the break, and our code is stronger and more thorough.

### Testing error branches
How can we effectively test the "error" branches of our code?
+ For `INSERT`s, try `INSERT`ing bad data: a FK that doesn't have a matching PK, or a duplicate PK, or a `NULL` in a required field, or something that violates a `CHECK` constraint.
+ For `UPDATE`s: you could `UPDATE` the data to a FK without a matching PK, or change the PK to a value that already exists, or change the PK of a record that has child records, or change a required field to `NULL`, or violate some `CHECK` constraint.
+ For `DELETE`s: you could try deleting a record that has a child record.


### Example pseudocode: creating a student 
```sql
IF (parameters are missing)
    RAISERROR -- branch 1
ELSE
	BEGIN TRANSACTION 
	INSERT into Registration ...
	IF (INSERT failed)
        RAISERROR
        ROLLBACK TRANSACTION -- branch 2
	ELSE
		UPDATE Student.BalanceOwing ...
		IF (UPDATE failed)
            RAISERROR
            ROLLBACK TRANSACTION -- branch 3
		ELSE
            COMMIT TRANSACTION --  branch 4
		
-- testing each brach: 
	-- 1. missing parameter(s)
	-- 2. failed insert
	-- 3. successful insert but failed update
	-- 4. successful insert & update
```	
