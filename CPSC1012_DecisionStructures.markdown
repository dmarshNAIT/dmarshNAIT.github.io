---
layout: page
title: Decision Structures
permalink: /cpsc1012/decisionstructures
---

Programs can decide which statements to execute based on a condition.

```csharp
if (radius < 0) {
	Console.WriteLine("Incorrect input");
}
else {
	double area = radius * radius * 3.14159;
	Console.WriteLine("Area is " + area);
}
```

C# has several types of selection statements: one-way `if` statements, two-way `if-else` statements, nested `if` statements, multi-way `if-else-if` statements, `switch` statements, and conditional operators.

+ **One-way `if` statements**

    Executes an action if the specified condition is `true`. Otherwise, do nothing.

    The syntax is:
    ```csharp
    if (boolean_expression) {
		statement(s)
	}
    ```

    For example:

    ```csharp
    if (radius > 0) {
	    double area = Math.Pow(radius,Math.PI);
	    Console.WriteLine($"The area for the circle of radius {radius} is {area}");
    }
    ```
+ **Two-way `if-else` statements**

    An `if-else` statement decides the execution path based on whether the condition is `true` or `false`.

    The syntax is:
    ```csharp
    if (boolean-expression) {
        statement(s)-for-true-case
    }
    else {
        statement(s)-for-false-case
    }
    ```

    For example:
    ```csharp
    if (number % 2 == 0) {
        Console.WriteLine($"{number} is even");
    }
    else {
        Console.WriteLine($"{number} is odd");
    }
    ```

+ **Nested `if` statements**

    An `if` statement can be inside another `if` statement to form a nested `if` statement.

    ```csharp
    if (isHungry)
        if (money > 10)
            Console.WriteLine("I’ll buy lunch.");
        else
            Console.WriteLine("no lunch for me");
    else
        Console.WriteLine("no lunch for me");
    ```

+ **Switch statements** execute based on the value of a variables or expression.

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
    }
    ```




