---
layout: page
title: Pseudo-Class Selectors
permalink: /comp1017/pseudo-classes
parent: COMP1017
nav_order: 6
---

# Pseudo-classes

A [pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) is a special type of selector which lets us target an element based on its **state**.

It lets us do useful things like target an element only when we hover over it, or targeting only the first item in a list.

Pseudo-classes are made up of a `:` followed by the name of the class, and some pseudo-classes have additional information following the class name inside a pair of parentheses.

> 📒 These are different from "pseudo-elements", which have `::` (2 colons) in front of their name.

The following is far from an exhaustive list, but contains some that are especially useful in CSS and JavaScript.

## User action pseudo-classes
These are pseudo-classes that require some action from the user.

- `:hover` targets an element only when the mouse is hovering over it. 
- `:active` targets a link while it’s being activated (being clicked). 

## Location pseudo-classes
These pseudo-classes relate to links.

- `:visited` targets all links that have already been visited.
- `:link` targets all links that have not already been visited.

## Input pseudo-classes
These are used for selecting form elements.

- `:valid` selects items with valid input, e.g. an email field with a valid email address.
- `:invalid` selects items with invalid input, e.g. an email field with random text entered instead of a valid email address.

## Tree-Structural Pseudo-classes
These pseudo-classes are related to the location of an element within the document tree.

- `:first-child` targets the first element in a list of siblings.
- `:last-child` targets the last element in a list of siblings.
- `:nth-child()` selects a specific element from a list of siblings.
	- e.g. `:nth-child(even)` targets every 2nd element in a list of siblings.
	- e.g. `:nth-child(4)` targets the 4th sibling.
- `:nth-last-child()` selects a specific element from a list of siblings, but counting from the end.
- `:nth-of-type()` selects an element from a list of siblings, but without including elements of other types.
	- For example, maybe there is an element with both `p` and `div` children. If we were to target `p:nth-of-type(1)`, that would target the first paragraph in the list, even if it wasn't the first sibling.

## Functional
These pseudo-classes accept a list of selectors.

- `:not()` is used to target elements that are not in the list of selectors. 
	- e.g. `:not(p)` targets everything except paragraphs.








