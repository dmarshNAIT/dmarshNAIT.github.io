---
layout: page
title: DDL
permalink: /dmit1508/DDL
parent: DMIT1508
nav_order: 4
---

# Creating Tables

Data are stored in tables, which are 2-dimensional arrays where 
- each **column** records one **attribute**, and 
- each **row** records the **attributes for an instance**.

We use a `CREATE TABLE` statement to create a table object. The statement includes:
- the **name** of the **table**
- the **name** of each **column**
- the **data type** of each column
- whether `NULL` is an acceptable value for the column
- any other **constraints** that must hold true

Here's what it looks like:
```sql
CREATE TABLE TableName (
    Column1Name datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
  , Column2Name datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
  , Column3Name datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
    ...  
    [<table constraints>]
) 
```

A lot of that is optional, so here's what it looks like with just some of the required fields:

```sql
CREATE TABLE TableName (
    Column1Name datatype
  , Column2Name datatype
  , Column3Name datatype
    ...  
) 
```

## Verifying your table

After a table has been created, use the system stored procedure `SP_HELP` to list the table definition.

To run a stored procedure:
```sql
EXEC ProcedureName Parameter1, Parameter2 --as many params as we need, all comma-separated
```

In this case, we'd run:
```sql
EXEC SP_HELP Customers
```

## Deleting a table

To drop a table, the syntax is 
```sql
DROP TABLE TableName
```

For example, if I have a table called `Items`, I'd execute 
```sql
DROP TABLE Items
``` 
or 
```sql
DROP TABLE dbo.Items
-- dbo is the name of the schema the table is in.
-- think of a schema as kind of like a folder to organize your tables.
-- unless you do something special, dbo is the default schema.
```

### What if the table doesn't exist?

If I try to run `DROP TABLE` on a table that doesn't exist, I will get an error.

We can add in a check to say: *if the table exists, drop it.*
That way, if the table doesn't exist, we won't see an error.

An example of what this would look like for a table called `dbo.Activity` follows:

```sql
IF OBJECT_ID('dbo.Activity', 'U') IS NOT NULL 
-- if a table called dbo.Activity exists
  DROP TABLE dbo.Activity; 
```

Another way to write this:
```sql
DROP TABLE IF EXISTS Activity -- drop Activity table IF it exists
```

# Constraints

Constraints are used to:
1. Define **primary keys** (this is defined by the *primary key constraint*).
2. Define **relationships** (this is defined by the *foreign key constraint*).
3. Define **default values** (this is defined by the *default constraint*).
4. Define a domain of **valid values** (this is defined by the *check constraint*).
5. Ensure that all values in a column are **unique**.

Constraints can be set when **creating** a table (i.e. using the `CREATE TABLE` syntax) or can be **added** to an already-existing table using `ALTER TABLE`.

Each constraint must have a **unique name** within the database, and will use a prefix to identify its type:
- **PK_** for primary key constraints
- **FK_** for foreign key constraints
- **CK_** for check constraints
- **DF_** for default constraints

## Primary key constraints

In a normalized db design, all tables must have the PK constraint, and any column acting as a PK must be defined as `NOT NULL`.

The syntax of a PK constraint is 
```sql
CONSTRAINT ConstraintName PRIMARY KEY [CLUSTERED | NONCLUSTERED]
```

Example:
```sql
CREATE TABLE Student (
    StudentID   CHAR(9)     NOT NULL    CONSTRAINT PK_Student PRIMARY KEY CLUSTERED
,   LastName    VARCHAR(20) NOT NULL
,   FirstName   VARCHAR(15) NOT NULL
)
```

If the table has a **composite key**, the primary key constraint will be on the **table level** rather than the **column level**. Instead of putting it **beside** the column definition, it's **comma separated** from the columns like this:
```sql
CREATE TABLE Marks (
    StudentID   CHAR(9)     NOT NULL
,   CourseID    CHAR(6)     NOT NULL
,   Mark        SMALLINT    NULL
,   CONSTRAINT PK_Marks PRIMARY KEY CLUSTERED (StudentID, CourseID)
)
```

## Foreign key constraints

The FK constraint defines **relationships** between rows, and defines a **parent-child relationship** between tables. This affects:
1. **Dropping tables** (e.g. cannot drop a parent table before its child)
2. **Creating tables** (e.g. cannot create a child table before its parent)
3. **Inserting/updating/deleting** rows in tables (e.g. cannot insert an FK in a child table if there isn't an corresponding PK in its parent, can't delete a PK in a parent it has a corresponding child record)

Foreign keys must have the **same datatype** as its associated PK.

### Syntax:
```sql
CONSTRAINT constraint_name 
[FOREIGN KEY (Col1Name)[, ... ColName2] ]
REFERENCES TableName (Col1Name[, ... ColNam2] )
```

