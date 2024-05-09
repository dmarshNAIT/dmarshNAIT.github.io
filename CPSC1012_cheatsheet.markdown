---
layout: page
title: Cheat Sheet
permalink: /cpsc1012/cheatsheet
---

This is meant to be a quick-reference of the methods & data types we've learned so far.
If you notice any gaps or errors, please let me know!

> **Tip**: Use Ctrl-F (or Command-F on a Mac) to search for specific words on this page.


# Topic 1: Intro to Programming
No methods or data types were covered in this section.

# Topic 2: Arithmetic Operators, Data Types, Programming Standards
## Methods

Methods are blocks of code that do something. There are a few "built-in" methods that we can use within our programs, including:

### Methods for communicating with our user

- `Console.Write()` prints "something" to the user. That "something" is whatever we typed inside the `()` symbols. For example, a `string` of text, the contents of a variable, or an expression that combines text and values.

    ```csharp
    Console.Write("hello"); // prints "hello"
    Console.Write(num123);  // prints the value of num123
    Console.Write("My name is " + myName);
                            // prints "My name is " followed by the value of myName
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
    double answer; // create a variable to hold the result

    answer = 3 * 3 * 3 * 3 * 3; // returns 3 to the power of 5
    answer = Math.Pow(3, 5);  // also returns 3 to the power of 5
    ```
- `Math.Sqrt()` returns the square root of a number. 4 squared = 4 * 4 = 16: that means that 4 is the "square root" of 16.
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
- There are other numeric data types: some hold [integer values](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) and others are designed for [numbers which may have decimals](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types). 
    - e.g. `decimal` numbers can hold up to 15-17 digits and are preferred in situations where we want extremely precise numbers without round errors, like financial data.
- `string` contains text. That text is a string of characters: could contain letters, digits, punctuation or spaces. We'll deal with `string`s often, as every time we read input from the user using `Console.ReadLine()` it'll initially come in as a `string`. Literal values for `string`s are surrounded by double quotes.
    - e.g. `string myName = "Bob";`
- `char` holds a single character. Literal values for `char`s are surrounded by single quotes.
    - e.g. `char menuChoice = 'c';`
- `bool` is short for Boolean. Variables of this type can only hold one of 2 values: `true` or `false`. They are often used to represent logical conditions, and will usually be named  starting with a word like `is` or `has`.
    - e.g. 
    ```csharp
    bool isValid = false;
    // other code
    if (isValid) {
        // do something
    }
    ```
    - or 
    ```csharp
    bool canContinue = true;
    do {
        // do something
    } while (canContinue);
    ```


# Topic 3: Decision Structures
- `if` statements let us make decisions in our code. For example, after answering a math quiz, we may either congratulate the user `if` they achieved a certain score, or `else` we show a different message. [Read more on the Decision Structures page.](./decisionstructures)

- `switch` statements are similar but were designed to check for specific values. [Read more on the Decision Structures page.](./decisionstructures)

- **Relational operators** allow us to compare values.

    C# Operator | Math Symbol | Name | Example | Result if `radius = 6`
    --- | --- | --- | --- | --- 
    `<` | < | Less than | `radius < 0` | `false`
    `<=` | ≤ | Less than or equal to | `radius <= 0` | `false`
    `>` | > | Greater than | `radius > 0` | `true`
    `>=` | ≥ | Greater than or equal to | `radius >= 0` | `true`
    `==` | = | Equal to | `radius == 0` | `false`
    `!=` | ≠ | Not equal to | `radius != 0` | `true`



- **Logical operators** are what we use to create compound Boolean expressions.

    + `!` represents _not_ and is a logical negation. It changes a Boolean value to the opposite value.
        - e.g. `!true` has the value of `false`.
    + `&&` represents _and_ and is a logical conjunction. It is used to connect 2 complete but separate Boolean expressions, and is only `true` if **both** expressions are `true`.
        - e.g. `true && false` has the value of `false`.
    + `||` represents _or_ and is a logical disjunction. It is used to connect 2 complete but separate Boolean expressions, and is `true` if **at least one** of the expressions are `true`.
        - e.g. `true && false` has the value of `true`.
    + `^` represents _exclusive or_ and is a logical exclusion. It is used to connect 2 complete but separate Boolean expressions, and is only `true` if **exactly one** of the expressions are `true`.
        - e.g. `true ^ false` has the value of `true`.

