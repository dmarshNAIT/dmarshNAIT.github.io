---
layout: page
title: DDL
permalink: /dmit1508/DDL
---

## Tables

Data are stored in tables, which are 2D arrays where each column records one attribute and each row records the attributes for an instance.

We use a `CREATE TABLE` statement to create a table object, which includes:
- the name of the table
- the name of each column
- the data type of each column
- whether `NULL` is an acceptable value for the column
- any other constraints that must hold true

```sql
CREATE TABLE tablename (
    column1 datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
  , column2 datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
  , column3 datatype [IDENTITY [(seed, increment)] | [NULL | NOT NULL] [<column constraints>]
    ...  
    [<table constraints>]
) 
```

A lot of that is optional, so here's what it looks like with just some of the required fields:

```sql
CREATE TABLE tablename (
    column1 datatype
  , column2 datatype
  , column3 datatype
    ...  
) 
```

### Verifying your table

After a table has been created, use the system stored procedure `SP_HELP` to list the table definition.

To run a stored procedure:
`EXEC procedurename [parameter1 [, parameter2 ... ]]`

In this case, we'd run:
`EXEC SP_HELP Customers`
