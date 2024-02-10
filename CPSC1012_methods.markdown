---
layout: page
title: Modularization
permalink: /cpsc1012/methods
---

# Methods

Methods let us **re-use** pieces of code, break down large tasks into a number of smaller tasks, and help us keep our code organized.

Some methods we might want to start collecting for our own personal **method libraries** are:
- methods to read and validate input from a user
- displaying a list of options
- displaying an array
- formatting outputs a certain way
- and so on

If we write the methods in our method libraries well, we can reuse them over and over and over again!

A few definitions before we get into examples:
- A **parameter** is a way to pass values or references into a method. Parameters are defined in the method header.
- An **argument** is the value we supply to the method when we call it.
- Methods can also **return** values to the caller (e.g. `ReadLine()` returns a `string`), but they do not have to. We call those (methods that don't return anything) `void` methods.


## Arguments

### Passing by value:
- Passing an argument as a **value** passes a **copy** of the value. It doesn't change the original variable/value. For example, when I pass an `int` variable as an argument to the method, that  method can use that value, but cannot *change* the value of that variable.

### Passing by reference:
- This means passing in the actual memory location where that value is stored. This can change the original value of the variable. Arrays are **reference** types, so they are always passed in as a reference, which means the called method has the ability to view and change its elements.
- If I want to pass in an `int` (or any other non-reference type) by reference, I need to preface the datatype with `ref` in both the method header (i.e. the **parameter**) and the method call (i.e. the **argument**).
  - There is a special kind of reference called an `out` reference: this means the called method can *change* the value of the referenced variable, but it cannot *view* the current value. To use an `out` reference, we preface the datatype with `out` in both the method header and the method call.
  - An example of a `System` method that uses an `out` reference is `TryParse`:
    ```csharp
    string userInputString;
    char userInputChar;
    ...
    bool isValidInput = char.TryParse(userInputString, out userInputChar);
    ```

## Syntax

### Calling a void method:
`void` methods are methods that do not return anything.
```csharp
static void Main(string[] args) {
    DoSomething();
} // end method

static void DoSomething() {
    Console.WriteLine("Something.");
} // end method
```

### Calling a method that returns something:
If in our method header, we define what our method returns (in this example, the method is returning an `int`), we need to ensure we have a `return` statement somewhere in that method. Then, the code that calls that method can take that returned value and use it or assign it to a variable.
```csharp
static void Main(string[] args) {
    int i = DoSomething();
} // end method

static int DoSomething() { // methods can also return string, double, etc.
    Console.WriteLine("Something.");
    return 5;
} // end method
```

### We can also pass in arguments:
Here is an example of a method with a single parameter, and one with two parameters. We define the datatype of each parameter, and give it a name so we can reference it within the method.

Each time we call the methods, we need to pass in corresponding arguments.
```csharp
static void Main(string[] args) {
    int i = 3;
    DoSomething(i); // passing a variable's value
    DoSomething(5); // passing a literal value
    DoSomethingElse(5, "hello"); // passing multiple values
    DoSomethingElse(i: 5, message: "hello");  
        // we can also explicitly name the arguments we're passing in
} // end method

static void DoSomething(int i) { // a method with one parameter
    Console.WriteLine($"You passed in {i}");
} // end method

static void DoSomethingElse(int i, string message) { // this method has two parameters
    Console.WriteLine(message);
    Console.WriteLine($"You passed in {i}");
} // end method
```

### Passing in references:
We can also pass in arguments by reference. This means the method has the ability to view and change the variable we are passing in.
```csharp
static void Main(string[] args) {
    int i = 5;
    Console.WriteLine($"i was originally {i}");
    MultiplyByTwo(ref i);
    Console.WriteLine($"now its value is {i}");
            // the value of i has changed
} // end method

static void MultiplyByTwo(ref int j) {
    j = j * 2;
} // end method
```

### Setting default values for parameters:
We can also set default values for parameters. These default values are used if a corresponding argument is not passed in. Warning: order is important here!
```csharp
static void Main(string[] args) {
    int i = 3;
    DoSomething(true);
    DoSomething(i == 3);    // equivalent to DoSomething(true)
    DoSomething();          // defaults to DoSomething(false)
} // end method

static void DoSomething(bool isValid = false) { 
        // that means: if no value is provided, default to FALSE
    if (isValid)
        Console.WriteLine("This is the valid branch.");
    else
        Console.WriteLine("Invalid!");
} // end method
```