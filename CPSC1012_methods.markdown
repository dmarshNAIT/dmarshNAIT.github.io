---
layout: page
title: Modularization
permalink: /cpsc1012/methods
---

# Methods

Methods let us re-use pieces of code.

Methods let us break down large tasks into a number of smaller tasks.

- Helps keep code organized!

A parameter is a way to pass values into a method call. It's defined in the method header and used in that method.

An argument is the value we supply to the method when it's called.

Methods can also return values to the caller (e.g. `ReadLine()` returns a string).

## Arguments

### Passing by value:
- Passing an argument as a value passes a copy of the value. It doesn't change the original value.

### Passing by reference:
- This means passing in the actual memory location where that value is stored. This will change the original value of the variable.
- `Out` references are a little less common. These let us change the value of the referenced variable.

## Method Libraries

Do you have code snippets you're using a lot? For example:
- Reading input from a user
- Displaying a list of options
- Validating input
- etc

These are all candidates for your own method library.
Save 'em somewhere useful! (Maybe a github repo….)

## Variables & Scope
Where a variable has value: "in scope"

- Otherwise: "out of scope"

Remember: anything declared in a block of code will stop existing once that block ends (i.e. once we hit the `}`).

**Variables must be declared before they are used.** Do your variables also need to be initialized, updated, and/or re-initialized?

## Syntax

### Calling a void method:
```csharp
static void Main(string[] args) {
    DoSomething();
} 

static void DoSomething() {
    Console.WriteLine("Something.");
}
```

### Calling a method that returns something:
```csharp
static void Main(string[] args) {
    int i = DoSomething();
} 

static int DoSomething() { // methods can also return string, double, etc.
    Console.WriteLine("Something.");
    return 5;
}
```

### We can also pass in arguments:
```csharp
static void Main(string[] args) {
    int i = 3;
    DoSomething(i); // passing a variable's value
    DoSomething(5); // passing a literal value
    DoSomethingElse(5, "hello"); // passing multiple values
    DoSomethingElse(i: 5, message: "hello");  
        // we can also explicitly name the arguments we're passing in
} 

static void DoSomething(int i) { // a method with one parameter
    Console.WriteLine($"You passed in {i}");
}

static void DoSomethingElse(int i, string message) { // this method has two parameters
    Console.WriteLine(message);
    Console.WriteLine($"You passed in {i}");
} 
```

### Passing in references:
```csharp
static void Main(string[] args) {
    int i = 5;
    Console.WriteLine($"i was originally {i}");
    MultiplyByTwo(ref i);
    Console.WriteLine($"now its value is {i}");
            // the value of i has changed
} 

static void MultiplyByTwo(ref int j) {
    j = j * 2;
}
```

### Setting default values for parameters:
```csharp
static void Main(string[] args) {
    int i = 3;
    DoSomething(true);
    DoSomething(i == 3); 	// equivalent to DoSomething(true)
    DoSomething(); 		    // defaults to DoSomething(false)
} 

static void DoSomething(bool isValid = false) { 
        // that means: if no value is provided, default to FALSE
    if (isValid)
        Console.WriteLine("This is the valid branch.");
    else
        Console.WriteLine("Invalid!");
}
```