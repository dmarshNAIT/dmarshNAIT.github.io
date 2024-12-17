---
layout: page
title: Glossary
permalink: /comp1017/glossary
parent: COMP1017
nav_order: 1
---

## C
+ **Children**, also called **child elements**, are elements that are inside of another element. For example, in this snippet, `<h2>` and `<p>` are both **children** of `<main>`, as they are directly inside of the `<main>` tag:
    ```html
    <main>
        <h2>This is a heading.</h2>
        <p>And here’s a paragraph.</p>
    </main>
    ```
+ A **client** is an internet-connected device and its web-accessing software, such as Google Chrome or FileZilla.

## D
+ The **DOM** is the Document Object Model and is how your browser interprets and renders any HTML document. It represents the structure of your webpage.
+ **Dynamic pages** use code to pull content from servers or databases. For example, YouTube isn't getting re-coded every time we view the page, but it will look different each time we hit the refresh button. This is because back-end languages (like PHP, Python, or others) are doing something behind the scenes to update the page.

## F
+ The **framework** we're using in this course is a folder with the following contents:
	+ a file named *index.html* which is the homepage of your site
	+ a folder named *css* which will contain our stylesheets
	+ a folder named *img* which will contain pictures and images
	+ a folder named *js* which would contain JavaScript files (which are out of scope for COMP 1017)
	+ optionally, additional files and folders, all semantically named with no spaces or uppercase letters in their names
+ **FTP** stands for *File Transfer Protocol* and is a way to transfer files over the web. In our case, we use FTP to put our files on a web server.
+ The **front end** is the client-side: it's what the user sees. Some common front-end languages are HTML, CSS, and JS.

## H
+ **HTML** is HyperText Markup Language. It's the standard language for structuring web pages. It labels the content so that your browser knows what to do with it. It is made up of tags, which are written with angled brackets (<>), and most tags come in pairs. Check out the [HTML page](./html) for more info.
	```html
	<h1>This tag describes a heading.</h1>
	<p>This tag is for paragraphs.</p>
	```

## I
+ **Inheritance** in CSS means that many property values applied to an element will also be applied to its children.


## P
+ A **parent**, also called a **parent container** or **parent element**, is an element which contains another element. 
	- For example, in the following snippet, `<body>` is the parent container for all the content, and has **children** `<header>`, `<main>`, and `<footer>`. 
	- Another parent element in this example is `<main>`, which contains its own children, `<h2>` and `<p>`.
		```html
		<body>
			<header>...</header>
			<main>
				<h2>This is a heading.</h2>
				<p>And here’s a paragraph.</p>
			</main>
			<footer>...</footer>
		</body>
		```

## R
+ **Reset code** is code meant to reduce inconsistencies between different browsers. We link to it *before* our site-specific CSS.

## S
+ **Sectioning elements** group related content together. Generally they consist of a heading and some supporting content. The sectioning elements are: 
	+ `<header>`
	+ `<main>`
	+ `<footer>`
	+ `<article>`
	+ `<aside>`
	+ `<nav>`
	+ `<section>`
	
	Check out the [HTML page](./html) to learn about each.
+ We use **selectors** in CSS to target the thing we want to style: whether that's a class, a type of HTML element, or something else. Check out the [CSS page](./css) for examples of selectors.
+ A web **server** is a computer that holds directories of code (which is all websites are, really) and sends those files whenever someone makes a valid request.
+ **Siblings** are elements which share a direct parent. 
	- In this snippet, `<header>`, `<main>`, and `<footer>` are **siblings**, as they are all children of `<body>`. 
	- `<h2>` and `<p>` are another set of siblings, as they share the parent `<main>`:
		```html
		<body>
			<header>...</header>
			<main>
				<h2>This is a heading.</h2>
				<p>And here’s a paragraph.</p>
			</main>
			<footer>...</footer>
		</body>
		```
+ **Static pages** are changes that do not change unless we go in and change the code. They look the same every time we view them.

## W
+ **Web standards** are standards to promote consistency in code and design. This enables the web to be *accessible*, *indexable*, and *compatible*.