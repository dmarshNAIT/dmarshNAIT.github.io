---
layout: page
title: DML
permalink: /dmit1508/DML
parent: DMIT1508
nav_order: 7
---
# DML

## INSERT

The `INSERT` statement adds 1+ rows to a table.

It can include **hard-coded values**, or can use **subqueries** to retrieve data from other tables.

There are 2 ways to `INSERT` data. Either we supply the exact number of rows directly:
```sql
INSERT INTO TableName (Column1, Column2, ...)
VALUES (Value1, Value2, ...))
-- Values could be DEFAULT, NULL, or an expression or subquery that returns a value
```

Or, we can `INSERT` data from another table, like a copy/paste:
```sql
INSERT INTO TableName (Column1, Column2, ...)
SELECT Column1, Column2, ...
FROM ...
```

If the statement supplies data that does not comply with constraints, or the data is incompatible with the data type of the column, the statement **fails**.

Example using hard-coded values:
```sql
INSERT INTO Staff (FirstName
    , LastName
    , DateHired
    , DateReleased
    , PositionID
    , LoginID)
VALUES ('Jason'
    , 'Teachalot'
    , 'Jan 1 2013'
    , NULL
    , 4
    , NULL)
```

Example using a **subquery**:
```sql
INSERT INTO Staff (FirstName
    , LastName
    , DateHired
    , DateReleased
    , PositionID
    , LoginID)
VALUES ('Jason'
    , 'Teachalot'
    , 'Jan 1 2013'
    , NULL
    , ( SELECT PositionID 
        FROM Staff 
        WHERE FirstName = 'Robert' and LastName = 'Smith')
    , NULL)
```

Examples using **default** values:
```sql
INSERT INTO Staff (FirstName
    , LastName
    , DateHired
    , DateReleased
    , PositionID
    , LoginID)
VALUES ('Jason'
    , 'Teachalot'
    , DEFAULT -- use default value for DateHired
    , NULL
    , 4
    , NULL) 
```
or
```sql
INSERT INTO Staff (FirstName
    , LastName
    , DateReleased
    , PositionID
    , LoginID) -- we've left out DateHired
VALUES ('Jason'
    , 'Teachalot'
    , NULL
    , 4
    , NULL)
```

## UPDATE
The `UPDATE` statement updates **existing rows** in the table. It can update **one or more** columns.

Data can be updated by providing new values for columns or by using subqueries to provide the data.
```sql
UPDATE	TableName
SET Column1 = expression[, Column2 = expression ... ]
[WHERE ... ]
```

Examples:
- Update the `Course` table and set `MaxStudents` to 3 for `CourseID` DMIT101:
    ```sql
    UPDATE Course
    SET MaxStudents = 3
    WHERE CourseID = 'DMIT101'
    ```

- Update the `Course` table and increase the cost of `DMIT108` by 10%:
    ```sql
    UPDATE Course
    SET Cost = Cost * 1.1
    WHERE CourseID = 'DMIT108'
    ```
- Update the `Course` table and set the `cost` of DMIT170 to be the same as the cost of DMIT254:
    ```sql
    UPDATE Course
    SET Cost = (	SELECT Cost 
                    FROM Course 
                    WHERE CourseID = 'DMIT254')
    WHERE CourseID = 'DMIT170'
    ```

- Update `CourseHours`, `MaxStudents`, and `Cost` columns for `CourseID` DMIT101:
    ```sql
    UPDATE Course
    SET 
        CourseHours = 4
    ,	MaxStudents = 5
    ,	Cost = 300
    WHERE CourseID = 'DMIT101'
    ```

## DELETE
The `DELETE` statement removes rows from a table.
```sql
DELETE FROM table_name
[WHERE ... ]
```

Examples:
- Delete all records in the `Club` table:
    ```sql
    DELETE FROM Club
    ```
    or
    ```sql
    DELETE Club
    ```
- Delete the record where the `ClubID` is ACM:
    ```sql
    DELETE FROM Club
    WHERE ClubID = 'ACM'
    ```

- Delete all `Payment` records that are less than the average payment amount.
    ```sql
    DELETE FROM Payment
    WHERE Amount < (SELECT AVG(Amount) FROM Payment)
    ```
