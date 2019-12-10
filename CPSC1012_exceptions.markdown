---
layout: page
title: Exception Handling
permalink: /cpsc1012/exceptions
---

# Exceptions

Exceptions are unexpected conditions or errors in our program (data is not valid, arithmetic error, parsing error, etc.)

For example:
```csharp
int i = 5;
int j = 0;
Console.WriteLine(i / j);
```
results in:

`Unhandled Exception: System.DivideByZeroException: Attempted to divide by zero.`

## We can avoid this error with logic:
```csharp
int i = 5;
int j = 0;

if (j != 0)
    Console.WriteLine(i / j);
else
   Console.WriteLine("Cannot divide by zero.");
```

## Or, we can catch the exception!
```csharp
int i = 5;
int j = 0;

try { // we'll try to run the code in this block. 
    // if any of it fails, we jump to the catch block.
    Console.WriteLine(i / j);
}
catch { // this code will only run if there was an exception in the try block.
    Console.WriteLine("Cannot divide by zero.");
}
```

## We can also view the specific exception message:
```csharp
int i = 5;
int j = 0;

try {
    Console.WriteLine(i / j);
}
catch (Exception ex) {
    Console.WriteLine("Cannot divide by zero.");
    Console.WriteLine(ex.Message);
}
```

Which returns:
```
Cannot divide by zero.
Attempted to divide by zero.
```

## Throwing our own exceptions

We may also write methods which `throw` exceptions in certain conditions.

We could have a method containing a segment of code that looks something like:
```csharp
bool isValid;

// some code executes that sets isValid to true or false

if (isValid) {
    Console.WriteLine("Input was valid.");
} // end if
else {
    throw new Exception("Input is invalid.");
} // end else
```

The code calling this method would then need to handle the exception this method has thrown.
