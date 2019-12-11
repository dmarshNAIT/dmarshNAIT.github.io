---
layout: page
title: Formatting
permalink: /cpsc1012/formatting
---

# Formatting Strings

Let's say I have two variables, an `int` called `firstNum` and a `double` called `secondNum`:
```csharp
int firstNum = 150;
double secondNum = 1234.56789;
```

- I can display the numbers are they are stored, either manually:
    ```csharp
    Console.WriteLine("firstNum: " + firstNum + "  secondNum: " + secondNum);
    ```
- Or using substitution parameters:
    ```csharp
    Console.WriteLine("firstNum: {0}  secondNum: {1}", firstNum, secondNum);
    ```
- Or with string interpolation:
    ```csharp
    Console.WriteLine($"firstNum: {firstNum}  secondNum: {secondNum}");
    ```

All three of these give the same output:
```csharp
firstNum: 150  secondNum: 1234.56789
```

# Adjusting number precision

If I'm using string interpolation or substitution parameters, I can add a format string inside the braces, after a `:` symbol.

For example, let's say I want my first number to be four digits long, no decimals, and my second number to be 1 digit before the decimal and 2 digits after the decimal. i.e. The first number would be in the format `0000` and the second number would be in the format `0.00`.

```csharp
// substitution parameters:
Console.WriteLine("firstNum: {0:0000}  secondNum: {1:0.00}", firstNum, secondNum);
// string interpolation:
Console.WriteLine($"firstNum: {firstNum:0000}  secondNum: {secondNum:0.00}");
```
Either of these will result in:
```csharp
firstNum: 0150  secondNum: 1234.57
```


## What if I don't know how many digits I need?

For example, what if I want to format a number to add commas, but I don't want to force any leading or trailing zeros? I'll use the same format string (`#,##0.00`) for both variables:
```csharp
Console.WriteLine("firstNum: {0:#,##0.00}  secondNum: {1:#,##0.00}", 
    firstNum, secondNum);
// or:
Console.WriteLine($"firstNum: {firstNum:#,##0.00}  secondNum: {secondNum:#,##0.00}");
```

The `#` basically means *show a number in this place if it exists* and the `0` means *show a digit in this place no matter what*.

Thus, our output is:
```csharp
firstNum: 150.00  secondNum: 1,234.57
```

# Printing in columns

Let's say I have a table of values that I want to display. Using what we know so far, I could code the following:
```csharp
Console.WriteLine("firstNum: {0:0.00}  secondNum: {1,10:0.00}", firstNum, secondNum);
Console.WriteLine("firstNum: {0:0.00}  secondNum: {1:0.00}", 0, 0);
Console.WriteLine($"firstNum: {0:0.00}  secondNum: {0:0.00}");
Console.WriteLine($"firstNum: {firstNum:0.00}  secondNum: {secondNum:0.00}");
```

This will result in:
```csharp
firstNum: 150.00  secondNum:    1234.57
firstNum: 0.00  secondNum: 0.00
firstNum: 0.00  secondNum: 0.00
firstNum: 150.00  secondNum: 1234.57
```

That's pretty ugly. Our numbers are not very nicely aligned. So, let's add an alignment expression! The alignment expression will be the width of our column, and it will be positive or negative depending on how we want our text to be aligned.

The contents of our braces will now be: `{variable or expression to display, alignment : format string}`. For example, let's set each column to be 10 characters wide and right-aligned:
```csharp
Console.WriteLine("firstNum: {0, 10:0.00}  secondNum: {1, 10:0.00}", 
    firstNum, secondNum);
Console.WriteLine("firstNum: {0, 10:0.00}  secondNum: {1, 10:0.00}", 0, 0);
Console.WriteLine($"firstNum: {0, 10:0.00}  secondNum: {0, 10:0.00}");
Console.WriteLine($"firstNum: {firstNum, 10:0.00}  secondNum: {secondNum, 10:0.00}");
```

Results in this much more table-y output:
```csharp
firstNum:     150.00  secondNum:    1234.57
firstNum:       0.00  secondNum:       0.00
firstNum:       0.00  secondNum:       0.00
firstNum:     150.00  secondNum:    1234.57
```

If I wanted my columns to be left-aligned, we simply make the width negative:
```csharp
Console.WriteLine("firstNum: {0,-10:0.00}  secondNum: {1,-10:0.00}", 
    firstNum, secondNum);
Console.WriteLine("firstNum: {0,-10:0.00}  secondNum: {1,-10:0.00}", 0, 0);
Console.WriteLine($"firstNum: {0,-10:0.00}  secondNum: {0,-10:0.00}");
Console.WriteLine($"firstNum: {firstNum,-10:0.00}  secondNum: {secondNum,-10:0.00}");
```
Which gives us:
```csharp
firstNum: 150.00      secondNum: 1234.57
firstNum: 0.00        secondNum: 0.00
firstNum: 0.00        secondNum: 0.00
firstNum: 150.00      secondNum: 1234.57
```


## Formatting currency

There are a ton of other things we can do in string formatting, but one particularly useful one is how we can format currency.

Here are a few different ways I could format currency:
```csharp
decimal moneyAmount = 12345m;

Console.WriteLine($"{moneyAmount:$#,#.00}");
Console.WriteLine($"${moneyAmount:#,#.00}");
Console.WriteLine($"{moneyAmount:c}");
```

These all look the same:
```
$12,345.00
$12,345.00
$12,345.00
```

So why would I pick one over the other?

Let's look at our output if our currency is negative:
```csharp
decimal moneyAmount = -12345m;

Console.WriteLine($"{moneyAmount:$#,#.00}");
Console.WriteLine($"${moneyAmount:#,#.00}");
Console.WriteLine($"{moneyAmount:c}");
```
Gives us:
```
-$12,345.00
$-12,345.00
($12,345.00)
```

Each of these deals with negative numbers in a different way.

# Adding colour
Another option I have is to adjust the colour of the text that is printed to the Console.

I can change the colour of the text by changing `ForegroundColor`:

And I can highlight text by changing `BackgroundColor`.

I can then go back to the default colours by using `ResetColor`.

Here's what it'll look like all together. Try copying this to VS and viewing the output!

```csharp
// the following line will change the text colour to red:
Console.ForegroundColor = ConsoleColor.Red;

// if I didn't like red, there are a few other options. The list follows:
// Black, Blue, Cyan, DarkBlue, DarkCyan, DarkGray, 
// DarkGreen, DarkMagenta, DarkRed, DarkYellow,
// Gray, Green, Magenta, Red, White, and Yellow.

// any Console.WriteLine will now be in red text.
Console.WriteLine("Like this one.");

// I can also highlight the text, using this:
Console.BackgroundColor = ConsoleColor.Cyan;
Console.WriteLine("Now this line will be red with a cyan highlight. Beautiful.");

// at any point, I can reset back to the default colours using:
Console.ResetColor();

Console.WriteLine("Now this line is in my regular colours again.");
```

Output:

<html>
<font face="Lucida Console">
 <table>
  <tbody>
    <tr>
      <td><span style="color:red">Like this one.</span></td>
    </tr>
    <tr>
      <td style="background-color:#00ffff"><span style="color:red">Now this line will be red with a cyan highlight. Beautiful.</span></td>
    </tr>
    <tr>
      <td><span style="color:black">Now this line is in my regular colours again.</span></td>
    </tr>
  </tbody>
 </table>
</font>
</html>



