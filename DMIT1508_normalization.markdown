---
layout: page
title: Normalization
permalink: /dmit1508/normalization
---

## What is normalization?

The rules of normalization guide us to decide:
- the number of tables in our database
- the assignment of data items (attributes) to the various tables

We evaluate database design by how well it minimizes data redundancy, and the occurrence of anomalies.

### Step 0: Create initial table
1. The initial table must have a primary key identified, after considering all candidates.
1. Repeating groups are listed in parentheses. Repeating groups are attributes that hae multiple values within the view.

### Step 1: Apply the rules of 1NF
1.  A table must contain only *atomic* attributes.
1.  A table cannot contain any repeating groups of attributes.

    | If a repeating group of attributes exists:
    |---
    |1. Move the repeating group of attributes to a new table.
    |2. Duplicate the PK of the original table and place in the new table as a FK.
    |3. Designate the cardinality of the relationship between the tables.
    |4. Designate a PK for the new table.
    
### Step 2: Apply the rules of 2NF

1. All non-key attributes in a table must fully depend on the entire primary key of the table.

    A violation can only occur in a table with a composite primary key.
    
    A non-key attribute is *fully dependent* on a PK attribute if: for each value of the key attribute there can be one value for the non-key attribute.
    
    An attribute that violates 2NF is referred to as a *partial dependency*.
    
    | If a partial dependency exists:
    |---
    |1. Move the partially dependent attribute to a new table.
    |2. Duplicate the PK it's dependent on, and place in new table.
    |3. Designate the cardinality of the relationship between the tables.
    |4. Designate a PK for the new table.
    
### Step 3: Apply the rules of 3NF
    
1. A non-key attribute cannot be fully dependent on another non-key attribute.
    
   A non-key attribute that is fully dependent on another non-key attribute is termed a *transitive dependency*.
        
    |If a transitive dependency exists:
    |---
    |1. Move the transitively dependent attribute to a new table.
    |2. Duplicate the non-key attribute it's dependent on, and place in new table.
    |3. Designate the cardinality of the relationship between the tables.
    |4. Designate a PK for the new table.
