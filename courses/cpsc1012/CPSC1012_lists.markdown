---
layout: page
title: Lists
permalink: /cpsc1012/lists
parent: CPSC1012
nav_order: 11
---
# Lists
Arrays are a type of **collection** class. All its elements are the **same data type**, and they are a **set size** (i.e. we can't change our mind later and increase the size of our array).

Another type of collection class is a `List`, which will **dynamically** increase its size as required. 

## (Some) Useful List Properties & Methods:
- `Capacity`: lets us get or set the number of elements our `List` can contain.
- `Count`: gets the number of elements currently in the `List`.
- `Add()`: public method to **add** objects to the `List`.
- `Clear()`: **Removes** all elements from the `List`.
- `Contains()`: Determines whether an element is in the `List`.
- `CopyTo()`: public method that **copies** a `List` to a 1-D array.
- `Insert()`: **Inserts** an element into a `List`.
- `Sort()`
- and the `List` goes on...

## Creating Lists

This creates a list called dogList that holds references to Dogs:
```csharp
List<Dog> dogList = new List<Dog>();
```

Here, we create a list of integers, and then add and modify records:
```csharp
List<int> marks= new List<int>();
marks.Add(50);
marks.Add(75);
marks.Add(100);
marks[1] += 5;
marks.RemoveAt(1);
```