- The **conditional operator** is basically a miniature `if else` structure.

   Here is an example of how we can use the conditional operator in place of an `if` statement.
   <script src="https://gist.github.com/dmarshNAIT/d0176ca742ae6c36918dd1f951a3b3ca.js"></script>

# Topic 4: Loops
Loops are structures that let us repeat commands without re-typing them. We start off with 3 types of loops, each with their own purpose. [Read more on the Loops page.](./loops)
- `for` loops are used when we know exactly how many times our loop must repat, or iterate. For example, maybe this is hardcoded value in our code (e.g. we always ask for 10 values) or perhaps the user decides. Either way, if we know before entering the loop how many times it must repeat, `for` loops are the best fit.
- `do while` loops execute once, then check a condition to see if they should continue to execute. This is perfect for code that must run at least once: for example, displaying a main menu or asking for valid input.
- And finally, `while` loops are used for everything else. The condition is checked first, so it is possible the loop executes once, many times, or maybe not at all!

# Topic 5: File I/O & Exceptions
- The `StreamReader` class can be used to get information from text files, and the `StreamWriter` class can be used to write (or save) information to a text file. [Read more on the File IO page.](./fileIO)
- Sometimes problems will occur in our program that cause it to crash. For example, perhaps we ask our user to enter their age and we attempt to save it as an `int`, but they enter a number that contains decimals. We must add something into our code to deal with this problem instead of crashing. One approach we can take is using a `try`/`catch` structure. [Read more on the Exceptions page.](./exceptions)

# Topic 6: Methods
In this section we learn how to create our own custom methods.
- Every method has a `return` type: this tells us essentially what "output" that method will create when we execute it.
    - Some methods have a `return` type of `void`: this means they don't `return` anything. For example, `Console.WriteLine()`.
    - Other methods will specify a data type as their `return` type. For example, `Console.ReadLine()` always `return`s a `string`; that means that `string` is its return type, and somewhere in the code that defines that method we will see the keyword `return` followed by the value it is returning. Here is a silly example of a custom method that returns an `int`:
        ```csharp
        static int GiveMeFive() {
            return 5;
        }
        ```
- Methods may or may not have **parameters**: they look and act a lot like variables. They are essentially the "input" into the method: in other words, what values the method needs in order to run. They are defined in between the parenthese in a method header, and just like variables, we must define their data type as well as give them a name.
    - Then, when we call that method, we must provide matching arguments. In other words, we must provide values or expressions in between the parentheses that match the data type of the parameters.

# Topic 7: Arrays
- If we think of variables as a box holding a single value, we can think of arrays as a large box split up into separate compartments, each holding its own value. Every compartment within an array must contain the same data type. For example, here is how to create an array that can hold up to 10 `int` values: 
    - `int[] myArray = new int[10];`
- If we provide starting values for each element, we don't need to provide the array size: 
    - `string[] dayOfWeek = { "SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT" }; `
- If we do not provide a starting value, every element has the default value for that data type. For example, `int` defaults to `0` and `bool` defaults to `false`.
- We can access individual elements of an array using square brackets, where the number within the brackets refers to the element #. Note: the first element is index `0`.
    - `myArray[7]` refers to the value in element 7 of our array.
- The elements within an array can be ordered from smallest to largest using a method called `Array.Sort()`. 
    - `Array.Sort(myArray)` results in `myArray` having its values sorted from smallest to largest. Arrays are a `ref`erence type: this means that when we pass them into a method they can actually be changed by that method!

# Topic 8: Classes & Objects
- Within a class, both methods & fields can be defined as `private` or `public`.
    - `private` means the member is only visible to members of that class. e.g. I can only access a specific field, or call a specific method, from **within** the same class.
    - `public` means that the member is available to anyone, from anywhere.
- Classes will have methods that fall into a few categories:
    - accessor methods: these let us *access* a specific field. They are usually named starting with the word Get, like `GetName()`.
    - mutator methods: these let us mutate, or change, the value of a specific field. They are usually named starting with the word Set, like `SetName()`.
    - constructor methods: these create a new instance of the Class
    - any other methods that support the functionality of the Class
- The keyword `this` lets us refer to the current object.
    - e.g. `return this.Age` means to return the `Age` of the current object.
- Methods marked as `static` do not require an object to be created in order to use the method.
- A `List` is another type of collection class, similar to an `Array`, but which is a bit more flexible. Instead of a set size, it will dynamically change its size as needed.