---
layout: page
title: CSS
permalink: /comp1017/css
---


# CSS
**Cascading Style Sheets** are how we tell the browser how everything should look. 

They're a set of rules that we write to help with **layout** and **style**.

**Cascading** means that if there are multiple styles applied to an element, the **last rule applied** will be the one that's used.

Here's what a bit of CSS can look like:
```css
p {
    color: red;
}
``` 
This means: *in each paragraph, set the color to red (i.e. change the colour of the font).*

+ `p` is an example of a **selector**: the thing we want to change.
+ `color` is an example of a **property**: the type of style we want to change.
+ `red` is an example of a **value**: what we want to set that property to.
+ The combination of `property: value;` is called a declaration.
+ We can have 1 or more declarations per selector.

We can leave comments in CSS like this:
```css
/* This is a comment for humans */
```
This doesn't appear anywhere on the page, and is meant for people reading the source code.

## How to use CSS
We have 3 options: linking, embedding, or inline styles.
1. **Linking** is the recommended way. It's when we link to an external stylesheet, by including something like this in the `<head>` of our HTML document:
    ```html
    <link rel="stylesheet" href="css/styles.css">
    ```
    where `styles.css` contains the CSS for our site.
1. **Embedding** is the next-best way. That's when we add something like this to the `<head>` of our HTML document:
    ```html
    <style>
        p {
            color: red;
        }
    </style>
    ```
1. **In-line styles** is the worst way and we won't do it. If we did, it would look like:
    ```html
    <p style="color:red;">Don’t do this.</p>
    ```

## Types of Selectors
+ **Element selectors**. That's when we target `<p>` or `<body>` or any of the other HTML elements we've learned.

+ A **multiple element selector** is when we target multiple elements with the same declaration(s). For example, this will make both my 1st and 2nd level headings blue:
    ```css
    h1, h2 {
        color: blue;
    }
    ```
+ IDs. We won't be using them for CSS in this class, but they look like this: `#jumbotron`

+ **Class selectors** are selectors we make up. In CSS, they'll have a period in their name:
    ```css
    .container {
        margin: 0 auto;
    }
    ```
    And we refer to them in HTML using the `class` attribute:
    ```html
    <div class="container">...</div>
    ```
    If an element has multiple classes applied to it in HTML, they are separated by spaces:
    ```html
    <div class="class-one class-two">...</div>
    <!-- these are terrible class names btw -->
    ```
    Class names should be lowercase and use dashes or underscores if their name contains more than one word. Names should be meaningful.
+ I can also combine element and class selectors. This CSS:
    ```css
    p.red-text {
        font-size: 56px;
    }
    ```
    specifically targets paragraphs with the `red-text` class applied. No other paragraphs, and no other HTML elements with that class, will be affected by this declaration.

+ **Descendant selectors** are when we use an element's location in the DOM to target it. We write it with a space between each element:
    ```css
    header h2 {
        color: blue;
    }
    ```
    This will only target `<h2>` tags that are in the `<header>`.
+ A **descendant combinator** combines these ideas. This:
    ```css
     ul.my-things li {
        color: blue;
    }
    ```
    targets `<li>` that are in an `<ul>` but only if that `<ul>` has the `my-things` class applied to it. Let's look at HTML to see what will be targeted:
    ```html
    <ul class="my-things">
        <li>One</li> <!-- this will be blue -->
        <li>Two</li> <!-- this will be blue -->
    </ul>

    <ul>
        <li>One</li> <!-- this will not -->
        <li class="my-things">Two</li> <!--  this will not -->
    </ul>
    ```
+ **Pseudo-class selectors** target an element based on their current state. A few we've covered in class:
    + `a:hover` targets links when we mouse over them.
    + `a:visited` targets links that have already been visited.
    + `a:active` targets links while you are clicking them.
    + `a:link` targets links that have not yet been visited.
    + `:nth-child()` targets an element based on their position within their group of siblings.
        + `nth-child(7)` targets the 7th element
        + `li:nth-child(2)` targets the 2nd `<li>` in a list
        + `:nth-child(4n)` targets every 4th element
        + `tr:nth-child(odd)` targets odd rows of a table
        + Learn more on the [:nth-child() page](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child).

+ The **universal selector** selects *everything*. It's also the weakest selector with a specificity value of 0.

## Specificity
If rules applied to different elements contradict each other, which one wins?

The most **specific** rule wins. The specificity weighting depends on the kind of selector:

Selector | Example | Specificity of Example
-- | -- | --
Element | `p, h1, h2` | 1
Descendant | `ul li a` | 3
Class | `body.container-960px` | 11
Descendant Combinator | `ul.my-things li` | 12
ID | `#jumbotron` | 100
`!important` | `p { color: red !important; }` | 101

## The Box Model
Everything on our page is rendered as a box, with 4 parts:
1. The **content**
1. A **border**
1. Space between the content and the border, called **padding**
1. Space outside the border, called **margin**

We will need to make sure that the total width of all the content, `border`, `padding`, and `margin`s within our page add up to a total width of exactly 960px.

### Border
By default, has a `width` of 0. In addition to `width` we can also control its `style` and `color`.
```css
border-width: 2px;
border-style: dashed;
border-color: olive;
```
is the same as
```css
border: 2px dashed olive;
```

### Margin
This is how we move things around on our page.
We can control the `margin` on each side of the box individually:
```css
margin: 5px 10px 5px 10px; 
/* The order is top, right, bottom, left. */
/* If you don't specify left, it'll be the same as right. */
/* If you don't specify bottom, it'll be the same as top. */
/* If you don't specify right, it'll be the same as top. */
```

### Padding
This is how we increase the space inside an element.
Just like `margin` and `border`, we can control each side individually. The same 'round-the-clock rules apply.


## Display Properties
Every element has a default `display` property (e.g. `<div>` is `block`-level, `<span>` is `inline`). We can change that property with the following declarations in CSS:
```css
display: block;
```
or
```css
display: inline;
```

## Flexbox
The **CSS Flexible Box Layout Model** is a way to order, align, and lay out website content.

To get items to be in the same flexbox (i.e. on the same line) we apply this to their **parent**:
```css
  display: flex;
```
The parent becomes the **flex container** and the children become **flex items**.

There are a ton of other properties for Flexbox, but we'll only use one other in this course:
```css
flex-wrap: wrap;
```
Just like turning on word-wrap in a text editor means that lines will `wrap` onto the next line if there isn't room for them, turning on `flex-wrap` lets items in the same `flex` container `wrap` onto the next line.