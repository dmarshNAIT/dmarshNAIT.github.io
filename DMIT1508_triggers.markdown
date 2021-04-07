---
layout: page
title: Triggers
permalink: /dmit1508/triggers
---

## Triggers

Triggers are objects that are stored in the database, that execute when they are triggered **by a specific DML statement**.

For example, we could create a trigger that's associated with an `INSERT` operation on the `Staff` table. Every time we execute an `INSERT` on the `Staff` table, the code in that trigger will execute.

**Triggers cannot be explicitly executed, and cannot accept parameters.**

Triggers can help us to
- Enforce referential integrity across databases
    - e.g. Every time I `INSERT` or `UPDATE` a specific table, I can check the values against another table or database to make sure they are valid.
- Enforce business rules
    - e.g. something too complicated for a `CHECK` constraint like "cannot increase this field by more than 25% at a time".
- Automate an operation
    - e.g. automatically `UPDATE` associated records when a new record is added, like updating the total Job cost when a new Service is added to the Job.
- Create an audit trail
    - e.g. automatically log the changes when a value is changed, like the cost of an item.

For example: 
+ one trigger might check the value of an `INSERT`ed or `UPDATE`d column, and `ROLLBACK` if it's an invalid value (e.g. a CustomerID that doesn't exist in our database, or an OrderNumber from an order with a status of "cancelled").
+ a 2nd trigger may `ROLLBACK` if we attempt to `DELETE` from a certain table that contains important data.
+ a 3rd trigger may automatically `INSERT` records into an audit-log table that contain the "old" and "new" values when key fields are changed, like the budget for our project, or an employee's wage.
+ and so on. Anything we'd want to *automatically* do or check after a specific DML statement is a candidate for a trigger!

### When *exactly* do triggers execute?
Triggers happen at a **specific** point in a series of events, most of which that are happening *automatically* behind-the-scenes. Here's what the whole series looks like:
1. The process kicks off when a DML operation is executed: `INSERT`, `UPDATE`, or `DELETE`.
1. Next, the server will check if any `CONSTRAINT`s were violated by the DML statement. If so, an error is raised and the process ends without executing our trigger.
1. Then, the server will check for any issues with data types. If there are, an error is raised and the process ends without executing our trigger.
1. The server then `BEGIN`s a `TRANSACTION`, and creates 2 temporary tables (more on those below).
1. The DML operation occurs, which will mean changes *may* occur on the base table and the temporary tables.
1. Then, **the trigger will execute**. In that trigger, we may `ROLLBACK` the `TRANSACTION` that was started by the server, but will never `COMMIT TRANSACTION`. We may do other DML operations, or `RAISERROR`s.
    + Note: It's possible that we have multiple triggers on a single table. In this case, we have very little control over what order they occur in... we will generally ignore this within the scope of this class.
1. After our trigger finishes, if it didn't `ROLLBACK` the `TRANSACTION`, the server automatically `COMMIT`s the `TRANSACTION`.
1. Finally, the `inserted` and `deleted` tables are dropped.


### More about temporary tables...
Two temporary tables are created and used by the server when executing a DML operation.
- `deleted`: contains the "before" image of all rows affected
- `inserted`: contains the "after" image of all rows affected
- We'll use the term "base table" to refer to the table the trigger is associated with.

The contents of each temporary table depend on which DML statement the trigger is associated with:

| |  `deleted` table | `inserted` table | base table
--- | --- | --- | --- 
`INSERT` trigger | *empty* | new rows | new rows and previously existing rows
`DELETE` trigger | before image of deleted rows | *empty* | all rows that weren't deleted
`UPDATE` trigger |  before image of changed rows | after image of changed rows | after image of changed rows AND all other rows not affected by the operation

For example, if the `deleted` table is empty, that might mean that no records were affected, or it could mean we just executed an `INSERT` operation. We can use the contents of the temporary tables within our trigger logic, as needed.

### Logic to include in triggers
We'll almost always check `@@rowcount` at the start of our trigger, and if our trigger is trigged by an `UPDATE`, check `UPDATE(column_name)`, to make sure there were actually changes we need to check/audit/etc. If not, we branch around the logic in our trigger.

Triggers will execute:
- When the DML operation affects **zero** rows in the base table
- When the DML operation affects **one** row in the base table
- When the DML operation affects **many** rows in the base table

**The logic must work in all three conditions.**

### Syntax:
```sql
CREATE TRIGGER	TrigerName
	ON	TableName
	FOR [UPDATE][,] [INSERT][,] [DELETE]	
AS
	-- SQL statements
RETURN
```

Example:
- To create a trigger for the `INSERT` and `UPDATE` operations associated with the `Staff` table:
    ```sql
    CREATE TRIGGER TR_Staff_Insert_Update
        ON Staff 
        FOR INSERT, UPDATE	
    AS
        -- SQL statements go here
    RETURN
    ```

- To create a trigger for the `DELETE` operation associated with the `Student` table:
    ```sql
    CREATE TRIGGER TR_Student_Delete
        ON Student 
        FOR DELETE	
    AS
        -- SQL statements go here
    RETURN
    ```

### Dropping existing triggers:
```sql
DROP TRIGGER TriggerName
```
    
If you drop a table that has triggers associated with it, the triggers are dropped as well.

**Triggers cannot exist without the table it is associated with.**

### Changing existing triggers:
```sql
ALTER TRIGGER TriggerName
    ON TableName
    FOR [UPDATE][,] [INSERT][,] [DELETE]
AS
    -- SQL statements
RETURN
```

### To see a list of triggers in your db:
```sql
SELECT Name 
FROM SysObjects 
WHERE Type = 'TR'
```

### To see the source code of a trigger:
```sql
sp_helptext TriggerName
```