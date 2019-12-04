---
layout: page
title: Formatting
permalink: /cpsc1012/formatting
---

# Formatting Strings
## Default formatting:
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine("i: {0} f: {1}", i, f);
```
results in:
```
i: 150 f: 1234.56789
```

## Adjusting precision:
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine("i: {0:0000} f: {1:0.00}", i, f);
```
results in:
```
i: 0150 f: 1234.57
```

## Getting really fancy...
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine ( "i: {0:#,##0} f: {1:##,##0.00}", i, f );
```
results in:
```
i: 150 f: 1,234.57
```

## Print in columns:
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine("i: {0,10:0} f: {1,15:0.00}", i, f);
Console.WriteLine("i: {0,10:0} f: {1,15:0.00}", 0, 0);
```
results in:
```
i:        150 f:         1234.57
i:          0 f:            0.00
```

Or we can left-align:
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine("i: {0,-10:0} f: {1,-15:0.00}", i, f);
Console.WriteLine("i: {0,-10:0} f: {1,-15:0.00}", 0, 0);
```
results in:
```
i: 150        f: 1234.57        
i: 0          f: 0.00           
```

## All together:
```csharp
int i = 150;
double f = 1234.56789;
Console.WriteLine("i: {0} f: {1}", i, f);
// this just writes the two numbers, as-is

Console.WriteLine("i: {0:0000} f: {1:0.00}", i, f);
// adding a colon and then a format pattern lets me set the precision of the two numbers.
// I'm saying: make the first number four digits, and the second number 1 digit before the decimal and 2 digits after the decimal.

Console.WriteLine("i: {0:#,##0} f: {1:##,##0.00}", i, f);
// I can also save spot for optional numbers using the # symbol, and include commas

Console.WriteLine("i: {0,10:0} f: {1,15:0.00}", i, f);
Console.WriteLine("i: {0,10:0} f: {1,15:0.00}", 0, 0);
// the number between the comma and the colon sets the column width

Console.WriteLine("i: {0,-10:0} f: {1,-15:0.00}", i, f);
Console.WriteLine("i: {0,-10:0} f: {1,-15:0.00}", 0, 0);
// if the column width is negative, it left-justifies the text
```

# Adding colour
```csharp
// the following line will change the text colour to red:
Console.ForegroundColor = ConsoleColor.Red;

// if I didn't like red, there are a few other options. The list follows:
// Black, Blue, Cyan, DarkBlue, DarkCyan, DarkGray, DarkGreen, DarkMagenta, DarkRed, DarkYellow,
// Gray, Green, Magenta, Red, White, and Yellow.

// any Console.WriteLine will now be in red text.
Console.WriteLine("Like this one.");

// I can also highlight the text, using this:
Console.BackgroundColor = ConsoleColor.Cyan;

// at any point, I can reset back to the default colours using:
Console.ResetColor();

Console.WriteLine("Now this line is in my regular colours again.");
```