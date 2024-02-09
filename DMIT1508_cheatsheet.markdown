---
layout: page
title: DMIT1508
permalink: /dmit1508/cheatsheet
---

Here is a (hopefully) exhaustive list of all the SQL keywords and functions we've learned!

> **Tip**: Use Ctrl-F (or Command-F on a Mac) to search for specific words on this page.


## A
- `ALL` can be added to a `UNION` to include duplicates, or lets us compare to multiple values in a subquery.
- `ALTER PROCEDURE` replaces the previously saved query in a stored procedure.
- `ALTER TABLE` lets us make changes to a table that already exists, like adding an a new column or constraint. The [DDL page](./DDL) explains exactly what types of changes we can make.
- `ALTER TRIGGER` replaces the SQL in an existing trigger with new logic.
- `ALTER VIEW` lets us replace the query defining a view with a new query.
- `AND` is used between two boolean expressions, if we need **both** expressions to be true. You need a full and complete expression on both sides of `AND`.
- `ANY` compares against any of the values:
`WHERE Grade > ANY (SELECT Grade … )`
- `AVG()` is a function that returns the average of numeric values.

## B
- `BEGIN TRANSACTION` marks the beginning of a transaction. This is the point we come back to if the `TRANSACTION` is later `ROLL`ed `BACK`.
- `BETWEEN` will return records between 2 values, *including* those 2 values: e.g. `WHERE Mark BETWEEN 50 AND 100`

## C
- `COMMIT TRANSACTION` marks the end of the transaction, and makes everything that happened since `BEGIN TRANSACTION` permanent.
- `CONSTRAINT`s can be added to define the Primary Key, Foreign Key, any default values, or conditions a column has (e.g. what values are allowed, or what format the value must be in). More on constraints on the [DDL page](./DDL).
- `COUNT(*)` returns the number of rows in a query.
- `COUNT(ColumnName)` returns the number of non-null values in the specified column.
- `CREATE NONCLUSTERED INDEX` lets us create a new index, which speeds up data retrieval.
- `CREATE PROCEDURE` lets us create a set of SQL statements that is stored in the database, and can be run as needed. Check out the [Stored Procedures](./storedprocedures) page for more info.
- `CREATE TABLE` creates the structure for a new table in our database (see [DDL page](./DDL) for syntax)
    - `IDENTITY(seed, increment)` is what we add to each column that is a technical key (i.e. SQL will generate the value for us)
- `CREATE TRIGGER` creates a new trigger that will be executed by a specific kind of DML statement on a specific table. Learn more on the [triggers page](./triggers).
- `CREATE VIEW` lets us save a specific query, and `SELECT` from that view just like we select from a table. More on the [Views](./views) page.

## D
+ `DATEADD(xx, n, date1)` adds `n` `xx` to `date1` (`n` may be negative). See the [Queries](./queries) page for possible values for `xx`.
    + e.g. `DATEADD(yy, 5, HireDate)` returns the date 5 years after the `HireDate`.
+ `DATEDIFF(xx, date1, date2)` returns the number of `xx` from `date1` to `date2`.  See the [Queries](./queries) page for possible values for `xx`.
    + e.g. `DATEDIFF(dd, OrderDate, ShipDate)` returns the number of days between `OrderDate` and `ShipDate`.
+ `DATENAME(xx, date1)` returns a string representation of the `xx` of `date1`.  See the [Queries](./queries) page for possible values for `xx`.
    + e.g. `DATENAME(dw, '2020-01-01')` returns `Wednesday`.
+ `DATEPART(xx, date1)` returns integer representation of the `xx` of `date1`.  See the [Queries](./queries) page for possible values for `xx`.
    + e.g. `DATEPART(mm, '2020-03-01')` returns `3` because March is the 3rd month of the year.
    + `YEAR(date1)` functions the same as `DATEPART(yy, date1)`
       + e.g. `YEAR('2020-03-01')` returns `2020`. 
    + `MONTH(date1)` functions the same as `DATEPART(mm, date1)`
        + e.g. `MONTH('2020-03-01')` returns `3`. 
    + `DAY(date1)` functions the same as `DATEPART(dd, date1)`
        + e.g. `DAY('2020-03-01')` returns `1`.
- `DECLARE` lets us create a new variable: e.g. `DECLARE @FirstName VARCHAR(10), @LastName VARCHAR(20)`
- `DELETE` statements remove record(s) from a table. More on the [DML](./DML) page. e.g. `DELETE FROM Student WHERE GraduationStatus = 'Y'`
- `DISTINCT` can be added to a `SELECT` or `COUNT()` to only count **unique** rows or values.
- `DROP INDEX` deletes an index from the database.
- `DROP PROCEDURE` deletes a stored procedure.
- `DROP TABLE` deletes a table from the database: both its structure AND its contents.
    - If you `DROP` a table that has triggers associated with it, the triggers are dropped as well.
