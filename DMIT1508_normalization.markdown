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
1. The initial table must have a primary key identified, *after considering all candidates*.
    + When picking a PK, think of whether this will *always* be unique for every instance of you entity (in other words, for every row in your table).
    + If a single attribute doesn't work, you may need a combination of 2+ attributes.
1. Repeating groups are listed in parentheses. Repeating groups are attributes that can have multiple values within the view.
    + One way to think about repeating groups of attributes: are there attributes that, for a *single* instance of our entity, can have more than one value *at the same time*? e.g. a Customer entity can have more than one payment record on their account: payment ID would be a repeating group.

### Step 1: Apply the rules of 1NF
1.  A table must contain only *atomic* attributes.
    + That means, if we have any composite attributes, break 'em down! e.g. Name becomes FirstName and LastName, Address gets split up into StreetAddress, City, Province, PostalCode, etc.
1.  A table cannot contain any repeating groups of attributes.

    | If a repeating group of attributes exists:
    |---
    |1. Move the repeating group(s) of attributes to a new table.
    |2. Duplicate the PK of the original table and place in the new table as a FK.
    |3. Designate the cardinality of the relationship between the tables.
    |4. Designate a PK for the new table.
    
### Step 2: Apply the rules of 2NF

1. All non-key attributes in a table must *fully depend* on the entire primary key of the table.

    A violation can only occur in a table with a composite primary key.
    + That means: if we don't have a composite PK, we're done with 2NF!
    
    A non-key attribute is *fully dependent* on a PK attribute if: for each value of the key attribute there can be one value for the non-key attribute.
    
    An attribute that violates 2NF is referred to as a *partial dependency*.
    + In other words: are there any attributes that rely on just *part* of the PK, rather than the combination of all the attributes in it?
    
    | If a partial dependency exists:
    |---
    |1. Move the partially dependent attribute(s) to a new table.
    |2. Duplicate the part of the PK it's dependent on, and place in new table as a PK (it's now an FK in the original table). 
    |3. Designate the cardinality of the relationship between the tables.
    
### Step 3: Apply the rules of 3NF
    
1. A non-key attribute cannot be fully dependent on another non-key attribute.
    
   A non-key attribute that is fully dependent on another non-key attribute is termed a *transitive dependency*.
   + In other words: is there a non-key attribute that depends on another non-key attribute, instead of depending on the PK?
        
    |If a transitive dependency exists:
    |---
    |1. Move the transitively dependent attribute(s) to a new table.
    |2. Duplicate the non-key attribute it's dependent on, and place in new table as PK (it's now a FK in the original table).
    |3. Designate the cardinality of the relationship between the tables.