---
layout: page
title: HTML
permalink: /comp1017/html
---


## The grammar of HTML
A basic template might look like this:
```html
<!DOCTYPE HTML>
<html>
	<head>
		<title></title>
	</head>
	<body>
		<header></header>
		<main></main>
		<footer></footer>
	</body>
</html>
```

+ `<!DOCTYPE HTML>` is a declaration that tells your browser that the following is in HTML.
+ The `<head>` tag contains instructions for your browser (like which fonts your browser should use), but nothing the user actually sees on your page.
+ The `<body>` tag is where the actual content goes. This is what the user will see.
+ We can add comments into HTML like this:
	```html
	<!-- this is a comment for humans -->
	```
	This will not appear on the rendered page but can be viewed in the source code.

## HTML Tags
Tags are how we mark up content. They usually come in pairs. They can also contain [**attributes**](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes). The format looks like:
```html
<element attribute="value">
	Content goes here! 
</element>
```

### Block-level elements
Block level elements start on a new line and take up the full width available. We can set their height and width in CSS. Some that we've learned about are:
+ The `<article>` tag is a sectioning element for content that would make sense all on its own: a blog post, news story, or, of course, an article.
+ The `<aside>` tag is a sectioning element for extra info that isn't the key content of a page: a glossary, related links, etc. An `<aside>` with a `<nav>` inside is generally how we'd mark up sidebar navigation.
+ The `<blockquote>` tag is how we mark up a quotation.
	```html
	<blockquote cite="en.wikipedia.org/wiki/Pee_Pee_Island">
		<p>Pee Pee Island is a small island located in the 
			province of Newfoundland and Labrador in the far 
			east of Canada. Shortly after the incorporation, 
			the name of the island was changed from "Pebble 
			Island" to its current name.</p>
	</blockquote>
	```
+ `<div>` is a non-semantic wrapper, and a generic container for any content you want to group together so that you can target it with CSS.
+ The `<figure>` tag is how we mark up images, diagrams, etc, and will have an `<img>` and a `<figcaption>` within. It will look like:
	```html
	<figure>
		<img src="img/chonkyboye.jpg" alt="hey it's Pikachu">
		<figcaption>
			fig. 1: chonk in its natural habitat
		</figcaption>
	</figure>
	```
+ The `<footer>` tag is a sectioning element. On a page, it contains repeated info like copyright or contact info, and is generally the same on every page of your site. There will be a max of one `<footer>` per section/article/body.
+ `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, and `<h6>` are headings. We'll only have one top-level heading (`<h1>`) per page.
+ The `<header>` tag is a sectioning element, and it contains introductory content (probably a heading) and if it's the page's `<header>`, could contain things like a logo and site nav, and will generally be the same across every page of your site. It could also be *inside* another sectioning element. For example, a `<header>` within an `<article>` might contain the headline and author name.
+ The `<main>` is a sectioning element, and the page's `<main>` contains content unique to that page. This is a crucial element for screen readers: they can skip to the important stuff right away.
+ `<nav>` is a sectioning element that wraps our site navigation. It might live in the `<header>` if it's main navigation, in `<main>` for sidebar links (*"more articles like this!"*) or in the `<footer>` for secondary nav.
+ `<ol>` lets us created ordered, or numbered, lists:
	```html
	<ol>
		<li>Item 1</li>
		<li>Item 2</li>
		<li>Item 3</li>
	</ol>
	```
	That code would render like this:
	1. Item 1
	1. Item 2
	1. Item 3
+ `<p>` is how we mark up a pararaph, or text:
	```html
	<p>This is the start of my paragraph. I don't have much 
	to say so I'm gonna type until I have a few lines.</p>
	```
+ The `<section>` tag is a sectioning element for generic grouping.
+ Tables are created using the `<table>` tag, which is then organized into a `<thead>`, `<tbody>`, and `<tfoot>`. Within each of those, data are organized into rows using `<tr>` and then within each row, cells: `<th>` for headings and `<td>` for data.  Altogether, that could look like:
	```html
	<table>
		<thead>
			<tr>
				<th>header 1</th>
				<th>header 2</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>lorem</td>
				<td>ipsum</td>
			</tr>
			<tr>
				<td>more</td>
				<td>words</td>
			</tr>
		</tbody>
		<tfoot>
			<tr>
				<td colspan= "2">extra special footer stuff</td>
			</tr>
		</tfoot>
	</table>
	```
	Which would render like:
	<html>
		<table>
		<thead>
			<tr>
				<th>header 1</th>
				<th>header 2</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>lorem</td>
				<td>ipsum</td>
			</tr>
			<tr>
				<td>more</td>
				<td>words</td>
			</tr>
		</tbody>
		<tfoot>
			<tr>
				<td colspan= "2">extra special footer stuff</td>
			</tr>
		</tfoot>
		</table>
	</html>

	*Note: **We only use tables for data, never for layout.***
+ `<ul>` lets us created unordered, or bullet, lists:
	```html
	<ul>
		<li>Item 1</li>
		<li>Item 2</li>
		<li>Item 3</li>
	</ul>
	```
	That code would render like this:
	+ Item 1
	+ Item 2
	+ Item 3

### In-line elements
Inline elements do not start a new line and only take up as much width as necessary (this means we can't set their height or width, and we don't have much control over their margins). Some we've learned are:
+ The anchor tag (`<a>`) is how we create links. This is what it looks like in HTML:
	```html
	<a href="https://www.instagram.com/maimee.the.chihuahua/">Maimee's page</a>
	```
	which would look like this on the page: [Maimee's page](https://www.instagram.com/maimee.the.chihuahua/).

	I could also use a **relative** URL and link to a page in my framework. That would look like:
	```html
	View my <a href="glosssary.html">glossary</a>
	```
	And would appear like: View my [glossary](./glossary).

	If the page we were linking to was in a subfolder, we'd use something like 
	```html
	View my <a href="articles/other-file.html">other page</a>
	```
	and if the page I was linking to was in a parent folder, it would look like 
	```html
	<a href="../index.html">Home</a>
	```
+ If you want to link to a part of a page (a **fragment**) you need to first identify where on the page you want to link to by adding an `id` attribute:
	```html
	<h2 id="contact-us">Contact Us Info</h2>
	<p>PO Box 123, MyTown, AB T0A 1A1</p>
	```
	and then use that `id` in your link:
	```html
	<a href="#contact-us">contact us</a> 
	<!-- this only works within the same page -->
	```
	or
	```html
	<a href="index.html#contact-us">contact us</a>
	<!-- this is how we could link to a fragment on index.html from another page>
	```
+ The `<img>` tag is how we place pictures or logos on our page:
	```html
	<img src="img/cats.png" alt="image of two cats sitting on a bench">
	```
	*Note: the `alt` text should sufficiently describe the photo to anyone who cannot view it.*
+ `<em>` is what makes text appear in *italics*. We'll use this sparingly because HTML is meant for content and CSS is where we style.
+ `<span>` is a non-semantic wrapper, and a generic container for any content you want to group together so that you can target it with CSS. It's like `<div>` except it doesn't create a new row.
+ `<strong>` is what makes text appear **bold**. We'll use this sparingly because HTML is meant for content and CSS is where we style.