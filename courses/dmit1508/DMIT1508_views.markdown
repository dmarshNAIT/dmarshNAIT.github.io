---
layout: page
title: Views
permalink: /dmit1508/views
parent: DMIT1508
nav_order: 6
---

## Views

Views are basically virtual tables. They can:
- simplify data retrieval from complex queries
- hide the underlying table structure
- controll access to data for different users

Modifying records through a view must meet all rules/constraints on the table(s) the view is based on.

An `INSERT` or `UPDATE` from a view cannot affect more than one table in the view.
You cannot `DELETE` from a view that is based on more than one table.

If the `SELECT` statement contains `GROUP BY`, `DISTINCT`, `TOP`, or `UNION` you cannot modify data in that view.


### Syntax:
```sql
CREATE VIEW ViewName
AS
SELECT ...
```

#### Retrieving the definition:
```sql
SP_HELPTEXT ViewName
```

#### Altering existing views:
```sql
ALTER VIEW ViewName
AS
SELECT ...
```
#### Dropping existing views:

```sql
DROP VIEW ViewName
```
