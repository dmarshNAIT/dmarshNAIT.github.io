---
layout: page
title: CPSC1012
permalink: /cpsc1012/arrays
---

CPSC1012 - Programming Fundamentals

<h1>Arrays</h1>

<p>
When we create an array, we identify the data type, and set the size:
```csharp
int[] myInts = new int[5];
```
This means all elements in this array will be of type `int`, and there are 5 elements.

We can also load data into the array manually when we create it:
```csharp
string[] dayOfWeek = new string[7] { "SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT" };
```

Alternatively, we can drop the `new string[7]` part because:
```csharp
string[] dayOfWeek = { "SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT" }; 
```

Once an array exists, we can view or modify each element by using square brackets and its index:
```csharp
int[] someNumbers = new int[10];
someNumbers[0] = 5;
```
I just set the 0th element of the array to the value `5`.

Because we know exactly how many elements are in the array, I could loop through each element and set each value:
```csharp
int[] someNumbers = new int[10];
for (int index = 0; index < 10; index++)
{
    someNumbers[index] = 6; // set every element to the value 6
}
```

We can assign values to the element using literals (as shown in the previous example), using variable names, or expressions.
```csharp
int[] someNumbers = new int[10];
Random keygen = new Random();
for (int index = 0; index < someNumbers.Length; index++) // the .Length property returns the number of elements in the array
{
    someNumbers[index] = keygen.Next(1,11);
}
```

<h2>Sorting arrays<h2>
Array.Sort will sort the elements in a 1-dimensional array.
```csharp
int[] myArray = new int[5] { 6, 4, 7, 2, 8 };
Array.Sort(myArray); // now array is: {2, 4, 6, 7, 8}
```

<h2>2D arrays</h2>

```csharp
int [,] board = new int [3,3]; // first digit is the row, 2nd digit is the column
board [1,1] = 1;
```