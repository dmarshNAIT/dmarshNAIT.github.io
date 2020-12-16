---
layout: page
title: CSS Properties
permalink: /comp1017/css-properties
---

## Font Styling ##
Some properties we've used to style our text include:
+ `color` sets the colour of the font by name or hexcode.
+ `font` combines: `font-style font-variant font-weight font-size/line-height font-family`. For example:
    ```css
    h1 {
        font: normal 
        small-caps 700 48px/1 
        'Lato', sans-serif;
    }
    ```
+ `font-family` defines the font being applied to an element. We list multiple fonts separated by commas, so if the first font isn't available it uses the next, and so on.
+ `font-size` is the height of a font.
+ `font-stretch` can be `condensed`, `normal`, `expanded`, etc.
+ `font-style` can be `normal`, `italic` or `oblique`.
+ `font-variant` can be `normal` or `small-caps`.
+ `font-weight` sets the weight: `100`, `300`, `400`, `500`, `600`, `700`, `800`, `900`, `bold`, etc.
+ `letter-spacing` defines the spacing between each character.
+ `line-height` defines the amount of space above and below inline elements. This creates space that we need to account for when we measure our margins and padding: we need to more than just `font-size` to know how much space our text takes up! In Photoshop, *leading* measures the distance from the baseline of one line of text to the baseline of the next, and that translates to our `line-height` in CSS, which is the `font-size` *plus* a bit of space above and below the text. More about that [on this site.](https://dev.to/lampewebdev/css-line-height-jjp)
+ `list-style-type` can be set to `none` to remove bullets.
+ `text-align` defines whether the text is aligned to the `left` or `right` or `center`, etc.
+ `text-decoration` can have a value of `underline` or `none`, among [other options](https://www.w3schools.com/cssref/pr_text_text-decoration.asp).
+ `text-transform` can set the text to be `uppercase`.
+ `word-spacing` defines the spacing between each word.

## Images ##
+ `background-image` lets us use an image as our background.
+ `background-repeat` lets us repeat the background by setting a value of `repeat-x` or `repeat-y`, or not at all with `no-repeat`.

## Styling nav ##
+ We can set the `display` property to `none` to make the element invisible.
+ We target our pseudo-classes in the following order:
    + `a:link`
    + `a:visited`
    + `a:hover`
    + `a:active`
