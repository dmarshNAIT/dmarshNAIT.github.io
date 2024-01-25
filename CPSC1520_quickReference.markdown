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
- We can print to the console using `console.log()`.
- We can create a variable that references an HTML element using a few different functions.
  - By **ID**: we use `document.getElementByID("xyz")` where `xyz` is the name of the ID. Since we aren't reusing IDs within a page, this returns a single element.
  - By **class**: we use `document.getElementsByClassName("xyz")` where `xyz` is the class name. As multiple elements may have the same class applied, this returns all the elements that match, and we will use the `[]` syntax to access specific elements. e.g. `elementName[0]` would refer to the first element, etc.
  - By **tag**: we use `document.getElementsByTagName("xyz")` where `xyz` is the tag (like `p` or `h2`). Since we may have many elements of the same, this returns all the elements that match, and we will use the `[]` syntax here too.
  - By **ID**, **class**, or **tag**: use `querySelector()` or `querySelectorAll()`. Make sure to include `#` before ID names and `.` before class names. `queryselector` will return the **first** element that matches, and `querySelectorAll` will return all the elements that match.
- `innerHTML` lets us view and edit the contents of a specific element. e.g. `elementX.innerHTML = "<p>hello</p>"`
- We can target styles using the `style` property: e.g. `elementName.style.color = 'blue'`.

## Functions & Events
Coming soon!

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