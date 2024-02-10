---
layout: page
title: HTML
permalink: /comp1017/html
---

> Hint: Use Ctrl-F (or Cmd-F on a Mac) to search for content on this page.

# Module 1

## The grammar of HTML
- A basic web page **template** might look like this:
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

	+ `<!DOCTYPE HTML>` is a **declaration** that tells your browser that the following is in HTML.
	+ The `<head>` tag contains **instructions** for your browser (like which fonts your browser should use), but nothing the user actually sees on your page.
	+ The `<body>` tag is where the actual **content** goes. This is what the user will see.
+ We can add **comments** into HTML like this:
	```html
	<!-- this is a comment for humans -->
	```
	This will not appear on the rendered page but can be viewed in the source code by other humans.


## HTML Tags
- Tags are how we mark up content, by defining what **type** of content they contain. 
	- For example, there is a tag that represents a photo, another that represents a link, yet another that represents regular text, and so on.
- Tags usually come in **pairs**, with one tag to mark the start of the content and another to mark the end of the content. 
- Tags can also contain [**attributes**](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes).
- Altogether, the format looks something like:
	```html
	<elementType attribute1Name="someValue" attribute2Name="anotherValue">
		Content goes here! 
	</elementType>
	```

## HTML elements
HTML elements generally fall into 2 categories, **block-level** and **inline** elements. Let's take a look at examples of each.

### Block-level elements
**Block level elements** start on a new line and take up the full width available. We can set their **height** and **width** using CSS.

Here are some block-level elements we'll be using in COMP 1017:
- The following are examples of **sectioning elements**. All of the content on our page will be in a sectioning element.
	+ The `<header>` tag contains **introductory content** (probably a heading) and if it's the page's `<header>`, could contain things like a logo and site nav, and will generally be the same across every page of your site. It could also be *inside* another sectioning element. For example, a `<header>` within an `<article>` might contain the headline and author name.
	+ The `<main>` element contains, well, the **main content**, and the page's `<main>` contains content unique to that page. This is a crucial element for screen readers: they can skip to the important stuff right away.
	+ The `<footer>` tag generally contains **repeated info** like copyright or contact info, and is usually the same on every page of your site. There will be a max of one `<footer>` per section/article/body.
	+ The `<article>` tag is a sectioning element for content that would make sense all on its own: e.g. a **blog post**, **news story**, or, of course, an **article**.
	+ The `<aside>` tag is a sectioning element for **extra info** that isn't the key content of a page: a glossary, related links, etc. An `<aside>` with a `<nav>` inside is generally how we'd mark up **sidebar** navigation.
	+ `<nav>` is a sectioning element that wraps our site navigation. It might live in the `<header>` if it's main navigation, in `<main>` for sidebar links (e.g. *"more articles like this!"*) or in the `<footer>` for secondary nav.
	+ The `<section>` tag is a sectioning element for generic grouping. Basically, if we want to group content but none of the previous options fit.
