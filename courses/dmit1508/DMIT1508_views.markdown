---
layout: page
title: Views
permalink: /dmit1508/views
parent: DMIT1508
nav_order: 6
---

# Views

Views are basically virtual tables. They can:
- **simplify** data retrieval from complex queries: instead of `SELECT`ing from a complex query with many `JOIN` clauses, we can simply `SELECT` everything from a `VIEW`.
- **hide** the underlying table structure: we can `SELECT` just the columns we need, without revealing other data.
- **control access** to data for different users: users who require less access can be given access to a `VIEW` that shows more limited data.

Once a `VIEW` has been created, we can:
- `SELECT` from it just the same as `SELECT`ing data from a regular table
- Modify records, assuming we meet all constraints on the underlying tables.
    - An `INSERT` or `UPDATE` from a view cannot affect more than one table in the view.
    - You cannot `DELETE` from a view that is based on more than one table.
    - If the `SELECT` statement contains `GROUP BY`, `DISTINCT`, `TOP`, or `UNION` you cannot modify data in that view.

The syntax to `CREATE` a `VIEW` is as follows:
```sql
CREATE VIEW ViewName
AS
SELECT ...
```

To see the definition of a `VIEW` that already exists:
```sql
EXEC SP_HELPTEXT ViewName
```

To replace the definition of an existing `VIEW`:
```sql
ALTER VIEW ViewName
AS
SELECT ...
```
To remove an existing `VIEW`:

```sql
DROP VIEW ViewName
```