### Example with a column-level constraint:
```sql
CREATE TABLE RegionInCountry (
    CountryId	SMALLINT	NOT NULL    
        CONSTRAINT FK_RegionInCountryToCountry REFERENCES Country (CountryId)
,   RegionId	SMALLINT	NOT NULL
,   Name	VARCHAR(100) 	NOT NULL
,   CONSTRAINT PK_CountryId_RegionId PRIMARY KEY CLUSTERED (CountryId, RegionId)
)
```

### Example with a table-level constraint:
```sql
CREATE TABLE StoreInRegion (
    CountryId	SMALLINT	NOT NULL
,   RegionId	SMALLINT	NOT NULL
,   StoreId	SMALLINT	NOT NULL
,   Phone	VARCHAR(100) 	NOT NULL
,   CONSTRAINT PK_CountryId_RegionId_StoreId  
        PRIMARY KEY CLUSTERED (CountryId, RegionId, StoreId)
,   CONSTRAINT FK_StoreInRegionToRegionInCountry  
        FOREIGN KEY (CountryId, RegionId) 
	REFERENCES RegionInCountry (CountryId, RegionId)
)
```

## CHECK Constraints

The `CHECK` constraint enables you to specify what values are acceptable (i.e. specify a domain).

### Syntax:
```sql
CONSTRAINT ConstraintName CHECK (expression)
```
The expression:
- cannot contain a subquery
- must evaluate to `TRUE` or `FALSE`
- can be a compound boolean expression (e.g. using `AND` and/or `OR`)

### Examples:
1. The column `QuantitySold` must be positive:
	```sql
	CONSTRAINT CK_QuantitySold CHECK (QuantitySold > 0)
	```

2. The column `DateReceived` must be on or after the `DateOrdered`:
	```sql
	CONSTRAINT CK_DateReceived CHECK (DateReceived >= DateOrdered)
	```

3. The column `CourseMark` must be between 0 and 100, inclusive:
	```sql
	CONSTRAINT CK_CourseMark CHECK (CourseMark >= 0 AND CourseMark <= 100)
	```
	or
	```sql
	CONSTRAINT CK_CourseMark CHECK (CourseMark BETWEEN 0 and 100)
	```

4. The column `PostalCode` must follow the pattern A9A 9A9:
	```sql
	CONSTRAINT CK_PostalCode 
		CHECK (PostalCode LIKE '[A-Z][0-9][A-Z] [0-9][A-Z][0-9]')
	```

### The LIKE operator

The `LIKE` operator allows us to perform pattern matching on character or datetime data.

#### Syntax: 
```sql
ColumnnName LIKE 'pattern'
```
#### Example: 
```sql
LastName LIKE 'A%'
```
The `%` is a wildcard that means: any string of zero or more characters, so this example would match last names of any length as long as they begin with the letter A.

#### Other useful wildcards:

Symbol | meaning
--- | ---
`%` | any string of zero or more characters
`_` | any single character
`[]` | any single character within the specified range (`[a-f]`) or set (`[adr]`) of characters
`[^]` | any single character *not* within the specified range (`[^a-f]`) or set (`[^adr]`) of characters

## The DEFAULT constraint

The `DEFAULT` constraint lets you define a value that is assigned to a column when the user adds a row and doesn't supply a value.

A default constraint can be defined on any column *except*:
- A column with the timestamp data type
- A column with the identity property

### Syntax: 
```sql
CONSTRAINT DF_ConstraintName DEFAULT constant | function | NULL
```

### Examples:
1. Use 5.90 as default for `HourlyRate`:
	```sql
	CONSTRAINT DF_HourlyRate DEFAULT 5.90
	```
1. Use `NULL` as default for `PostalCode`:
	```sql
	CONSTRAINT DF_PostalCode DEFAULT NULL
	```
1. Use current date as default for `DateReceived`:
	```sql
	CONSTRAINT DF_DateRecevied DEFAULT GetDate()
	```



# Altering Tables
The `ALTER TABLE` statement is used to:
- **Add** a **column** to an existing table
- **Modify** the **datatype** or **null** status of an existing column
- **Modify** the seed and increment value of an existing **`identity`** property
- **Drop** an existing **column**
- **Add** a **constraint** to an existing column / table
- **Drop** an existing **constraint**
- **Disable** or **enable** an existing **constraint** (foreign key or check only: you cannot disable/enable a default or primary key constraint)
- **Disable** or **enable** an existing database **trigger**

> 💡 A note on adding **new columns** to an **existing table with data**: your new column **must** accept `NULL` or have a `default` constraint.
If the table is empty, you can add a column that is `NOT NULL`.

