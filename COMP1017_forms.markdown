---
layout: page
title: Forms
permalink: /comp1017/forms
---

## Forms
Most websites have some type of form: search, login, email subscriptions, etc.

### HTML
All forms start with the `<form>` element, which has 2 attributes:
`action` which tells the browser where the submitted data will go, and `method` which tells the browser **how** the submitted data will be sent (`GET` or `POST`).

Within form, we can have a bunch of elements: `input`, `textarea`, `label`, `button`, and [more](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Forms)!

Here's an example of a form with 3 input 

```html
<form id="contact-form">
<!-- the id is optional but lets me link to this form directly from another location, using an anchor tag-->
    <div class="user-name">
    <!-- adding this div will help us to easily target this input in our CSS, and we **always** add a class to divs so that we can target a specific div in our CSS. -->
        <label for="firstname">Your Name:</label>
        <!-- the "for" tag connects this label to the thing that it's labelling, using the id field. in other words, the value of "for" must match the value of the "id" for the related input or textarea -->
        <input id="firstname"  type="text"> 
        <!-- see below for more on the type attribute -->
    </div>
    <div class="user-phone">
        <label for="phonenumber">Your Phone Number:</label>
        <input id="phonenumber"  type="tel"> 
    </div>
    <div class="user-password">
        <label for="pw">Your Password:</label>
        <input id="pw"  type="password"> 
    </div>
    <div class="user-feedback">
        <label for="user-message">Your Feedback:</label>
        <textarea id="user-message"></textarea>
    </div>
    <div class="button">
        <button type="submit">ok</button>
    </div>
</form>
```
This is how it would look:
<html>
    <form id="contact-form">
        <div class="user-name">
            <label for="firstname">Your Name:</label>
            <input id="firstname"  type="text"> 
        </div>
        <div class="user-phone">
            <label for="phonenumber">Your Phone Number:</label>
            <input id="phonenumber"  type="tel"> 
        </div>
        <div class="user-password">
            <label for="pw">Your Password:</label>
            <input id="pw"  type="password"> 
        </div>
        <div class="user-feedback">
            <label for="user-message">Your Feedback:</label>
            <textarea id="user-message"></textarea>
        </div>
        <div class="button">
            <button type="submit">ok</button>
        </div>
    </form>
</html>
Then, we'd use CSS to style it.


#### HTML Attributes

Some elements have a `type` attribute which controls the input field behaviour. For example, `input` can have a `type` of `email` or `tel` or just regular `text` (amongst many other values), and the `button` can have a type of `submit` or `reset`. A list of all the types is available [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) and more info on them is available [here](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types).

The `ID` attribute lets us hook up the element with JavaScript and CSS. 

The `name` attribute will be used as a variable name, which will be out of scope for COMP 1017.

There are a few other attributes, including `value`, `placeholder`, `disabled`, and `required`. More on those [here](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls).

### CSS
We can target our form elements using classes, and descendant selectors, as well as something new: using the value of an attribute. If I wanted to target all the inputs where the `type` is `text`, I could use this declaration:

```css
input[type=text] {
    /** CSS goes here **/
}
```