---
layout: page
title: DMIT1508
permalink: /dmit1508/cheatsheet
---

Here is a (hopefully) exhaustive list of all the SQL keywords and functions we've learned!

## A
- `ALL` can be added to a `UNION` to include duplicates, or lets us compare to multiple values in a subquery.
- `ALTER TABLE` lets us make changes to a table that already exists, like adding an a new column or constraint. The [DDL page](./DDL) explains exactly what types of changes we can make.
- `AND` is used between two boolean expressions, if we need **both** expressions to be true. You need a full and complete expression on both sides of `AND`.
- `ANY` compares against any of the values:
`WHERE Grade > ANY (SELECT Grade … )`
- `AVG()` is a function that returns the average of numeric values.

## B
- `BETWEEN` will return records between 2 values, *including* those 2 values: e.g. `WHERE Mark BETWEEN 50 AND 100`

## C
- `CONSTRAINT`s can be added to define the Primary Key, Foreign Key, any default values, or conditions a column has (e.g. what values are allowed, or what format the value must be in). More on constraints on the [DDL page](./DDL).
- `COUNT(*)` returns the number of rows in a query.
- `COUNT(ColumnName)` returns the number of non-null values in the specified column.
- `CREATE NONCLUSTERED INDEX` lets us create a new index, which speeds up data retrieval.
- `CREATE TABLE` creates the structure for a new table in our database (see [DDL page](./DDL) for syntax)
    - `IDENTITY(seed, increment)` is what we add to each column that is a technical key (i.e. SQL will generate the value for us)

## D
- `DISTINCT` can be added to a `SELECT` or `COUNT()` to only count **unique** rows or values.
- `DROP INDEX` deletes an index from the database.
- `DROP TABLE` deletes a table from the database: both its structure AND its contents. If you drop a table that has triggers associated with it, the triggers are dropped as well.

## E
- `EXEC ProcedureName ParameterName` is how we execute a stored procedure called *ProcedureName* with a parameter called ParameterName. Some SPs have no parameters, some have one, some have many.
    - `EXEC sp_help Customers` runs the `sp_help` on the `Customers` table.

## G
- `GetDate()` returns the current datetime (i.e. today's date).

## I
- `IN` lets us check for an exact match within a list of values. e.g. `WHERE StudentID IN (20001, 20002, 20004)`

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
    | `LEFT`  |  parents regardless of whether they have child records | use `INNER JOIN` instead
    | `RIGHT`  |  use `INNER JOIN` instead | parents regardless of whether they have child records
    | `FULL OUTER`  |  use `LEFT JOIN` instead | use `RIGHT JOIN` instead


## L
- The `LIKE` operator lets us do pattern matching on a character. This is useful in a `CHECK` constraint or in a `WHERE` clause. Check out the [DDL page](./DDL) to see the wildcards we can use within our patterns.

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


## S
- `SELECT` is how we start a query that retrieves data from our database. Details on all its parts are available on the [Queries](./queries) page.
- `SOME` compares against any of the values:
    + `WHERE Grade > SOME (SELECT Grade … )` 
    + It's the same as `ANY`.
- `SUM()` is a function that returns the sum of a column containing numeric values.

## U
- `UNION` lets us combine the results of multiple SQL queries, as long as they have the same number of columns and similar data types. The columns are named according to the **first** query in the `UNION` (i.e. the names of the columns in subsequent queries doesn't appear in the results).

## Other Operators
- `=` lets us look for an exact match (*is equal to*)
- `<>` or `!=` both mean *is not equal to*
- `<` means *less than*
- `<=` means *less than or equal to*
- `>` means *greater than*
- `>=` means *greater than or equal to*

## String functions:
+ `LEN(column | expression) `
+ `LEFT(column | expression, length) `
+ `RIGHT(column | expression, length) `
+ `SUBSTRING(column | expression, start, length) `
+ `REVERSE(column | expression) `
+ `UPPER(column | expression) `
+ `LOWER(column | expression) `
+ `LTRIM(column | expression) `
+ `RTRIM(column | expression)` 
+ Check out the [Queries](./queries) page for definitions of each.

## Date Functions
+ `GETDATE()` returns the system date
+ `DATEADD(xx, n, date1)` adds `n` `xx` to `date1` (`n` may be negative)
+ `DATEDIFF(xx, date1, date2)` returns the number of `xx` from `date1` to `date2`
+ `DATENAME(xx, date1)` returns string representation of the `xx` of `date1`
+ `DATEPART(xx, date1)` returns integer representation of the `xx` of `date1`
    + `YEAR(date1)` functions the same as `DATEPART(yy, date1)`
    + `MONTH(date1)` functions the same as `DATEPART(mm, date1)`
    + `DAY(date1)` functions the same as `DATEPART(dd, date1)`

## To be added:
+ Lesson 26 - Views & DML
    + In the meantime, check out the [Views](./views) and [DML](./DML) pages!
+ Lesson 28 - Stored Procedures
+ Lesson 37 - Triggers