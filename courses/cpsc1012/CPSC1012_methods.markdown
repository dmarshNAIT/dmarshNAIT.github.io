---
layout: page
title: Modularization
permalink: /cpsc1012/methods
parent: CPSC1012
nav_order: 9
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
- Methods **can** also **`return`** values to the caller (e.g. `ReadLine()` returns a `string`), but they do not **have** to `return` anything. We call those (methods that don't return anything) `void` methods.

💡 A method may or may not have parameters, and may or may not return something. Any combination is valid!
For example:
- `Console.ResetColor()` has no parameters & a `void` return type.
- `Console.ReadLine()` has no parameters but does return something (a `string`).
- `Console.Write("hello")` has a parameter & a `void` return type.
- `Math.Round(3.14159)` has a parameter & returns something (a `double`).

Now that we have our terminology and know all our options, let's get into the details.


## 📥 Arguments
Let's learn a bit more about *arguments*, what is supplied between the `()` when we call an existing method. Think about arguments as the "input" to a method. Arguments can be passed in 2 ways:

### Passing by value:
- Passing an argument as a **value** passes a **copy** of the value. It doesn't change the original variable/value. For example, when I pass an `int` variable as an argument to the method, that  method can use that value, but cannot *change* the value of that variable.

    For example, let's say we've created a method called `DoSomething`:
    ```csharp
    static void DoSomething(int inputValue) { 
        Console.WriteLine($"You passed in {inputValue}");
        input = 100;
    } 
    ```

    We can call it by passing in a value for the argument:
    ```csharp
    DoSomething(5);         // prints "You passed in 5."
    ```
    or
    ```csharp
    int myNum = 3;
    DoSomething(myNum);     // prints "You passed in 3."
    // the variable name ("myNum") doesn't need to match the parameter name ("inputValue"): we just need to match the data type.

    // now, let's see what happens to the value of that variable:
    Console.WriteLine(myNum);   // still 3

    ```



### Passing by reference:
- This means passing in the actual memory location where that value is stored. This can change the original value of the variable. Arrays are **reference** types, so they are always passed in as a reference, which means the called method has the ability to view and change its elements.
- If I want to pass in an `int` (or any other non-reference type) by reference, I need to preface the datatype with `ref` in both the method header (i.e. the **parameter**) and the method call (i.e. the **argument**).

    Let's see what that looks like. First, let's create a method that expects an argument to be passed in as a `ref`erence:

    ```csharp
    static void MultiplyByTwo(ref int j) {
        j = j * 2;
    } 
    ```

    Now, let's call it:
    ```csharp
    int i = 5;
    Console.WriteLine($"i was originally {i}"); // i was originally 5

    MultiplyByTwo(ref i);

    Console.WriteLine($"now its value is {i}"); // now its value is 10
    ```



- There is a special kind of reference called an `out` reference: this means the called method can *change* the value of the referenced variable, but it cannot *view* the current value. To use an `out` reference, we preface the datatype with `out` in both the method header and the method call, instead of `ref`.
  - An example of a `System` method that uses an `out` reference is `TryParse`:
    ```csharp
    string userInputString;
    char userInputChar;
    ...
    bool isValidInput = char.TryParse(userInputString, out userInputChar);
    ```

### Bonus content: setting default values for parameters:
We can also set default values for parameters. These default values are used if a corresponding argument is not passed in. ⚠️ Warning: order is important here, if there are multiple parameters!

First, let's create a method with a default value for a parameter:
```csharp
    static void DoSomething(bool isValid = false) { 
    // this means: if no value is provided, default to FALSE

        if (isValid) {
            // do something
        }
        else {
            // do something else
        }
    } 
```

Now, when we call this method, we can still provide an argument if we want to, but if we don't provide one, the default value is used instead.

```csharp
    int i = 3;

    DoSomething(true);
    DoSomething(i == 3);    // equivalent to DoSomething(true)
    DoSomething();          // defaults to DoSomething(false)
```




## 📤 Return types
Another important consideration is whether or not the called method has an "output": what is its `return` type?

### Calling a `void` method:
`void` methods are methods that do not return anything.

For example:
```csharp
static void DoSomething() {
    Console.WriteLine("Something.");
} 
```
can be called like this:
```csharp
DoSomething();
```

### Calling a method that `return`s something:
If a method isn't `void`, we need to ensure we have a `return` statement somewhere in that method. Then, the code that calls that method can take that returned value and use it or assign it to a variable.
```csharp
static int DoSomething() { // this method returns an int
    Console.WriteLine("Something.");
    return 5;
} /
```
Now to call this method, I still call the method the same way, but I need to be prepared for the value that will be `return`ed. Often, we will save the returned value to a variable to be used later.
```csharp
int i = DoSomething();
```
> 🟰 Remember: the assignment operator (`=`) always takes the value from the right and assigns it to the variable on the left. In other words, the output from `DoSomething` will be "saved" in the poorly-named variable `i`.
