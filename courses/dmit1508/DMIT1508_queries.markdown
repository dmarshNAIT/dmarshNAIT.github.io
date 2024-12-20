---
layout: page
title: Queries
permalink: /dmit1508/queries
parent: DMIT1508
nav_order: 5
---

## Queries

Queries are used to **retrieve data** from the database.

We can choose **which columns** we want to see, **which rows** we want, and which **aggregate** calculations we want.

Queries are written with a `SELECT` statement:
```sql
SELECT [ALL | DISTINCT] column_list 	
[INTO [new_table_name]]
[FROM table_name [, table_name2 [..., table_name16]] 
[INNER, LEFT OUTER, RIGHT OUTER JOIN]
[WHERE clause] 
[GROUP BY clause] 
[HAVING clause] 
[ORDER BY clause] 
[COMPUTE clause]
```

However, we won't always need all those pieces. Let's look at each clause individually.

### WHERE Clause

We can use a `WHERE` clause to return only certain records. Think of it as a filter:
```sql
SELECT 
    FirstName
,   LastName 
FROM STUDENT
WHERE City = 'Edmonton' 
    -- only return rows where the City column is exactly the value "Edmonton"
```

#### Search Criteria Operators
There are many useful keywords and symbols we can include in our `WHERE` clauses.

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

The `UNION` operation lets you **combine** the data retrieved by **multiple** `SELECT` statements. It's basically just gluing together the results of 2 or more queries, combining them into one output.
```sql
SELECT ...
UNION [ALL]
SELECT ...
```

### Aggregate Functions
Aggregate functions are functions that aggregate a bunch of individual values into a single value.

Generally, the syntax is: `aggregate_function_name([ ALL | DISTINCT] expression)`. For example:
- `AVG` returns the **average** of numeric values (ignoring any `NULL` values)
- `SUM` returns the **sum** of a column containing numeric values
- `MIN` and `MAX` return the **minimum** and **maximum** values from a column of numeric, date, or character values
- `COUNT` returns the number of **non-null values** OR the **number of records** that match the `WHERE` criteria
- `ALL` and `DISTINCT` can be in a query or with a `COUNT` function. `ALL` is the default and usually not explicitly declared.
  - When `DISTINCT` is used with the `COUNT` function it only counts the **unique** values.

The `GROUP BY` clause is used with **aggregate** functions to provide subtotals. For example:
  ```sql
  SELECT CourseID, AVG(Mark) AS AverageMark
  FROM Registration
  GROUP BY CourseID
  -- what this means:
  -- "for each course, select CourseID and the average mark"
  ```


### HAVING Clause

`HAVING` is like the `WHERE` clause, except it applies its criteria ***after*** `GROUP BY`. For example:
```sql
SELECT CourseID, AVG(Mark) as AverageMark
FROM Registration
WHERE AVG(Mark) > 80 
    -- this line will fail: I can't check the AVG(Mark) until after I group-by,
    -- i.e. I need to know the average mark per CourseID
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

The `ORDER BY` clause **sorts** one or more columns, in `ASC`ending or `DESC`ending order (`ASC` is the default).

```sql
SELECT FirstName, LastName
FROM Student
ORDER BY FirstName ASC, LastName DESC
```

### String Functions
Some useful functions include:
- `LEN(column | expression)` returns the **# of characters** in a string or expression
- `LEFT(column | expression, length)` returns `length` number of characters, starting at the left
- `RIGHT(column | expression, length)` returns `length` number of characters, starting at the right
- `SUBSTRING(column | expression, start, length)` returns a **subset** of characters from a string or expression
- `REVERSE(column | expression)` returns the string in **reverse** order
- `UPPER(column | expression)` returns the string in **UPPERCASE**
- `LOWER(column | expression)` returns the string in **lowercase**
- `LTRIM(column | expression)` trims any leading **whitespace**
- `RTRIM(column | expression)` trims any trailing **whitespace**

### Date Functions
- `GETDATE()` returns the **current system date**
- `DATEADD(units, num, date)` **adds** `num` `units` to `date` (n may be negative)
- `DATEDIFF(units, date1, date2)` returns the number of `units` from `date1` to `date2`
- `DATENAME(units, date)` returns **string representation** of the `units` of `date`
- `DATEPART(units, date)` returns **integer representation** of the `units` of `date`
  - `YEAR(date)` functions the same as `DATEPART(yy, date)`
  - `MONTH(date)` functions the same as `DATEPART(mm, date)`
  - `DAY(date)` functions the same as `DATEPART(dd, date)`

where `units` represents some unit of time:

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

How do we **connect** data in one table to its related record(s) in another?
```sql
SELECT Field1, Field2, ... 
FROM Table1
[INNER, LEFT OUTER, ...] JOIN Table2
	ON Table1.JoinField = Table2.JoinField
  -- the Join Field is generally the FK/PK that connects the tables, though technically we can JOIN by any field.
```

To see what that looks like with real fields/columns:
```sql
SELECT FirstName, LastName, Mark
FROM Student 
INNER JOIN Registration ON Student.StudentID = Registration.StudentID
-- studentID is the FK
```

#### Types of Joins
- `INNER JOIN` returns only records that exist in **both** tables
- `FULL OUTER JOIN` returns all records that exist in **either** table (if we're `JOIN`ing on our FK, which we always do in DMIT 1508, this type of `JOIN` isn't used)
- `Table1 LEFT JOIN Table2` returns all records in `Table1`, regardless of whether they exist in `Table2`
- `Table1 RIGHT JOIN Table2` returns all tables in `Table2`, regardless of whether they exist in `Table1`


#### Selecting from 3+ tables
We can add additional `JOIN` statements:
```sql
SELECT Field1, Field2, ... 
FROM Table1
INNER JOIN Table2
	ON Table1.JoinField = Table2.JoinField
INNER JOIN Table3
	ON Table.JoinField = Table3.JoinField 
        -- where "Table" is Table1 or Table2
INNER JOIN table4
	ON Table.JoinField = table4.JoinField 
        -- where "Table" is Table1, Table2, or Table3
...
```

### Subqueries
A subquery is a `SELECT` statement **inside** of another statement.

There are **nested** and correlated subqueries, and in this course we will focus on nested subqueries only, which are full and complete `SELECT` statements that could execute on their own.


They are especially useful for finding records that are in one table but not another: for example, staff who have never taught a course:
```sql
SELECT FirstName, LastName
FROM Staff
WHERE StaffID NOT IN (
    -- the list of Staff who HAVE taught:
    SELECT DISTINCT StaffID 
    FROM Offering
)

```

### ANY, SOME, and ALL operators
What if want something other than an exact match?
```sql
WHERE StudentID IN (SELECT StudentID ... )
-- IN lets us compare to a bunch of values at once, unlike = which only compares to a single value
```
`ANY` or `SOME` compares against any of the values:
```sql
WHERE Grade > SOME (SELECT Grade ... )
-- this will be TRUE if Grade (in the outer query) is greater than at least one Grade in the inner query
```
`ALL` compares against all of the values:
```sql
WHERE Grade > ALL (SELECT Grade ...)
-- this will only be TRUE if Grade (in the outer query) is greater than every single Grade in the inner query
```