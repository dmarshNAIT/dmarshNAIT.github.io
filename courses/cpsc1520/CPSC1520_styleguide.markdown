---
layout: page
title: CPSC 1520 Style Guide
permalink: /cpsc1520/styleguide
parent: CPSC1520
nav_order: 2
---

# Style Guide
Adapted from [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html).

These guidelines are expected to be followed in all submissions for Dana's sections of CPSC 1520. If you have another instructor, please confirm with them what style guide they expect you to use: just like companies may use different style guides in industry.

## Variables & Functions
- Use `const` by default, or `let` when a variable needs to be reassigned.
- Only one variable per declaration.
- Variables are declared when needed (not all together at the start).
- Arrow functions are preferred over the `function` keyword.

## Names
- **File names** must be in **lowercase** and with **no punctuation** other than underscores or dashes.
- Use only letters and digits in your **descriptive** names, with appropriate capitalization:
    - **Classes** in PascalCase.
    - **Methods**, **variables**, and **parameters** in camelCase.
    - True **constants** in UPPERCASE_LETTERS, also known as SCREAMING_SNAKE_CASE.

# Punctuation
- **Semicolons** are required for every statement.
- **Braces** are used around structures even if they only contain a single statement. e.g. `if`, `do`, `for`, etc
    - *Except*: when the entire `if` statement fits on one line:
        ```js
        if(shortCondition()) doThing();
        ```
- Use **trailing** commas e.g. for arrays that span multiple lines.
- Use single quotes for **string** literals.

# White Space
- One statement per line.
- The content of a structure is indented. e.g. the body of a `function`, `switch`, `if`, `while`, etc
- Blank lines are used to create logical groupings of elements.
- A single space is on both sides of binary and ternary operators, and `//`.
- A single space follows a comma or semi-colon.

# Misc.
- Switch statements always include a `default` statement, even if it's empty.
- JSDoc is used on all classes, fields, and methods.