---
layout: page
title: Queries
permalink: /dmit1508/queries
---

## Queries

Queries are used to retrieve data from the database.

We can choose which columns we want to see, which rows we want, and which aggregate calculations we want.

Queries are written with a `SELECT` statement:
```sql
SELECT [ALL | DISTINCT] column_list 	
[INTO [new_table_name]]
[FROM table_name [, table_name2 […, table_name16]] 
[INNER, LEFT OUTER, RIGHT OUTER JOIN]
[WHERE clause] 
[GROUP BY clause] 
[HAVING clause] 
[ORDER BY clause] 
[COMPUTE clause]
```

### WHERE Clause

We can use a `WHERE` clause to return only certain records:
```sql
SELECT 
    FirstName
, 	LastName 
FROM STUDENT
WHERE City = 'Edmonton' 
    -- only return rows where the City column contains the value "Edmonton"
```

#### Search Criteria Operators

Operator | Usage
--- | ---
`=` | looks for exact match
`<>` or `!=` | looks for something that does NOT match
`<` | less than
`<=` | less than or equal
`>` | greater than
`>=` | greater than or equal
`AND` | both expressions must be true
`OR` | either expression must be true
`BETWEEN` | returns all records between 2 values (inclusive)
`IN` | matches within a list of values
`NOT BETWEEN`, `NOT IN`, etc | the `NOT` operator negates other operations
`LIKE` | pattern matching

### UNION

The union operation lets you combine the data retrieved by multiple `SELECT` statements.
```sql
SELECT ...
UNION [ALL]
SELECT ...
```

### Aggregate Functions

Syntax: `aggregate_function_name([ ALL | DISTINCT] expression)`
- `AVG` returns the average of numeric values (ignoring any `NULL` values)
- `SUM` returns the sum of a column containing numeric values
- `MIN` and `MAX` return the minimum and maximum values from a column of numeric, date, or character values
- `COUNT` returns the number of non-null values OR the number of records that match the `WHERE` criteria
- `ALL` and `DISTINCT` can be in a query or with a `COUNT` function. `ALL` is the default and usually not explicitly declared.
  - When `DISTINCT` is used with the `COUNT` function it only counts the unique values.

The `GROUP BY` clause is used with aggregate functions to provide subtotals. For example:
```sql
SELECT CourseID, AVG(Mark) AS AverageMark
FROM Registration
GROUP BY CourseID
```

This can be read as: *for each course ID, return courseID and the average mark*

### HAVING Clause

`HAVING` is like the `WHERE` clause, except it applies its criteria *after* `GROUP BY`. For example:
```sql
SELECT CourseID, AVG(Mark) as AverageMark
FROM Registration
WHERE AVG(Mark) > 80 
    -- this line will fail: I can't check the AVG(Mark) until after I group-by.
GROUP BY CourseID
```

Instead:
```sql
SELECT CourseID, AVG(Mark) as AverageMark
FROM Registration
GROUP BY CourseID
HAVING AVG(Mark) > 80
```

### ORDER BY

The `ORDER BY` clause sorts one or more columns, in `ASC`ending or `DESC`ending order (`ASC` is the default).

```sql
SELECT FirstName, LastName
FROM Student
ORDER BY FirstName ASC, LastName DESC
```

### String Functions
Some useful functions include:
- `LEN(column | expression)` returns the length of a string or expression
- `LEFT(column | expression, length)` returns `length` number of characters, starting at the left
- `RIGHT(column | expression, length)` returns `length` number of characters, starting at the right
- `SUBSTRING(column | expression, start, length)` returns a subset of characters from a string or expression
- `REVERSE(column | expression)` returns the string in reverse order
- `UPPER(column | expression)` returns the string in UPPERCASE
- `LOWER(column | expression)` returns the string in lowercase
- `LTRIM(column | expression)` trims any leading whitespace
- `RTRIM(column | expression)` trims any trailing whitespace

### Date Functions
- `GETDATE()` returns the current system date
- `DATEADD(xx, n, date1)` adds `n` `xx` to `date1` (n may be negative)
- `DATEDIFF(xx, date1, date2)` returns the number of `xx` from `date1` to `date2`
- `DATENAME(xx, date1)` returns string representation of the `xx` of `date1`
- `DATEPART(xx, date1)` returns integer representation of the `xx` of `date1`
  - `YEAR(date1)` functions the same as `DATEPART(yy, date1)`
  - `MONTH(date1)` functions the same as `DATEPART(mm, date1)`
  - `DAY(date1)` functions the same as `DATEPART(dd, date1)`

where `xx` represents datepart:

Datepart | Abbreviation | Minimum | Maximum
--- | --- | --- | ---
Year | `yy` | 1753 | 9999
Quarter | `qq` | 1 | 4
Month | `mm` | 1 | 12
Week | `wk` | 1 | 53
Day of year | `dy` | 1 | 366
Weekday | `dw` | 1 (Sun) | 7 (Sat)
Day | `dd` | 1 | 31
Hour | `hh` | 0 | 23
Minute | `mi` | 0 | 59
Second | `ss` | 0 | 59
Millisecond | `ms` | 0 | 999

### JOINs

How do we connect data in one table to its related record(s) in another?
```sql
SELECT field1, field2, … 
FROM table1
[INNER, FULL OUTER, …] JOIN table2
	ON table1.joinfield = table2.joinfield
```

#### Types of Joins
- `INNER JOIN` returns only records that exist in both tables
- `FULL OUTER JOIN` returns all records that exist in either table
- `LEFT JOIN` returns all records in `table1`, regardless of whether they exist in `table2`
- `RIGHT JOIN` returns all tables in `table2`, regardless of whether they exist in `table1`

#### Selecting from 3+ tables
We can add additional `JOIN` statements:
```sql
SELECT field1, field2, … 
FROM table1
INNER JOIN table2
	ON table1.joinfield = table2.joinfield
INNER JOIN table3
	ON table.joinfield = table3.joinfield 
        -- where table is table1 or table2
INNER JOIN table4
	ON table.joinfield = table4.joinfield 
        -- where table is table1, table2, or table3
…
```

### Subqueries
A subquery is a `SELECT` statement inside of another statement.
It's a full and complete `SELECT` statement that could execute on its own.
There are nested and correlated subqueries, and in this course we will focus on nested subqueries only.

### ANY, SOME, and ALL operators
What if want something other than an exact match?
```sql
WHERE StudentID IN (SELECT StudentID … )
```
`ANY` or `SOME` compares against any of the values:
```sql
WHERE Grade > SOME (SELECT Grade … )
```
`ALL` compares against all of the values:
```sql
WHERE Grade > ALL (SELECT Grade …)
```