Here's the syntax for `ALTER TABLE`:
```sql
[ WITH { CHECK | NOCHECK } ]
{
[ { CHECK | NOCHECK } CONSTRAINT  ConstraintName ]
| [ ADD ColumnName column properties [column_constraints ]
| [ ADD TableConstraint ] 
| [ ( ALTER ColumnName
{ datatype {NULL|NOT NULL} | IDENTITY (seed, increment) 
| DROP DEFAULT | SET DEFAULT expression} ) ]
| [ DROP COLUMN ColumnName ]
| [ DROP CONSTRAINT ConstraintName ]
| [ {ENABLE | DISABLE } TRIGGER TriggerName ]
}
```
However, we will seldom have a statement that complex! Let's look at some simpler examples.

### Examples:
1. To **add** a **Semester** column to the **Marks** table:
	```sql
	ALTER TABLE Marks ADD Semester CHAR(1) NULL
	```

2. To **add** the **Semester** column to the **Marks** table and make it a **FK** referencing the **Schedule** table:
	```sql
	ALTER TABLE Marks
		ADD Semester	CHAR(1)	NULL
			CONSTRAINT FK_MarksToSchedule REFERENCES Schedule (Semester)
	```

3. To add a **FK** constraint to the **existing** CourseID column in the **Marks** table, making it reference the **Courses** table:
	```sql
	ALTER TABLE Marks
		ADD CONSTRAINT FK_CourseId 
		FOREIGN KEY (CourseId)  REFERENCES Courses (CourseId)
	```

4. To **add** a **check** constraint to the **existing** PhoneNo column in the **Student** table to ensure the phone number is in the format (nnn) nnn-nnnn:
	```sql
	ALTER TABLE Student
		ADD CONSTRAINT CK_PhoneNo
			CHECK ( PhoneNo LIKE '([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' )
	```

5. To add a **default constraint** to the existing OrderDate column in the Sales table to default to the current date:
	```sql
	ALTER TABLE Sales
		ADD	CONSTRAINT DF_OrderDate 
		DEFAULT GetDate() FOR OrderDate
	```

6. To **disable** the **default constraint** named CK_PhoneNo in the Student table:
	```sql
	ALTER TABLE Student
		NOCHECK CONSTRAINT CK_PhoneNo
	```

7. To **enable** the **default constraint** named CK_PhoneNo in the Student table:
	```sql
	ALTER TABLE Student
		CHECK CONSTRAINT CK_PhoneNo
	```

8. To **delete** the **default constraint** named DF_Mark from the Marks table:
	```sql
	ALTER TABLE Marks
		DROP CONSTRAINT DF_Mark
	```

# Indexes

An index is an object stored in the db that helps the DBMS look up data more quickly.

It's associated with 1 or more columns, in a specific table, that act as the key for the index.

For example:
- We could create an index for the `Employee` table, using the `EmployeeID` column as the key.
- Each row in the `Employee` table would have an entry in the index, with `EmployeeID` defining the order in which the entries are maintained in the index.
- Each entry in the index contains info (pointers) to where the associated row in the `Employee` table is located. The DBMS uses this info to speed up its retrieval of data.

There are 2 types of indices:
- **Clustered**:
  - A table has its rows physically stored in the same order as the order of the entries. (Therefore, one clustered index per table.)
  - The PK is often the key.
- **Non-clustered**:
  - Provides a method to use a 2nd-hand criteria for quickly finding/retrieving rows.
  - For example: we could define a non-clustered index for the `Employee` table that ses the `DepartmentNumber` as the key. The DBMS uses this to quickly retrieve the rows of employees who work for a specific department. 
  - We can have a max of 249 non-clustered indexes per table.

Indexes speed up data retrieval, but slow down operations to modify data in a table.
Consider a table with a clustered index and 3 non-clustered indices. 
- To insert a new row, the DBMS must add the row AND update four indices.
- To update a row: the DBMS deletes the old row, updates each index, adds a new row, and updates each index again. Updating the index might mean adding/deleting several items.
- That’s a lot of overhead!

Since we can only have one clustered index, how do we choose?
By default, the clustered index is created using the PK of the table. In many instances, this is the best choice. If another column is frequently used in the `ORDER BY` clause, or passed to the `COUNT`, `MIN`, or `MAX` aggregate functions, it’s also a good candidate.
Some designers create a non-clustered index for each FK. This increased overhead needs to be weighed against the improved performance of retrieving data.

Here's the syntax:
```sql
CREATE NONCLUSTERED INDEX IX_Name
ON TableName ( ColumnName )
```

The column name is the key for the index (one or more columns may act as the key). All indexes must have a unique name. We normally use the prefix `IX` when naming an index.

For example, to create a nonclustered index associated with the `Marks` table using `CourseID` (a FK referencing the `Course` table) as the index key:
```sql
CREATE NONCLUSTERED INDEX IX_CourseId
		ON Marks (CourseId)
```

And finally, to drop a nonclustered index:
```sql
DROP INDEX IX_CourseID ON Marks
```


