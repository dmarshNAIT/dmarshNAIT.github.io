---
layout: page
title: Loops
permalink: /cpsc1012/loops
---

# Operator Shorthand
Three different ways of writing the same increment:
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

# Pre-test loops
These are loops where the test happens before the process, so the process can execute 0 or more times.

## `while` loops

### Syntax:
```csharp
while (test) {
	// statements
	// including something to prevent an infinite loop!
}
```
## `for` loops
```csharp
for (initalize; test; modify)
	process;
```
- There may be zero, one, or multiple initializations, separated by commas
- There may be only one test (although it can be compound using `&&` or `||`)
- There may be zero, one, or multiple modifications, separated by commas
- There may be many process statements if braces are used

We can translate a `while` loop into a `for` loop:

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

# Post-test loops
The test happens after the process, so the process will always execute at least once:

## `do-while` loops

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