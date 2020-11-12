---
layout: page
title: Stored Procedures
permalink: /dmit1508/storedprocedures
---

## Variables
Variables are used to hold values.

Before we use variables, we must **declare** them:
```sql
DECLARE     
    @VariableName datatype
,   @VariableName datatype
,   @VariableName datatype
...
```

We can assign values by hardcoding them:
```sql
DECLARE @FirstName varchar(40)
SET @FirstName = 'Dana' 
-- assigning a single variable from a literal is the only time I can use SET, otherwise I use SELECT
```

We can hardcode many at a time:
```sql
DECLARE @FirstName varchar(40)
    ,	@LastName varchar(40)
SELECT @FirstName = 'Dana'
    ,	@LastName = 'Marsh'
```

We can assign values from a query:
```sql
DECLARE @FirstName varchar(40)
SELECT @FirstName = StaffFirstName 
FROM Staff 
WHERE StaffID = 1
```

Or from a query that returns multiple columns/expressions:
```sql
DECLARE @FirstName varchar(40)
    ,	@LastName varchar(40)
SELECT @FirstName = StaffFirstName
    ,	@LastName = StaffLastName
FROM Staff 
WHERE StaffID = 1
```

## Flow Control

We can control the flow of SQL by using an `IF-ELSE` structure:
```sql
IF condition
	BEGIN
	statements -- these statements only execute if the condition is TRUE
	END
ELSE
	BEGIN
	statements -- these statements only execute if the condition is FALSE
	END
```

For example:
```sql
DECLARE @Total int
    , @Result varchar(10)
SET @Total = 100

IF @Total = 100
	BEGIN
	SET @Result = 'IS'
	END
ELSE
	BEGIN
	SET @Result = 'IS NOT'
	END

PRINT 'The total ' + @Result + ' 100.' -- PRINT is not how we should return messages to the user: it's primarily used for testing/debugging.
```
Another example using `EXISTS`:
```sql
IF EXISTS (SELECT * FROM Staff WHERE StaffID = 5)
	BEGIN
	PRINT 'There's a record for that StaffID'
	END
ELSE
	BEGIN
	PRINT 'There's NOT a record for that StaffID'
	END
```

## Batches & `GO`
A **batch** is a series of SQL statements.

`GO` is a **batch terminator**. It causes the batch to go to the server for execution.

It is recommended to use `GO` between batches to ensure they work properly: for example, if we're changing a `CONSTRAINT` and then running a related `INSERT`, I want to make sure my `CONSTRAINT`  is in place before `INSERT`ing, so I'll put them in separate batches.

## Stored Procedures
A stored procedure is a set of SQL statements.

### Syntax

- To create a new stored procedure:
    ```sql
    CREATE PROCEDURE procedure_name AS
    -- SQL statements go here
    RETURN
    ```
- To drop an existing stored procedure:
    ```sql
    DROP PROCEDURE procedure_name
    ```
- To change an existing stored procedure:
    ```sql
    ALTER PROCEDURE procedure_name
    -- SQL statements go here
    RETURN
    ```
- To run a stored procedure:
    ```sql
    EXEC procedure_name
    ```
    If the procedure has parameters, they are listed after, separated by commas:
    ```sql
    EXEC procedure_name param1, param2
    ```
- To display the definition of an existing stored procedure:
    ```sql
    EXEC sp_helptext procedure_name
    ```

### Parameters

We can pass in parameters to be used within our stored procedures:
```sql
CREATE PROCEDURE LookupStudent (@StudentID int) 
AS
-- SQL statements go here
RETURN
```
We can also initalize the values of the parameters:
```sql
CREATE PROCEDURE LookupStudent (@StudentID int = NULL) 
AS
-- SQL statements go here
RETURN
```

### Raising errors
To raise an error within our stored procedure, we use `RAISERROR`:
```sql
RAISERROR(msg_text, severity, state)
```

Example:
```sql
RAISERROR('Must provide required parameters', 16, 1)
```

### Global variables
- `@@error` returns the error count for the last statement executed. If the last statement did not error, it has a value of `0`.
- `@@identity` returns the last-inserted identity value.
- `@@rowcount` returns the number of rows affected by the last statement.

### Transactions
Transactions are SQL structures that ensure that a complete Logical Unit of Work is complete.

+ `BEGIN TRANSACTION` marks the beginning of the transaction
+ `COMMIT TRANSACTION` marks the end of the transaction, and makes the changes permanent.
+ `ROLLBACK TRANSACTION` marks the end of the transaction, and "undoes" the changes: we go back to the state we were in when the transaction began.

### Putting it all together...
Let's say we are creating an SP to register a student. Our stored procedure would:
+ Check to see if parameters are null. If so, `RAISERROR`.
+ Otherwise:
    + `BEGIN TRANSACTION `
    + `INSERT` into Grade
    + Check if the `INSERT` failed. If so, `ROLLBACK`.
    + Otherwise:
        + `UPDATE` Student.BalanceOwing
        + Check if the `UPDATE` failed. If so, `ROLLBACK`.
        + Otherwise, `COMMIT`.

