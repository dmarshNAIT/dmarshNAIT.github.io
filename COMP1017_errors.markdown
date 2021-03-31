---
layout: page
title: Common Errors
permalink: /comp1017/errors
---

This is not an exhaustive list, but some common problems I've seen (AKA, things you may lose marks for).
+ wrong URL (the name of your folder defines your URL)
+ errors in HTML or CSS validation
+ a Document Outline that has untitled sections or a weird structure
+ HTML or CSS isn't formatted

## HTML
+ more than one `<h1>` on a page
+ content outside of a sectioning element
+ page content in `<head>`
+ using discouraged tags like `<br>`
+ broken links or images

## CSS
+ unnecessarily complex (extra classes, redundant declarations, etc)
+ poorly named classes (or typos in class names)
+ missing fixed-width container

## Framework
+ files/folders with uppercase characters, spaces, or any punctuation other than a dash or an underscore
+ non-semantic names
+ missing a required component:
    + an HTML doc named **index.html**
    + a folder called **img** that contains all the image and logo files
    + a folder called **css** that contains the reset code and any site-specific code
    + a folder called **js**

## URL
+ missing **index.html** in the root of your folder
+ the folder in public_html is not named exactly the same as the last part of the URL you're trying (e.g. if I'm trying to access dmarsh.dmitstudent.ca/my-page, my folder needs to be named exactly **my-page**)