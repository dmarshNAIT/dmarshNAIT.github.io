---
layout: page
title: Stored Procedures
permalink: /dmit1508/storedprocedures
---

## Variables

Before we use variables, we must declare them:
```sql
DECLARE 
    @variablename datatype
,	@variablename datatype
,	@variablename datatype
...
```

We can assign values by hardcoding them:
```sql
DECLARE @firstname varchar(40)
SET @firstname = 'Dana'
```

We can hardcode many at a time:
```sql
DECLARE @firstname varchar(40)
    ,	@lastname varchar(40)
SELECT @firstname = 'Dana'
    ,	@lastname = 'Marsh'
```

We can assign values from a query:
```sql
DECLARE @firstname varchar(40)
SELECT @firstname = StaffFirstName 
FROM Staff 
WHERE StaffID = 1
```

Or from a query that returns multiple columns/expressions:
```sql
DECLARE @firstname varchar(40)
    ,	@lastname varchar(40)
SELECT @firstname = StaffFirstName
	,	@lastname = StaffLastName
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

## Stored Procedures

### Syntax

- To create a new stored procedure:
    ```sql
    CREATE PROCEDURE procedure_name AS
    SQL statements
    RETURN
    ```
- To drop an existing stored procedure:
    ```sql
    DROP PROCEDURE procedure_name
    ```
- To change an existing stored procedure:
    ```sql
    ALTER PROCEDURE procedure_name
    SQL statements
    RETURN
    ```
- To run a stored procedure:
    ```sql
    EXEC procedure_name
    ```
- To display the definition of an existing stored procedure:
    ```sql
    EXEC sp_helptext procedure_name
    ```

### Parameters

We can pass in parameters to be used within our stored procedures:
```sql
CREATE PROCEDURE LookupStudent 
	(@StudentID int) AS
SQL statements
RETURN
```
We can also initalize the values of the parameters:
```sql
CREATE PROCEDURE LookupStudent 
	(@StudentID int = NULL) AS
SQL statements
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