---
layout: page
title: Cheat Sheet
permalink: /cpsc1012/cheatsheet
---

This is meant to be a quick-reference of the methods & data types we've learned so far.
If you notice any gaps or errors, please let me know!

# Topic 1 slides: Intro to Programming
No methods or data types were covered in this section.

# Topic 2 slides: Arithmetic Operators, Data Types, Programming Standards
## Methods

Methods are blocks of code that do something. There are a few "built-in" methods that we can use within our programs, including:

### Methods for communicating with our user

- `Console.Write()` prints "something" to the user. That "something" is whatever we typed inside the `()` symbols. For example, a `string` of text, the contents of a variable, or an expression that combines text and values.

    ```csharp
    Console.Write("hello"); // prints "hello"
    Console.Write(num123);  // prints the value of num123
    Console.Write("My name is " + myName);
                            // prints "My name is " followed by the vvalue of myName
    ```

- `Console.WriteLine()` does the exact same as `Console.Write()`, except it moves the cursor to the next line after printing its message.
- `Console.ReadLine()` waits for the user to type something then hit enter; then returns that text to us. It will always return the value in the form of a `string`.
    ```csharp
    // first we print the question or prompt:
    Console.Write("Please enter your name:"); 

    // then we "read" in their response & save it to a variable:
    string userName = Console.ReadLine();
    ```
- `int.Parse()` is a method that essentially turns a `string` into an `int`. After we read input from our user, if we need that value to be an `int`, this is one approach we could take to do so. Another method that works very similarly is: `Convert.ToInt32()`. For example:

    ```csharp
    // declare our variables
    string userResponse;
    int userAge;

    // print the prompt for the user
    Console.Write("Please enter your age in years:");

    // read in their answer and save as a string
    userResponse = Console.ReadLine();

    // then here is one way to convert it to an int:
    userAge = int.Parse(userResponse);

    // & here is another:
    userAge = Convert.ToInt32(userResponse);
    ```

- `double.Parse()` is just like `int.Parse()`: except it returns the number as a `double` instead. Another similar method is called `Convert.ToDouble().`

    ```csharp
    // declare our variables
    string userResponse;
    double currentTemp;

    // print the prompt for the user
    Console.Write("Please enter the temperature in Celsius:");

    // read in their answer and save as a string
    userResponse = Console.ReadLine();

    // then here is one way to convert it to an double:
    currentTemp = double.Parse(userResponse);

    // & here is another:
    currentTemp = Convert.ToDouble(userResponse);
    ```

### Methods for doing `Math`

- `Math.Pow()` lets us calculate the power, which is how many times we use a number when we multiply it by itself. For example, "3 to the power of 5" is taking the number 3 and then multiplying it 5 times: **3 x 3 x 3 x 3 x 3**. This can also be written as **3<sup>5</sup>**.
    ```csharp
    double answer = 3 * 3 * 3 * 3 * 3; // returns 3 to the power of 5
    double answerV2 = Math.Pow(3, 5);  // also returns 3 to the power of 5
    ```
- `Math.Sqrt()` returns the square root of a number. 4 squared is 4 times 4, which is 16: that means that 4 is the "square root" of 16.
    ```csharp
    double root = Math.Sqrt(16);       // root has the value of 4
    ```
- `Math.Round()` lets us round numbers, using "engineering rounding". We can specify the number and the # of digits we want, or we can just provide the number to round to the nearest integer value.
    ```csharp
    double number = 123.456789;
    Console.WriteLine("The approximate value is " + Math.Round(number));
        // displays 123
    Console.WriteLine("The approximate value is " + Math.Round(number, 2));
        // displays 123.46
    ```

## Data types
C# is a strongly typed language: each piece of data we use must have a known data type. This is true for variables, constants, even literals and expressions! The type of the data helps us know what we can do with that data: whether we can do math or change capitalization, etc.

So far we have learned about:
- `int` which holds integer values between approximately -2 billion and +2 billion. Decimals cannot be stored in an `int`: that additional information will be "lost" if we try to store a number with decimal digits as an `int`.
- `double` holds numeric values that may or may not have decimal digits. They can be very large: as large as 34 with 37 zeroes after it, or as negative as -34 with 37 zeroes after it. They can also be very, very small: more than 300 zeroes after the decimal place before the first non-zero digit. In total, they can hold up to about 15 digits, so both of these numbers are valid doubles: 123,456,789,012,345 or 0.123456789012345.
- `string` contains text. That text is a string of characters: could contain letters, digits, punctuation or spaces. We'll deal with `string`s often, as every time we read input from the user using `Console.ReadLine()` it'll initially come in as a `string`.


# Topic 3
- Coming soon!


