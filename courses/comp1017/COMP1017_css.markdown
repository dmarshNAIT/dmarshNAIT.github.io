---
layout: page
title: CSS
permalink: /comp1017/css
parent: COMP1017
nav_order: 3
---

# Module 1

**Cascading Style Sheets** are how we tell the browser how everything should look. 

They're a set of rules that we write to help with **layout** and **style**.

The word **cascading** means that if there are multiple styles applied to an element, the **last rule applied** will be the one that's used.

Here's what a snippet of CSS can look like:
```css
p {
    color: red;
}
``` 
This means: *in each paragraph, change the colour of the font to red.*

+ `p` is an example of a **selector**: the thing we want to change.
+ `color` is an example of a **property**: the type of style we want to change.
+ `red` is an example of a **value**: what we want to set that property to.
+ The combination of `property: value;` is called a **declaration**.
+ We can have multiple declarations per selector. In regular English: we can apply many rules to the same HTML element.

We can leave **comments** in CSS like this:
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
    where `styles.css` is a file which contains the CSS for our site.
1. **Embedding** is the next-best way. That's when we add something like this to the `<head>` of our HTML document:
    ```html
    <style>
        p {
            color: red;
        }
    </style>
    ```
    A downside of this approach is we then have to style every page separately, rather than having one file style all the pages on our website.
1. **In-line styles** is the worst way and we won't do it. If we did, it would look like:
    ```html
    <p style="color:red;">Don’t do this.</p>
    ```
    This approach leads to a mish-mash of HTML & CSS, and a lot of repeated declarations, meaning it's a LOT harder to read and maintain.

## Types of Selectors
+ **Element selectors**: That's when we target an element by name, like `<p>` or `<body>` or any of the other HTML elements we've learned.
    + For example, this turns the text in every `<p>` red:
        ```css
        p {
            color: red;
        }
        ``` 

+ A **multiple element selector** is when we target multiple elements so that we can give them all the same declaration(s). Elements must be separated by commas.
    + For example, this will make both my 1st and 2nd level headings blue:
        ```css
        h1, 
        h2 {
            color: blue;
        }
        ```
+ **IDs**: We won't be using them for CSS in this class, but they look like this: `#jumbotron`. 
    + The # symbol (called a number or pound or hash* symbol) is how CSS knows the text that follows is an ID.
        
        \* This is why social media tags are called hashtags: they're the combination of the hash symbol and a category tag.

+ **Class selectors** are selectors we make up. In CSS, they'll have a dot in their name:
    ```css
    .container {
        margin: 0 auto;
    }
    ```
    And we refer to them in HTML using the `class` attribute:
    ```html
    <div class="container">...</div>
    ```
    If an element has **multiple classes** applied to it in HTML, they are separated by spaces:
    ```html
    <div class="class-one class-two">...</div>
    <!-- these are terrible class names btw -->
    ```
    **Class names** should be lowercase and use dashes or underscores if their name contains more than one word. Names should be **meaningful**.
+ We can also **combine** element and class selectors. This CSS:
    ```css
    p.red-text {
        font-size: 56px;
    }
    ```
    specifically targets paragraphs with the `red-text` class applied. Other paragraphs, and  other HTML elements with the `red-text` class applied, will **not** be affected by this declaration.

+ **Descendant selectors** are when we use an element's location in the DOM to target it. We write it with a space between each element:
    ```css
    header h2 {
        color: blue;
    }
    ```
    This will only target `<h2>` tags that are **inside of** the `<header>`.
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
        <li class="my-things">Two</li> <!--  neither will this -->
    </ul>
    ```
+ **Pseudo-class selectors** target an element based on their current state. A few we've covered in class:
    + `a:hover` targets links when we **mouse over** them.
    + `a:visited` targets links that have **already been visited**.
    + `a:active` targets links ***while*** you are clicking them.
    + `a:link` targets links that have **not yet been visited**.
    + `:nth-child()` targets an element based on its **position** within its group of siblings. Some examples:
        + `nth-child(7)` targets the 7th element
        + `li:nth-child(2)` targets the 2nd `<li>` in a list
        + `:nth-child(4n)` targets every 4th element
        + `tr:nth-child(odd)` targets odd rows of a `<table>`
            + *Learn more on the [:nth-child() page](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child).*

+ The **universal selector** (`*`) selects *everything*. It's also the weakest selector with a specificity value of 0.

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

*Learn more with the [specificity calculator](https://specificity.keegan.st/).*

## The Box Model
Everything on our page is rendered as a box, with 4 parts:
1. The **content**
1. A **border**
1. Space *between* the content and the border, called **padding**
1. Space *outside* the border, called **margin**

[Learn more about the box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model) on MDN.

In COMP 1017, we are making fixed-width pages, so will need to make sure that the total width of all the **content**, `border`, `padding`, and `margin`s within our page add up to a total width of *exactly* 960px.

### Border
By default, all items have a border with a `width` of 0. In addition to `width` we can also control the border's `style` and `color`.
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
This is how we move things around on our page. Margin is the space **around** or **outside** of an element.
We can control the `margin` on each side of the box individually:
```css
margin: 5px 10px 5px 10px; 
/* The order is top, right, bottom, left... start at the top then go around clock-wise. */
/* If you don't specify left, it'll be the same as right. */
/* If you don't specify bottom, it'll be the same as top. */
/* If you don't specify right, it'll be the same as top. */
```
Sometimes adjacent elements will essentially "share" their margin. This is called **margin collapsing**, and means we can't always just add together margins to figure out how much space they take up. More on this phenomenon is available on [this page](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing).

### Padding
This is how we increase the space **inside** an element.
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
or
```css
display: inline-block;
```
This can be useful if we want to set the `height` and `width` of an element that is normally `inline`, or we want an element that is normally `block` to show up on the same line as another element: we can just change their `display` property! [More on this at MDN.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Block_and_Inline_Layout_in_Normal_Flow)


## Flexbox
The **CSS Flexible Box Layout Model** is a way to order, align, and lay out website content.

To get items to be in the same flexbox (i.e. on the same line) we apply this to their **parent**:
```css
  display: flex;
