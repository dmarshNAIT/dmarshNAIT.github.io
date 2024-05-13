---
layout: page
title: Coding Standards
permalink: /cpsc1012/standards
parent: CPSC1012
nav_order: 3
---

This is a quick-reference of some commonly used coding practices & standards that will be expected within this course.

# Naming Conventions
- **Always give variables a descriptive and meaningful name using camelCase.** It should be clear from the variable's name what value the variable contains. Vague names like `num1` make for poor readability.
- Name Boolean variables & properties with an **affirmative** phrase (`CanSeek` instead of `CantSeek`). You can also prefix Boolean properties with `is`, `can`, or `has`.
    - e.g. `isValid`, `canContinue`, `hasValue`
    - This style makes for improved readability: e.g. `if(isValid)` or `while(canContinue)`
- Use SCREAMING_SNAKE_CASE for **constant** names.
- Give **methods** names that are verbs or verb phrases, using PascalCase. 
    - e.g. `CalculateSum()` rather than `Sum()`.

# Declaring Variables
- All variables will be declared at the beginning of the **innermost scope** in which they are required.
    - That means we don't have a huge list of variables at the start of the program; instead we have a section at the start of each structure (e.g. the first statements within a `do while` loop) containing the variables needed within that block.
    - That also means we don't have to hunt through the code to find out where your variables are declared, as they are not  mixed in with the rest of your logic.

# Data Types
- Use `int` rather than **unsigned** types. The use of `int` is common throughout C#, and it's easier to interact with other libraries when you use `int`.
- Use `var` only when a reader can infer the type from the expression, and a **more specific data type** is not known by the programmer. 

# Jump Statements
- `break` is not to be used other than to **terminate** a `case` in a `switch` statement.
- `continue` and `goto` should not be used. Both result in **unstructured** code and poor scope management.
- `void` methods do not need a `return` statement. All other methods should have exactly 1 `return` statement.


# Style
- User **input** should be on the same line as the prompt, unless there is no room to do so. e.g. use `Console.Write()` instead of `WriteLine()` for user prompts.
- Please make it clear to **the user** what they are expected to enter. e.g. if you ask the user if they want to continue, are you expecting them to type "y" or "yes" or something else?
- Do not use `ReadLine()` and `ReadKey()` interchangeably: one trains the user to type their response then hit Enter, the other immediately takes input and hitting Enter would actually bring us to the next user prompt. Switching back and forth between these 2 is a confusing and jarring user experience.
- Write only **one statement** per line.
- Write code with **clarity** and **simplicity** in mind.
- Avoid overly complex and convoluted code logic.
- **Align** code **consistently** to improve readability. 
    - ***Tip***: Visual Studio does this automatically if you click "Format Document".



> Tips adapted from learn.microsoft.com & the Code Assessment Standards available on our Moodle course page.
> - [Common C# code conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions?redirectedfrom=MSDN)
> - [C# programming guide](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/?redirectedfrom=MSDN)
> - [Names of Type Members](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-type-members)