- `DROP TRIGGER` deletes a trigger from the database.
- `DROP VIEW` deletes a view from the database.

## E
- `EXEC ProcedureName ParameterName` is how we execute a stored procedure called *ProcedureName* with a parameter called *ParameterName*. Some SPs have no parameters, some have one, some have many: if we have multiple parameters, we separate them with commas like this: `EXEC ProcedureName Param1, Param2`.
    - e.g. `EXEC sp_help Customers` runs the `sp_help` on the `Customers` table.
    - e.g. `EXEC sp_helptext CustomerView` runs `sp_helptext` on the `CustomerView` view. It can also be used to get the definition of [triggers](./triggers)!

## G
- `GetDate()` returns the current datetime (i.e. today's date).
- `GO` is a batch terminator. It basically says, "Hey SQL, execute up to this point. Everything after this point is a separate batch."

## I
- `IF` is a conditional statement: the code within an `IF` block will only run if its condition evaluates to **true**. Optionally, an `IF` statement may have an `ELSE` block: that code will only run if the original condition evaluates to **false**.
- `IF EXISTS (...)` will run the query in parentheses, and will return **true** if at least one record is returned. This is helpful to check if there are existing records to `UPDATE` or `DELETE` before trying to `UPDATE` or `DELETE` them.
- `IN` lets us check for an exact match within a list of values. e.g. `WHERE StudentID IN (20001, 20002, 20004)`
- `INSERT` lets us add a new row (or rows) to a table. We can add using hardcoded values, the results of a subquery, or the results of a `SELECT` statement! More on the [DML](./DML) page. Some examples:
```sql
    INSERT INTO Staff (FirstName, LastName)
    VALUES ('Bob', 'Smith')
        , ('Bob', 'Jones') --inserting 2 rows in a single INSERT
```
```sql
    INSERT INTO Item (ItemID
        , ItemName
        , Cost
        , Description)
    VALUES (123  
        , 'Thingamabob'
        , SELECT AVG(Cost) FROM Item -- INSERTing a value from subquery!
        , NULL)
```
```sql
    INSERT INTO Student (FirstName, LastName)
    SELECT FirstName, LastName FROM Employee
    -- this is essentially copying values from one table to another
```

## J
- `JOIN` lets us join data from multiple tables.
    - `table1 INNER JOIN table2` returns only **records that exist in both tables**. 
        + If you're joining a parent to child, OR child to parent, you'll only get **records for parents that have child records**.
    - `table1 LEFT JOIN table2` returns **all records in table1**, regardless of whether they exist in table2.
        + If you're joining parent to child, you'll get **parents regardless of whether they have child records**.
        + If you're joining child to parent, you'll get only child records, so you **should use `INNER JOIN` instead**.
    - `table1 RIGHT JOIN table2` returns **all records in table2**, regardless of whether they exist in table1.
        + If you're joining parent to child, you'll get only child records, so you **should use `INNER JOIN` instead**.
        + If you're joining child to parent, you'll get **parents regardless of whether they have child records**.
    - `table1 FULL OUTER JOIN table2` returns all records that exist in either table.
        + If you're joining parent to child, you'll get parents regardless of whether they have child records, so you **should use `LEFT JOIN` instead**.
        + If you're joining child to parent, you'll get parents regardless of whether they have child records, so you **should use `RIGHT JOIN` instead**.
    + How to pick a `JOIN` type:

    |  | joining Parent to Child | joining Child to Parent
    | -----  |  ----- | -----
    | `INNER` | only records for parents that have child records | only records for parents that have child records
    | `LEFT`  |  parents regardless of whether they have child records | *use `INNER JOIN` instead*
    | `RIGHT`  |  *use `INNER JOIN` instead* | parents regardless of whether they have child records
    | `FULL OUTER`  |  *use `LEFT JOIN` instead* | *use `RIGHT JOIN` instead*


## L
- `LEN(column | expression)` returns the length of a string or expression. e.g. `LEN('hello')` has the value `5`.
- `LEFT(column | expression, length)` returns `length` number of characters, starting at the left. e.g. `LEFT('12345', 2)` returns the first `2` characters of `12345`: `12`.
- The `LIKE` operator lets us do pattern matching on a character. This is useful in a `CHECK` constraint or in a `WHERE` clause. Check out the [DDL page](./DDL) to see the wildcards we can use within our patterns.
- `LOWER(column | expression)` returns a string in all lowercase. e.g. `LOWER('Bob')` returns `bob`.
- `LTRIM(column | expression)` trims any leading whitespace from a string (e.g. spaces and tabs at the start of a string).

## M
- `MAX()` retuns the maximum value from a column of numeric, date, or character values.
- `MIN()` retuns the minimum value from a column of numeric, date, or character values.

## N
- `NOT` can be added to many other keywords: `NOT IN`, `NOT BETWEEN`, `NOT NULL`.
- `NULL` is the absence of a value. We can test whether or not a value is null by using `IS NULL` in our clause.
    + We do **not** use "`= NULL`". Why? `NULL` is **not** a value so it's impossible to be equal to it).

## O
- `OR` is used between two boolean expressions, if we need **either** to be true. Both sides of the expression need to be a full and complete boolean expression:
    e.g. "`WHERE Value = 5 OR Value = 10`" is correct. "`WHERE VALUE = 5 OR 10`" is incorrect, because "`10`" is not a boolean expression.

## P
- `PRINT` lets us print informational messages to the screen to help with testing and debugging.

## R
- `RAISERROR('error message', 16, 1)` is how we raise errors to a user. For example: if a parameter is missing, a DML statements fails, or an `UPDATE` or `DELETE` affects zero records. We should always include helpful error messages so the user knows what went wrong.
- `REVERSE(column | expression)` returns a string in reverse order: e.g. `REVERSE('123')` returns `321`.
- `RIGHT(column | expression, length)` returns `length` number of characters, starting at the right. e.g. `RIGHT('12345', 2)` returns the last `2` characters of the string: `45`.
- `ROLLBACK TRANSACTION` marks the end of a transaction, and "undoes" everything that happened since `BEGIN TRANSACTION`.
- `RTRIM(column | expression)` trims any trailing whitespace (e.g. spaces and tabs at the end of a string) from a string.

## S
- `SELECT` is how we start a query that retrieves data from our database. Details on all its parts are available on the [Queries](./queries) page.
    - It's also how we can assign literal values to multiple variables, or assign values to a variable FROM a `SELECT` statement. Check out the [Stored Procedures](./storedprocedures) page for more info.
    - We can also use it to get info from our databases, like a list of triggers: `SELECT Name FROM SysObjects WHERE Type = 'TR'`
- `SET` lets us assign a literal value to a variable: e.g. `SET @FirstName = 'Bob'`
- `SOME` compares against any of the values:
    + `WHERE Grade > SOME (SELECT Grade … )` 
    + It's the same as `ANY`.
- `SUBSTRING(column | expression, start, length)` returns a subset of characters from a string or expression. e.g. `SUBSTRING('abcdefg', 2, 3)` returns `3` characters, starting at position `2`: `bcd`.
- `SUM()` is a function that returns the sum of a column containing numeric values. e.g. `SUM(GST)` will take all the values in the `GST` column, add them together, and return the total.

## U
- `UNION` lets us combine the results of multiple SQL queries, as long as they have the same number of columns and similar data types. The columns are named according to the **first** query in the `UNION` (i.e. the names of the columns in subsequent queries doesn't appear in the results).
- `UPDATE` statements let us change the values of one or more columns in existing rows. More on the [DML](./DML) page.
    - e.g. `UPDATE Student
        SET FirstName = 'Bob', LastName = 'Smith'
        WHERE StudentID = 123`
- The `UPDATE()` function returns **true** if an `INSERT` or `UPDATE` was attempted on a specified column. These are used in triggers to let us branch around the logic if the column of interest wasn't updated.
- `UPPER(column | expression)` returns a string in UPPERCASE. e.g. `UPPER('Bob')` returns `BOB`.


## Other Operators
- `@@error` is a global variable that holds the error code for the most recently executed statement. If that statement did not error, it has a value of `0`. We'll check its value after every DML statement.
- `@@identity` returns the most recently used identity value.
- `@@rowcount` returns the number of rows affects by the most recent statement.
- `=` lets us look for an exact match (*is equal to*)
    - e.g. `FirstName = 'Bob'` evaluates to **true** only if FirsName is **exactly** "Bob". Any extra letters, punctuation, or spacing, or another word entirely, evaluates to **false**.
- `<>` or `!=` both mean *is not equal to*
    - e.g. `@@error <> 0` is how we check if `@@error` has a value other than `0`.
- `<` means *less than*
    - e.g. `Subtotal < 5` is **true** if the value of `Subtotal` is less than (not equal to) the value `5`.
- `<=` means *less than or equal to*
    - e.g. `Subtotal <= 5` is **true** if the value of `Subtotal` is less than, or exactly, the value `5`.
- `>` means *greater than*
    - e.g. `Total > 10` is **true** if the value of `Total` is greater than (not equal to) the value `10`.
- `>=` means *greater than or equal to*
    - e.g. `Total >= 10` is **true** if the value of `Total` is greater than, or exactly, the value `10`.