```
The parent becomes the **flex container** and the children become **flex items**.

There are a ton of other properties for Flexbox, but we'll only require one other in this course:
```css
flex-wrap: wrap;
```
Just like turning on word-wrap in a text editor means that lines will `wrap` onto the next line if there isn't room for them, adding `flex-wrap: wrap;` to a container lets items in that `flex` container `wrap` onto the next line.

**We'll only use `flex-wrap` on elements that are flex boxes.**

Some "bonus" content:
+ Adding `justify-content: center;` to a flex-container **centers** items along the *main* axis of the container. If your container contains items that are side-by-side, this means it *horizontally* centers them, rather than the left where they'd "normally" sit. For example:
    + Here's a `flex`-box containing 3 children. It isn't using `justify-content`:
        <html>
            <style>
                div.flex-demo { border: 1px solid black; padding: 0.25rem; }
            </style>
            <div style="display: flex;" class="flex-demo">
                <div class="flex-demo">child 1</div>
                <div class="flex-demo">child 2</div>
                <div class="flex-demo">child 3</div>
            </div>
        </html>
    + And here's the exact same example but with `justify-content: center;` applied to the parent:
        <html>
            <style>
                div.flex-demo { border: 1px solid black; padding: 0.25rem; }
            </style>
            <div style="display: flex; justify-content: center;" class="flex-demo">
                <div class="flex-demo">child 1</div>
                <div class="flex-demo">child 2</div>
                <div class="flex-demo">child 3</div>
            </div>
        </html>

+ Adding `align-items: center;` to a flex-container will **center** items along the *cross* axis of the container. If your items are side-by-side, this means it'll *vertically* center them, rather than putting them at the the top or bottom or stretching the full height. Let's add a bit of height to the previous example to see the difference:
    + Here's a `flex`-box containing 3 children. It isn't using `align-items` so by default each child stretches to fill the full height of the parent:
        <html>
            <style>
                div.flex-demo { border: 1px solid black; padding: 0.25rem;}
            </style>
            <div style="display: flex; height: 4rem;" class="flex-demo">
                <div class="flex-demo">child 1</div>
                <div class="flex-demo">child 2</div>
                <div class="flex-demo">child 3</div>
            </div>
        </html>
    + And then with `align-items: center;` applied to the parent:
        <html>
            <style>
                div.flex-demo { border: 1px solid black; padding: 0.25rem; }
            </style>
            <div style="display: flex; align-items: center; height: 4rem;" class="flex-demo">
                <div class="flex-demo">child 1</div>
                <div class="flex-demo">child 2</div>
                <div class="flex-demo">child 3</div>
            </div>
        </html>


+ There are helpful examples of both in this [complete guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

# Module 3

## Font Styling ##
Some properties we'll use to style our text include:

+ `color` sets the **colour** of the font by name or hexcode.
+ `font` combines: `font-style font-variant font-weight font-size/line-height font-family`. For example:
    ```css
    h1 {
        font: normal small-caps 700 48px/1 'Lato', sans-serif;
    }
    ```
    + `font-family` defines the **font** being applied to an element. We list multiple fonts separated by commas, so if the first font isn't available it uses the next, and so on.
    + `font-size` is the **height** of a font.
    + `font-style` can be `normal`, `italic` or `oblique`.
    + `font-variant` can be `normal` or `small-caps`.
    + `font-weight` sets the weight: `100`, `300`, `400`, `500`, `600`, `700`, `800`, `900`, `bold`, etc.
    + `line-height` defines the **amount of space** above and below inline elements. This creates space that we need to account for when we measure our margins and padding: we need to more than just `font-size` to know how much space our text takes up! In Photoshop, *leading* measures the distance from the baseline of one line of text to the baseline of the next, and that translates to our `line-height` in CSS, which is the `font-size` *plus* a bit of space above and below the text. More about that [on this site.](https://dev.to/lampewebdev/css-line-height-jjp)
+ `font-stretch` can be `condensed`, `normal`, `expanded`, etc.
+ `letter-spacing` defines the **spacing** between each character.
+ `list-style-type` can be set to `none` to remove **bullets**.
+ `text-align` defines whether the text is **aligned** to the `left` or `right` or `center`, etc.
+ `text-decoration` can have a value of `underline` or `none`, among [other options](https://www.w3schools.com/cssref/pr_text_text-decoration.asp).
+ `text-transform` can set the text to be `uppercase`.
+ `word-spacing` defines the **spacing** between each word.

## Images ##
+ `background-image` lets us use an image as our background.
    - e.g. `background-image: url("../img/name-icon.gif");`
+ `background-repeat` lets us repeat the background image by setting a value of `repeat-x` or `repeat-y`, or not at all with `no-repeat`.

## Styling nav ##
+ We can set the `display` property to `none` to make the element invisible.
+ We target our pseudo-classes in the following order:
    + `a:link`
    + `a:visited`
    + `a:hover`
    + `a:active`

# Module 4
## Styling Forms
We can target our form elements using classes, and descendant selectors, as well as something new: using the **value** of an **attribute**. e.g. If we wanted to target all the inputs where the `type` is `text`, I could use this declaration:

```css
input[type=text] {
    /** CSS goes here **/
}
```

Another useful trick is to define the size of a `textarea`:
```css
textarea {
    min-height: 200px;
    max-height: 200px;
    min-width: 150px;
    max-width: 150px;
}
```

