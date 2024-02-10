---
layout: page
title: Glossary
permalink: /cpsc1012/glossary
---

> Tip: Use Ctrl-F (or Command-F on a Mac) to search for a specific term within this page.

## A
+ **Arithmetic operators** are operators we use to do math. Some common operators are:

    Operator | Meaning | Example
    --- | --- | ---
    `+` | Addition | `total = cost + tax;`
    `-` | Subtraction | `cost = total - tax;`
    `*` | Multiplication | `tax = cost * rate;`
    `/` | Division | `salePrice = original / 2;`
    `%` | Modulus | `remainder = value % 3;`


## C

+ **camelCase** is a type of capitalization where the first letter is lowercase and all remaining words are capitalized. Generally, we'll use camelCase to name our variables (e.g. `myInt`, `itemsOrdered`).

+ **Combined assignment operators** combine the assignment operator with another arithmetic operator.

    Operator | Example | which is the same as...
    --- | --- | ---
    `+=` | `x += 5;` | `x = x + 5;`
    `-=` | `y -= 2;` | `y = y - 2;`
    `*=` | `z *= 10;` | `z = z * 10;`
    `/=` | `a /= b;` | `a = a / b;`
    `%=` | `c %= 3;` | `c = c % 3;`



+ The **conditional operator** is an example of a ternary operator (it requires 3 operands).

   Here is an example of how we can use the conditional operator in place of an `if` statement.
   <script src="https://gist.github.com/dmarshNAIT/d0176ca742ae6c36918dd1f951a3b3ca.js"></script>


+ **Constants** are variables whose value cannot change.

    ```csharp
    const double GST_RATE = 0.05;
    ```

## D

+ Every variable in C# has a **data type**, which defines what kind of data it can hold (e.g. numbers with or without decimal places, strings of characters, etc). Some common data types are:

    Data type | Size | Range | Suffix
    --- | --- | --- | ---
    `byte` | 1 byte | 0 to 255
    `short` | 2 bytes | -32,768 to 32,767
    `int` | 4 bytes | -2,147,483,648 to 2,147,483,647
    `long` | 8 bytes | 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | `L`
    `float` | 4 bytes | ±1.5 x 10<sup>−45</sup> to ±3.4 x 10<sup>38</sup>, 7 digits precision | `f`
    `double` | 8 bytes | ±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup>, 15-16 digits precision | `d`
    `decimal` | 16 bytes | ±1.0 x 10<sup>-28</sup> to ±7.9228 x 10<sup>28</sup>, 28-29 significant digits | `m`

    Before a value can be stored in a variable, the value's data type **must** be compatible with the variable's data type. This is where data type ranking comes in: `int` has lower rank than `double`, which means I can assign an `int` value to a `double` variable, but not the reverse.

## E

+ **Escape sequences** are special combinations of characters that we can use in strings that aren't intrepreted literally, but rather represent something else. For example, some common escape sequences are:

   Escape Sequence | Name | Description
   --- | --- | ---
   `\n` | New line | Advances the cursor to the next line for subsequent printing
   `\t` | Horizontal tab | Causes the cursor to skip over to the next tab stop
   `\r` | Return | Causes the cursor to go to the beginning of the current line
   `\\` | Backslash | Causes the backslash to be printed
   `\'` | Single quote | Causes a single quote to be printed
   `\"` | Double quote | Causes a double quote to be printed

## I

+ **Integer division** is what happens when both operands of the division operand are integers: remainders are discarded.

    ```csharp
    double number = 5/2; // results in 2, not 2.5
    ```

    Integer division can be avoided by converting one of the numbers to a floating point number (like a `double`) first.

## L

+ **Literals** are values written into the code of a program.

    ```csharp 
    int i = 5; // 5 is a literal
    ```

+ **Logical operators** are what we use to create compound Boolean expressions.

    + `!` represents _not_ and is a logical negation.
    + `&&` represents _and_ and is a logical conjunction.
    + `||` represents _or_ and is a logical disjunction.
    + `^` represents _exclusive or_ and is a logical exclusion.

## M

+ The **Math** class provides us a number of useful methods to perform mathematical operations.

    Some handy methods are:
    + `Math.Pow(x,y)` returns x raised to the power of y.
    + `Math.Sqrt(x)` returns the square root of x.
    + `Math.Round(x)` will round a number to the nearest integer using engineering rounding. We can also pass in a second argument to specify the number of digits we'd like.

## P

+ **PascalCase** is a type of capitalization where the first letter of every word is capitalized. Generally, we'll use PascalCase to name our namespaces, classes, methods, and member fields (e.g. `DoSomething()`, `Name`).

+ **Precedence** basically tells us the order of operations. For example, unary negation will be evaluated first, then multiplication/division, then addition/subtraction.

    The precedence of the operators we've used is:
    1. `-` `!` (unary negation, logical NOT)
    1. `*` `/` `%` (multiplication, division, modulus)
    1. `+` `-` (addition, subtraction)
    1. `<` `>` `<=` `>=` (less than, greater than, less than or equal to, greater than or equal to)
    1. `==` `!=` (equal to, not equal to)
    1. `&&` (logical AND)
    1. `||` (logical OR)
    1. `=` `+=` `-=` `*=` `/=` `%=` (assignment, combined assignment)


## R

+ **Random objects** can be used to generate random numeric values.

```csharp
Random numGenerator = new Random(); 
    // creates a random number generator

int randNum1 = numGenerator.Next();
    // generates a random non-negative int
    // i.e. 0 - 2,147,483,647

int randNum2 = numGenerator.Next(5); 
    // generates a random non-negative int less than 5 
    // i.e. 0 - 4

int randNum3 = numGenerator.Next(2, 6); 
    // generates a random int that's at least 2 and less than 6 
    // i.e. 2 - 5

double randNum4 = numGenerator.NextDouble(); 
    // generates a random double that's at least 0 and less than 1
    // i.e. 0 - .999999999999999
```

+ **Relational operators** allow us to compare values.

    C# Operator | Math Symbol | Name | Example | Result if `radius = 6`
    --- | --- | --- | --- | --- 
    `<` | < | Less than | `radius < 0` | `false`
    `<=` | ≤ | Less than or equal to | `radius <= 0` | `false`
    `>` | > | Greater than | `radius > 0` | `true`
    `>=` | ≥ | Greater than or equal to | `radius >= 0` | `true`
    `==` | = | Equal to | `radius == 0` | `false`
    `!=` | ≠ | Not equal to | `radius != 0` | `true`


## S

+ **Scope** is the part of the program that has access to a variable. Variables come into existence when they are declared, and stop existing at the end of that block of code.

    For example, if I declare a variable within a `for` loop, it's only visible within that loop.

    **Variables must be declared before they are used.** Do your variables also need to be initialized, updated, and/or re-initialized?

    It is good practice to declare variables in their innermost scope. For example, if I have a counter variable in a `for` loop inside of another `do-while` loop and it isn't used anywhere else, I should probably declare it inside that `for` loop rather than at the very beginning of my program.

## V

+ **Variables** are named locations in a computer's memory. They hold one value at a time.

    ```csharp 
    int myInt; // myInt is a variable of type int
    ```

