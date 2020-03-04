---
layout: page
title: Decision Structures
permalink: /cpsc1012/decisionstructures
---

Programs can decide which statements to execute based on a condition.

```csharp
if (radius < 0) {
	Console.WriteLine("Incorrect input");
} // end if
else {
	double area = radius * radius * Math.PI;
	Console.WriteLine("Area is " + area);
} // end else
```

C# has several types of selection statements: one-way `if` statements, two-way `if-else` statements, nested `if` statements, multi-way `if-else-if` statements, `switch` statements, and conditional operators.

# **One-way `if` statements**

Executes an action if the specified condition is `true`. Otherwise, do nothing.

The syntax is:
```csharp
if (boolean_expression) {
    // statement(s)
} // end if
```

For example:

```csharp
if (radius > 0) {
    double area = Math.Pow(radius, Math.PI);
    Console.WriteLine($"The area for the circle of radius {radius} is {area}");
} // end if
```
# **Two-way `if-else` statements**

An `if-else` statement decides the execution path based on whether the condition is `true` or `false`.

The syntax is:
```csharp
if (boolean-expression) {
    // statement(s)-for-true-case
} // end if
else {
    // statement(s)-for-false-case
} // end else
```

For example:
```csharp
if (number % 2 == 0) {
    Console.WriteLine($"{number} is even");
} // end if
else {
    Console.WriteLine($"{number} is odd");
} // end else
```

# **Nested `if` statements**

An `if` statement can be inside another `if` statement to form a nested `if` statement.

```csharp
if (isHungry) {
    if (money > 10) {
        Console.WriteLine("I’ll buy lunch.");
    } // end inner if
    else {
        Console.WriteLine("no lunch for me");
    } // end inner else
} // end outer if
else {
    Console.WriteLine("no lunch for me");
} // end outer else
```

# **Switch statements** 

Switch statements execute based on the *value* of a variable or expression.

```csharp
switch (variable or expression to check) {
    case value1:        // if (the expression we're checking == value1)
        statements(s);  // then we execute these statements
        break;          // then break out of the structure
    case value2:
        statements(s);
        break;
    ...
    default:            // if none of the above cases matched
        statement(s)-for-default;
        break;
} // end switch
```


# Common errors:
- Using `=` instead of `==` to compare primitive values
- Forgetting to enclose an `if` statement’s boolean expression in parentheses
- Writing a semicolon at the end of an `if` clause
- Forgetting to enclose multiple conditionally executed statements in braces
- Omitting the trailing `else` in an `if-else-if` statement
- Not writing complete Boolean expressions on both sides of a logical `&&` or `||` operator
- Using a `switch` expression that is not an `int`, `char`, or `string`
- Using a `case` expression that is not a literal or `const` variable
- Forgetting to write a colon at the end of a `case` statement
- Forgetting to write a `default` section in a `switch` statement
- Reversing the `?` and the `:` when using the conditional operator