- The following are examples of elements that can contain **text**:
	+ `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, and `<h6>` are **headings**. We'll only have one top-level heading (`<h1>`) per page.
	+ The `<blockquote>` tag is how we mark up a **quotation**.
		```html
		<blockquote cite="en.wikipedia.org/wiki/Pee_Pee_Island">
			<p>Pee Pee Island is a small island located in the 
				province of Newfoundland and Labrador in the far 
				east of Canada. Shortly after the incorporation, 
				the name of the island was changed from "Pebble 
				Island" to its current name.</p>
		</blockquote>
		```
	+ `<p>` is how we mark up a **pararaph**, or **text**:
		```html
		<p>This is the start of my paragraph. I don't have much 
		to say so I'm gonna type until I have a few lines.</p>
		```
	+ `<ol>` lets us created **ordered**, or numbered, **lists**:
		```html
		<ol>
			<li>Item 1</li>
			<li>Item 2</li>
			<li>Item 3</li>
		</ol>
		```
		which would render a list like this:

		<html>
		<style type="text/css" media="screen">
			ol {
				margin: 0 0 1rem 2rem;
				border: 1px solid grey;
				box-shadow: 0 2px 5px 0;
				width: 20%;
			}
		</style>
		<ol>
			<li>Item 1</li>
			<li>Item 2</li>
			<li>Item 3</li>
		</ol>
		</html>
	+ `<ul>` lets us created unordered, or bullet, lists:
		```html
		<ul>
			<li>Item 1</li>
			<li>Item 2</li>
			<li>Item 3</li>
		</ul>
		```
		That code would render a list that looks like this:

		<html>
		<style type="text/css" media="screen">
			ul.fake-list {
				margin: 0 0 1rem 2rem;
				border: 1px solid grey;
				box-shadow: 0 2px 5px 0;
				width: 20%;
			}
		</style>
		<ul class="fake-list">
			<li>Item 1</li>
			<li>Item 2</li>
			<li>Item 3</li>
		</ul>
		</html>

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
			<style>
				table {border: 1px solid grey; box-shadow: 0 2px 5px 0 ;}
			</style>
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

	> Note: **We only use tables for data, never for layout.***
- Finally, a few other elements whose jobs revolve around **containing** other elements.
	+ The `<figure>` tag is how we mark up content that needs a **caption**, like diagrams, and will contain an `<img>` and a `<figcaption>` attribute. It will look like:
		```html
		<figure>
			<img src="img/aioli.jpg" alt="a picture of a grey kitten">
			<figcaption>
				fig. 1: Aïoli the kitten
			</figcaption>
		</figure>
		```
	+ `<div>` is a non-semantic wrapper, and a **generic container** for any content you want to group together so that you can target it with CSS. 
	> It is strongly recommended to add classes to each `div` so they can be easily targeted by your CSS.

### In-line elements
**Inline elements** do not start a new line and only take up as much width as necessary (this means we can't set their height or width, and we don't have much control over their margins). Some we'll use in COMP 1017 are:

+ The `<img>` tag is how we place **pictures** or **logos** on our page:
	```html
	<img src="img/cats.png" alt="image of two cats sitting on a bench">
	```
	> Note: the `alt` text should sufficiently describe the photo to anyone who cannot view it.*

+ `<em>` is what makes text appear in *italics*. We'll use this sparingly because HTML is meant for content and CSS is where we style.
+ `<strong>` is what makes text appear **bold**. We'll use this sparingly because HTML is meant for content and CSS is where we style.
+ `<span>` is a non-semantic wrapper, and a **generic container** for any content you want to group together so that you can target it with CSS. It's like `<div>` except it doesn't create a new row.

+ The anchor tag (`<a>`) is how we create links. This is what it looks like in HTML:
	```html
	<a href="https://www.instagram.com/maimee.the.chihuahua/">Maimee's page</a>
	```
	which would look like this on the page: 
	<html>
		<style type="text/css" media="screen">
		a.fake-link {
			display: block;
			margin: 1rem;
			padding: 1rem;
			border: 1px solid grey;
			box-shadow: 0 2px 5px 0;
			width: 25%;
		}
	</style>
		<a href="https://www.instagram.com/maimee.the.chihuahua/" class="fake-link">Maimee's page</a>
	</html>

	+ Instead of a full URL, we could use a **relative** link. That means we are giving directions relative to the current page. In other words, how do we get from the current location, to our destination, using our framework?
		- Linking to a **file** in the **same folder**: `href="glossary.html"`
		- Linking to a page in a **sub-folder**: `href="articles/other-file.html"`
		- Linking to a page in the **parent folder**: `href="../other-page.html"`
		- Linking to a **specific location** on **this page**: `href="#contact-us"`, where `"contact-us"` is the value of an `id` attribute added to some element.
		- Linking to a **specific location** on **another page**: `href="other-page.html#contact-us"`, where `"contact-us"` is the value of an `id` attribute added to some element.

	+ As a bonus, we can set the `target` attribute so that the file opens in a **new tab** or window, which is a best practice when linking to non-HTML resources:
		```html
		<a href="cool-file.pdf" target="_blank">Click here for a PDF! </a>
		```
	+ We can also use anchor tags to launch **email** clients and create a new message:
		```html
		<a href="mailto:nowhere@gmail.com">Send an email to nowhere. </a>
		```








# Module 4
## Form Elements
- Most websites have some type of form: search, login, email subscriptions, etc.

- All forms start with the `<form>` element, which has 2 attributes:
`action` which tells the browser where the submitted data will go, and `method` which tells the browser **how** the submitted data will be sent (e.g. `GET` or `POST`).

- Within `form`, we can have a bunch of elements: `input`, `textarea`, `label`, `button`, and [more](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Forms)!

- Here's an example of a form with 3 `input` elements, a `textarea`, and a `button`:

	```html
	<!-- adding ID makes it easier to link directly to the form -->
	<form id="contact-form">

		<!-- adding a class helps us more easily target this field -->
		<div class="user-name">
			<label for="firstname">Your Name:</label>
			<input id="firstname"  type="text"> 
			<!-- see below for more on the for and type attributes -->
		</div>

		<div class="user-phone">
			<label for="phone-number">Your Phone Number:</label>
			<input id="phone-number"  type="tel"> 
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
    <style type="text/css" media="screen">
        form {
            margin: 1rem;
            padding: 1rem;
            border: 1px solid grey;
            box-shadow: 0 2px 5px 0;
            width: 400px;
        }
    </style>
    <form id="contact-form">
        <div class="user-name">
            <label for="firstname">Your Name:</label>
            <input id="firstname"  type="text"> 
        </div>
        <div class="user-phone">
            <label for="phone-number">Your Phone Number:</label>
            <input id="phone-number"  type="tel"> 
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


### Form Attributes
+ the `for` attributes connects a **label** to the element that it's labelling, using the other element's `id`. 
	+ In other words, the value of `for` must match the value of the `id` for the related `input` or `textarea`.

+ The `ID` attribute lets us hook up the element with JavaScript and CSS. 
	+ It needs to be **unique** within the page (in other words, you can't use the same `id` twice on the same page).

+ The `name` attribute will be used as a **variable** name, which will be out of scope for COMP 1017.

+ Some elements have a `type` attribute which controls the input **field behaviour**. 
	+ For example, `input` can have a `type` of `email` or `tel` or just regular `text` (amongst many other values), and the `button` can have a type of `submit` or `reset`. 
	+ A list of all the types is available [on MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) and more info on them is available [in this list](https://developer.mozilla.org/en-US/docs/Learn/Forms/HTML5_input_types).


+ There are a few **other** attributes, including `value`, `placeholder`, `disabled`, and `required`. More on those [on MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls).

