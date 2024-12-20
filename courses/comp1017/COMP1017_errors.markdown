---
layout: page
title: Common Errors
permalink: /comp1017/errors
parent: COMP1017
nav_order: 5
---

# Common Web Development Errors

This is not an exhaustive list, but some common problems I've seen in student submissions. 

These are errors that can reduce the quality of your code, and lower your page's readability and maintainability.


## HTML Errors
+ 🚨 errors in [HTML validation](https://validator.w3.org/) 
+ 🎋 a [Document Outline](https://gsnedders.html5.org/outliner/) that has untitled sections or a weird structure
+ 📰 HTML isn't [formatted](https://prettier.io/) following best standards
+ 🤯 more than one `<h1>` on a page
+ 🛟 content outside of a sectioning element
+ 🔤 page content in `<head>`
+ 🚫 using discouraged tags like `<br>`
+ 🖼️ a page has broken links or images

## CSS Errors
+ 🚨 errors in [CSS](https://jigsaw.w3.org/css-validator/) validation
+ 📰 CSS isn't [formatted](https://prettier.io/) following best standards
+ 🕸️ unnecessarily complex CSS (e.g. extra classes, redundant declarations, etc)
+ 🔤 poorly named classes (or typos in class names)
+ 📦 missing fixed-width container

## Framework Errors
+ ⁉️ files/folders with uppercase characters, spaces, or any punctuation other than a dash or an underscore
+ 🔤 non-semantic names
+ ❎ missing a required component:
    + ✅ an HTML doc named **index.html** in the root folder
    + ✅ a folder called **img** that contains all the image and logo files
    + ✅ a folder called **css** that contains the reset code and any site-specific code
    + ✅ a folder called **js**
+ 📁 the folder in public_html is not named exactly the same as the last part of the URL you're trying (e.g. if I'm trying to access `dmarsh.dmitstudent.ca/my-page`, my folder needs to be named exactly **`my-page`**)
