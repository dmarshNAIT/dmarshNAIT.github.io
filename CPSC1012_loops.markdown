---
layout: page
title: Loops
permalink: /cpsc1012/loops
---

# Operator Shorthand
Incrementing the value of a variable is a pretty common occurrence, and there are a way different ways we can do so. Here are 3 examples, all of which have the same net effect:
```csharp
window_count = window_count + 1;
window_count += 1;
window_count++;
```

`i++` means “give me the value **before** the increment”

`++i` means “give me the value **after** the increment”

Therefore, in this code snippet:
```csharp
int i = 2, j;
j = ++ i;
```
`j` is equal to `3`.

*Please note: `i` and `j` are terrible variable names. You should use something more descriptive in your actual code.*

# Pre-test loops
These are loops where the test happens before the process, so the process can execute 0 or more times.

## while loops
We generally use `while` loops for loops that are condition-controlled.

### Syntax:
```csharp
while (boolean expression) {
	// statements
	// including something to prevent an infinite loop!
}
```
For example, maybe we have a segment of code that is filling something, and we want to iterate until our container is full:
```csharp
bool isFull = false;
while (!isFull) { // this is the same as: while (isFull == false)
    ...
    // code to conditionally set isFull to true
    ...
} // end while
```
We will keep iterating through the loop until something sets `isFull` to true.

## for loops
`for` loops are best used when we (or the user) know how many times we will iterate through our loop.
### Syntax:
```csharp
for (initalize; test; modify)
	process;
```
- There may be zero, one, or multiple initializations, separated by commas
- There may be only one test (although it can be compound using `&&` or `||`)
- There may be zero, one, or multiple modifications, separated by commas
- There may be many process statements if braces are used

For example, we can translate this `while` loop into a `for` loop:

```csharp
while (count > 1) {
    nFactorial *= count;
    count--;
} // end while
```
```csharp
nFactorial = 1;
for (count = n; count > 1; count--) {
	nFactorial *= count;
} // end for
```
Both of these have the same net effect.

# Post-test loops
The test happens after the process, so the process will always execute at least once:

## do-while loops

We'll use a `do-while` loop if we know the code in our loop needs to execute at least one time.

### Syntax

```csharp
do {
    // process
} while (test_condition) ;
```

For example:
```csharp
long n, nFactorial, count;
char response;
Console.WriteLine("Welcome to the factorial calculator!");

do {
    Console.Write("Enter positive n value: ");
    n = long.Parse(Console.ReadLine());

    if (n >= 0)
    {
        nFactorial = 1;
        count = n;
        for (count = n; count > 1; count--)
            nFactorial *= count;
        Console.WriteLine($"N = {n}, N! = {nFactorial}");
    } // end if
    else
    {
        Console.WriteLine("ERROR: N must be at least 0.");
    } // end else

    Console.WriteLine("Enter 'Y' to continue or 'N' to exit.");
    response = char.Parse(Console.ReadLine());
} while (response == 'Y' || response == 'y');

Console.WriteLine("Thanks, please come again.");
```