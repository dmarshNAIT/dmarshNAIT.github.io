---
layout: page
title: Triggers
permalink: /dmit1508/triggers
---

## Triggers

Triggers are objects that are stored in the database, that execute when they are triggered by a specific DML statement.

For example, we could create a trigger that's associated with an `INSERT` operation on the `Staff` table. Every time we execute an `INSERT` on the `Staff` table, the code in that trigger will execute.

**Triggers cannot be explicitly executed, and cannot accept parameters.**

Triggers can help us to
- Enforce referential integrity across databases
- Enforce business rules
- Automate an operation
- Create an audit trail

### Temporary tables
Two temporary tables are created and used by the server when executing a DML operation.
- `Deleted`: contains the before image of all rows affected
- `Inserted`: contains the after image of all rows affected
- We'll use the term "base table" to refer to the table the trigger is associated with.

The contents of each temporary table depend on which DML statement the trigger is associated with:

| |  `deleted` table | `inserted` table | base table
--- | --- | --- | --- 
`INSERT` trigger | empty | new rows | new rows and previously existing rows
`DELETE` trigger | before image of deleted rows | empty | all rows that weren't deleted
`UPDATE` trigger |  before image of changed rows | after image of changed rows | after image of changed rows AND all other rows not affected by the operation

Triggers will execute:
- When the DML operation affects zero rows in the base table
- When the DML operation affects one row in the base table
- When the DML operation affects many rows in the base table

**The logic must work in all three conditions.**

### Syntax:
```sql
CREATE TRIGGER	trigger_name
	ON	table_name
	FOR [UPDATE][,] [INSERT][,] [DELETE]	AS
	SQL statements
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
DROP TRIGGER trigger_name
```
    
If you drop a table that has triggers associated with it, the triggers are dropped as well.

**Triggers cannot exist without the table it is associated with.**

### Changing existing triggers:
```sql
ALTER TRIGGER trigger_name
    ON table_name
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
sp_helptext trigger_name
```