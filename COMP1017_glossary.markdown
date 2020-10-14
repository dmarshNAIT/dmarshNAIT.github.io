---
layout: page
title: Glossary
permalink: /comp1017/glossary
---

## C
+ In this snippet, `<h2>` and `<p>` are **children** of `<main>`:
    ```html
    <main>
        <h2>This is a heading.</h2>
        <p>And here’s a paragraph.</p>
    </main>
    ```

## P
+ A **parent container** is an element which contains another element. For example, in the following snippet, `<body>` is the parent container for all the content, and has **children** `<header>`, `<main>`, and `<footer>`:
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

## S
+ In this snippet, `<header>`, `<main>`, and `<footer>` are **siblings**:
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