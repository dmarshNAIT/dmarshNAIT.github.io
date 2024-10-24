---
layout: page
title: Lists
permalink: /cpsc1012/lists
parent: CPSC1012
nav_order: 11
---
# Lists
A `List` is another type of collection class. In contrast with an [array](./arrays), a `List` will **dynamically** increase its size as required. 

## (Some) Useful List Properties & Methods:
There are [many](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-8.0) properties and methods available in the `List` class: here are a few handy ones.
### Properties
- `Capacity`: lets us get or set the number of elements our `List` **can** contain.
- `Count`: gets the **number of elements** currently in the `List`.
- We can also access elements using square brackets, just like with an `Array`.

### Methods
- `Add()`: public method to **add** objects to the `List`.
- `Clear()`: **Removes** all elements from the `List`.
- `Contains()`: Determines whether an element is in the `List`.
- `CopyTo()`: public method that **copies** a `List` to a 1-D array.
- `Insert()`: **Inserts** an element into a `List`.
- `Sort()`: sorts elements using the default comparer.


## Creating Lists

This creates a list called `dogList` that holds references to `Dog` objects:
```csharp
List<Dog> dogList = new List<Dog>();
```

We can even make a `List` containing elements of a built-in type. Here's what that looks like, including adding, modifying, and removing elements:
```csharp
List<int> marks= new List<int>();

marks.Add(50);      // add a new element with the value 50
marks.Add(75);      // add a new element with the value 75
marks.Add(100);     // add a new element with the value 100
marks[1] += 5;      // increase the value of the element at index 1
marks.RemoveAt(1);  // remove the element at index 1
```