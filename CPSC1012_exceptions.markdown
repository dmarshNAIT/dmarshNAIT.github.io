---
layout: page
title: Exception Handling
permalink: /cpsc1012/exceptions
---

# Exceptions

Exceptions are **unexpected** conditions or errors in our program (data is not valid, arithmetic error, parsing error, etc.)

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

if (j != 0) {
    Console.WriteLine(i / j);
} // end if
else {
   Console.WriteLine("Cannot divide by zero.");
} // end else
```

## Or, we can catch the exception!
```csharp
int i = 5;
int j = 0;

try { // we'll try to run the code in this block. 
    // if any of it fails, we jump to the catch block.
    Console.WriteLine(i / j);
} // end try
catch { // this code will only run if there was an exception in the try block.
    Console.WriteLine("Cannot divide by zero.");
} // end catch
```

## We can also view the specific exception message:
```csharp
int i = 5;
int j = 0;

try {
    Console.WriteLine(i / j);
} // end try
catch (Exception ex) {
    Console.WriteLine("Cannot divide by zero.");
    Console.WriteLine(ex.Message);
} // end catch
```

Which returns:
```
Cannot divide by zero.
Attempted to divide by zero.
```

## We can catch exceptions of many kinds. A common exception is when we parse our user's input.

For example
```csharp
int userAge;
Console.WriteLine("How old are you?");
userAge = int.Parse(Console.ReadLine());
```
This works perfectly if the user enters a number. But what if the user enters something else, like the word "eight"?

An **exception**!

We can move this into a `try`/`catch` block:
```csharp
int userAge;
Console.WriteLine("How old are you?");

try
{
    userAge = int.Parse(Console.ReadLine());
} // end try
catch (Exception)
{
    Console.WriteLine("Invalid input!");
} // end catch
```

Now, the program doesn't crash, but instead returns a message back to the Console. 

We can continue to build on this example by moving the code inside of a loop, which we remain in until the user enters a valid number:
```csharp
int userAge;
bool validInput = false; // default value, will be set to true if parsing is successful
Console.WriteLine("How old are you?");

while (!validInput)
{
    try
    {
        userAge = int.Parse(Console.ReadLine());
        validInput = true;
    } // end try
    catch (Exception)
    {
        Console.WriteLine("Invalid input! Please re-enter.");
    } // end catch

} // end while

Console.WriteLine("We got to the end!");
```

An alternative way to deal with parsing exceptions would be to use the `.TryParse()` method. This returns a `bool` that is `true` if the parsing was successful, and `false` otherwise, and when we call this method, we pass in a `string` that we want to parse, and an `out` reference of the variable where the parsed data should be stored.

For example:
```csharp
string rawInputString = Console.ReadLine();
int userInt;
bool parsingSuccessful = int.TryParse(rawInputString, out userInt);
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
