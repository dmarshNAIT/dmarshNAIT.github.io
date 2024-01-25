---
layout: page
title: CPSC 1520
permalink: /cpsc1520/QuickReference
---

# Quick Reference

This page is meant to be a cheat sheet of the key pieces of JavaScript we've learned so far.

> **Tip**: Use Ctrl-F (or Command-F on a Mac) to search for specific words on this page.

## Intro to JavaScript
- Variables are created using `let`. e.g. `let stringVariable = "text123"`.
  - If we know the contents shouldn't change, we'll use `const` instead of `let`.
- We can print to the console using `console.log()`.
- We can create a variable that references an HTML element using a few different functions.
  - By **ID**: we use `document.getElementByID("xyz")` where `xyz` is the name of the ID. Since we aren't reusing IDs within a page, this returns a single element.
  - By **class**: we use `document.getElementsByClassName("xyz")` where `xyz` is the class name. As multiple elements may have the same class applied, this returns all the elements that match, and we will use the `[]` syntax to access specific elements. e.g. `elementName[0]` would refer to the first element, etc.
  - By **tag**: we use `document.getElementsByTagName("xyz")` where `xyz` is the tag (like `p` or `h2`). Since we may have many elements of the same, this returns all the elements that match, and we will use the `[]` syntax here too.
  - By **ID**, **class**, or **tag**: use `querySelector()` or `querySelectorAll()`. Make sure to include `#` before ID names and `.` before class names. `queryselector` will return the **first** element that matches, and `querySelectorAll` will return all the elements that match.
- `innerHTML` lets us view and edit the contents of a specific element. e.g. `elementX.innerHTML = "<p>hello</p>"`
- `innerText` is similar, but it doesn't include the HTML tags. e.g. `elementX.innerHTML = "hello"`
- We can target styles using the `style` property: e.g. `elementName.style.color = 'blue'`.

## Functions & Events
- `prompt()`: built-in function to prompt user for input.
- `alert()`: built-in function to create a pop-up message.
- There are a few different way to create a function.
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
- There are a few ways to convert text to numbers:
  - `Number()`: converts an entire string, including `null` values.
  - `parseInt()`: converts until it hits a non-numeric value.
- All values are truthy or falsy.
  - **Falsy** values are: false, 0, empty strings, null, undefined, and NaN.
  - Everything else is **truthy**.
- Strings can be concatenated with variables in a few different ways.
  - `"Hello, " + userName + "."`
  - `` `Hello, ${userName}.` ``
- To add an event listener to an element named `bob`:
  - `bob.addEventListener(eventType, functionName)` where `eventType` is something like `"click"` or `"submit"`, and `functionName` is a previously defined function.
  - & if the function wasn't previously defined, replace `functionName` with this syntax:
    ```js
    (paramNameHere) => {
        // code to do stuff
    }
    ```
- If our function has `event` as a param, we can do:
  - `event.stopPropagation()`
  - `event.preventDefault()`

### Forms
- Assuming `form` refers to a form element in our HTML document, and if the first field in the form is called `bob`, this is how we can access that specific field:
  - `form.elements.bob`
  - `form.elements["bob"]`
  - `form.elements[0]`
  - `document.querySelector("input[name=bob]")`
- Then, we can add `.value` to access the value entered into that field!
- We can **focus** on a specific element with `focus()`.
  - We can target a focussed element using `document.activeElement.tagName`.



## Decisions
Coming soon!

## Loops & Arrays
Coming soon!

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