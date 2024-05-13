---
layout: page
title: CPSC 1520 Quick Reference
permalink: /cpsc1520/QuickReference
parent: CPSC1520
nav_order: 1
---

# Quick Reference

This page is a cheat sheet of the key pieces of JavaScript we've learned so far.

> **Tip**: Use Ctrl-F (or Command-F on a Mac) to search for specific words on this page.

## Intro to JavaScript
### Variables
- `let` creates a variable. e.g. `let stringVariable = "text123"`.
- `const` should be used instead if we know the contents shouldn't change.
- Variables that reference an HTML element can be created a few different ways:

  Function  | parameter      | used for  | returns
  ---                                       | ---             | ---       | ---
  `getElementByID()`          | name of the ID | IDs       | a single element
  `getElementsByClassName()`  | name of the class     | classes   | all elements that match
  `getElementsByTagName()`    | tag (e.g. `h2`) | tags      | all elements that match
  `querySelector()`                | tag, class name (including the `.`), or ID (including the `#`) | all of the above | the **first** element that matches
  `querySelectorAll()`             | tag, class name (including the `.`), or ID (including the `#`) | all of the above | all elements that match

  - e.g. `document.querySelector("#about")` is targeting the same element as `document.getElementByID("about")`.
  - e.g. `document.querySelector(".menu")` is targeting the first element targeted by `document.getElementsByClassName("menu")`.
  - e.g. `document.querySelector("h2")` is targeting the first element targeted by `document.getElementsByTagName("h2")`.

### Built-in Functions & Properties
- `console.log()` prints to the console, and is used primarily for debugging.
- `.innerHTML` lets us view and edit the entire HTML contents of a specific element. e.g. `elementX.innerHTML = "<p>hello</p>"`
- `.innerText` is similar, but it doesn't include the HTML tags. e.g. `elementX.innerText = "hello"`
- We can target styles using the `style` property: e.g. `elementName.style.color = 'blue'`.



## Functions & Events
### Functions
- `prompt()`: built-in function to prompt user for input.
- `alert()`: built-in function to create a pop-up message.
- Creating your own functions:
  - As a function expression:
    ```js
    const functionNameHere = function(paramNameHere) {
      // code to do stuff
    }
    ```
  - Using a function statement:
    ```js
    function functionNameHere(paramNameHere) {
      // code to do stuff
    }
    ```
  - As an arrow function:
    ```js
    const functionNameHere = (paramNameHere) => {
      // code to do stuff
    }
    ```
  - As an IIFE:
    ```js
    (function () {
      // code to do stuff
    })();
    ```

### Data Types
- There are a few ways to convert text to numbers:
  - `Number()`: converts an entire string, including `null` values.
  - `parseInt()`: converts until it hits a non-numeric value. e.g. `12px` becomes `12`.
- All values are truthy or falsy.
  - **Falsy** values are: `false`, `0`, empty strings, `null`, `undefined`, and `NaN`.
  - Everything else is **truthy**.
- Strings can be concatenated with variables in a few different ways.
  - `"Hello, " + userName + "."`
  - `` `Hello, ${userName}.` ``


### Events
- To add an event listener to an element named `bob`:
  - `bob.addEventListener(eventType, functionName)` where `eventType` is something like `"click"` or `"submit"`, and `functionName` is a previously defined function.
  - If the function wasn't previously defined, replace `functionName` with this syntax:
    ```js
    (paramNameHere) => {
        // code to do stuff
    }
    ```
- If our function has `event` as a param, we can do access methods and properties within the `event` object. e.g.
  - `event.stopPropagation()`
  - `event.preventDefault()`
- Classes can be added using `.classList.add()` and removed with `.classList.remove()`.

### Forms
- Assuming `form` is a variable that refers to a form element in our HTML document, and if the first field in the form is called `bob`, this is how we can access that specific field:
  - `form.elements.bob`
  - `form.elements["bob"]`
  - `form.elements[0]`
  - `document.querySelector("input[name=bob]")`
- Then, we can add `.value` to access the value entered into that field!
- We can **focus** on a specific element with `.focus()`.
  - We can target a focussed element using `document.activeElement.tagName`.


## Decisions
- Conditional operators include:
  - `<`, `<=`, `>`, `>=`, `==`, `!=`, `===`, `!==`
- Logical operators include:
  - `&&`, `||`, `!`
- Unary operators include:
  - `++`, `--`, `typeof`
- `if` statement syntax:
  ```js
  if (someCondition) {
    // do something
  } else if (someOtherCondition) {
    // do another thing
  } else {
    // default thing
  }
  ```
- `switch` statement syntax:
  ```js
  switch (valueOrExpressionToCompare) {
    case value1:
      // do stuff;
      break;
    case value2:
      // do different stuff
      break;

    // other cases
    
    default:
      // if nothing else matches
    }
  ```

## Loops & Arrays
### Arrays
- Arrays can be created with the following syntax:
  ```js
  let cats = ["Lily", "Aïoli", "Spruce"];
  ```
- Individual elements can be accessed with square brackets. e.g. `cats[1]` refers to the element at index `1`.
- Built-in array methods include:

  Name | Parameter | Description
  -- | -- | --
  `length` | | returns largest index + 1
  `indexOf(x)` | element to find | returns index of that element
  `push(x)` | new element | adds element to end
  `unshift(x)` | new element | adds element to start
  `pop()` | | removes last element
  `shift()` | | removes 0th element
  `slice(start, end)` | indexes | copies an array
  `includes` | element to find | returns true if that element is in the array
  `map()` | `function`(element, index, array) | creates a new array after a specified transformation
  `filter()` | `function`(element, index, array) |  filters an array based on a specified condition
  `reduce()` | `function`(accumulator, value, index, array), initial value | reduces the array into a single value.

### Loops
- `while` loops:
  ```js
  while (someCondition) {
    // do things
  }
  ```
- `do while` loops:
  ```js
  do {
    // do things
  }
  while (someCondition);
  ```
- `for` loops:
  ```js
  for (initialize; condition; increment) {
    // do things
  }
  ```
- `for`/`of` loops:
  ```js
  for (let kitten of cats) { 
    // kitten is a variable we name here that represents each element
    // cats is a collection that already exists
    // do things
  }
  ```
- `forEach()`:
  ```js
  myArray.forEach( 
    (element) => { // we can pass in element, index, and array
      // do things
    }
  );
  ```
- `break` statements exit the loop.
- `continue` skips to the next iteration.

## Objects
Coming soon!

## Fetch
Coming soon!

## DOM API & Timers
Coming soon!

## NPM, Tools, ES
Coming soon!

## Class/Object Prototypes
Coming soon!