---
layout: page
title: DMIT1508
permalink: /dmit1508/glossary
---

## A
- **Attributes** are pieces of data that describe an entity. For example, a *Customer* entity may have the following attributes: customer number, last name, first name, address, and phone number.

    Attributes are either *atomic* or *composite*. Composite attributes are attributes that could be sub-divided. For example, customer name is composite, but customer first name and customer last name would be atomic.
    
    *Derived* attributes are those that are not actually stored in the database, but could be calculated, like Order Amount could be derived by multiplying Quantity and Price.

## D
- Attributes have a **data type** which describes the kind of data it can hold (e.g. numeric).

- Attributes also have a **domain** which are the legitimate values it can hold (e.g. greater than zero).

## E
- An **entity** is a person, place, thing, or concept. Also called an entity class or entity type.

    *Associative entities* are entities which connect two other entities who have a many:many relationship, and they contain the primary key attributes of both the other entities.

## F
- A **foreign key** is how we define relationships between entities. A foreign key is the primary key of another entity (the parent) that appears as an attribute of this entity (the child).

## P
- **Primary keys** are unique identifiers for each instance of an entity. Sometimes there isn't a naturally occuring identifier, so we make one up. These are called *technical keys*, and are created in SQL using `IDENTITY`.

    A combination of 2 or more attributes acting as the primary key is called a *concatenated key* or *composite key*.
