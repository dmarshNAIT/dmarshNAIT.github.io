---
layout: page
title: CPSC 1520 Quick Reference
permalink: /cpsc1520/QuickReference
parent: CPSC1520
nav_order: 1
---

# CPSC 1520 Quick Reference

This page is a cheat sheet of the **key pieces of JavaScript** we'll cover throughout this course. It is loosely **organized by topic** so the order will differ slightly from our class examples.

> 🔥 **Tip**: Use **Ctrl-F** (or **Command-F** on a Mac 🍎) to **search** for specific words on this page.



* TOC
{:toc}

> Items marked with ⭐ are more advanced or "bonus" content.

***

## Intro to JavaScript
### Variables
- `let` creates a variable. e.g. `let stringVariable = "text123"`.
- `const` should be used instead if we know the contents shouldn't change.

### HTML Elements
Variables that reference an HTML element can be created in a few different ways:

  Function  | parameter      | searches by | returns
  ---                                       | ---             | ---       | ---
  `getElementByID()`          | name of the ID | IDs       | a **single** element
  `getElementsByClassName()`  | name of the class     | classes   | **all** elements that match
  `getElementsByTagName()`    | tag (e.g. `h2`) | HTML tags      | **all** elements that match
  `querySelector()`                | tag, class name (including the `.`), or ID (including the `#`) | all of the above | the **first** element that matches
  `querySelectorAll()`             | tag, class name (including the `.`), or ID (including the `#`) | all of the above | **all** elements that match

  - e.g. `document.querySelector("#about")` is targeting the **same** element as `document.getElementByID("about")`.
  - e.g. `document.querySelector(".menu")` is targeting the **first** element targeted by `document.getElementsByClassName("menu")`.
  - e.g. `document.querySelector("h2")` is targeting the **first** element targeted by `document.getElementsByTagName("h2")`.

### Element Properties

- `.innerHTML` lets us view and edit the entire **HTML contents** of a specific element. 
  - e.g.
    ```js
    console.log(elementX.innerHTML);
    ```
    returns
    ```html
    <p>hello</p>
    ```
- `.innerText` is similar, but it **doesn't include the HTML tags**. 
  - e.g. 
    ```js
    console.log(elementX.innerText);
    ```
    returns
    ```html
    hello
    ```

- We can target **styles** using the `style` property: e.g. `elementName.style.color = 'blue'`.
- ⭐ We can access custom **data attributes** in JavaScript by using the `dataset` property.
  - In HTML, custom data attributes are named `data-xyz` where `xyz` is a descriptive name containing lowercase letters, numbers, and certain punctuation.
  - The corresponding name in JavaScript removes the `data-` prefix as well as any dashes (`-`), and converts the remaining letters to camelCase.
  - For example, in HTML we might have an attribute named `data-first-name`. In JavaScript, we access it by dropping `data-` and converting `first-name` to camelCase (`firstName`):
      ```js
      // let's assume we have a variable targeting an element:
      let customer = event.target;

      // now we can access any data attributes within that element:
      let customerName = customer.dataset.firstName;
      ```

***

## Functions
JavaScript has a number of built-in functions that we can use.
- `console.log()` **prints** to the **console**, and is used primarily for debugging.
- `prompt()`: built-in function to prompt user for **input**.
- `alert()`: built-in function to create a **pop-up message**.

### Defining Functions
More excitingly, we can also create our own custom functions! There are many different ways to do so:
  - As a **function expression**:
    ```js
    const functionNameHere = function(paramNameHere) {
      // code to do stuff
    }
    ```
  - Using a **function statement**:
    ```js
    function functionNameHere(paramNameHere) {
      // code to do stuff
    }
    ```
  - As an **arrow function**:
    ```js
    const functionNameHere = (paramNameHere) => {
      // code to do stuff
    }
    ```
  - As an **IIFE**:
    ```js
    (function () {
      // code to do stuff
    })();
    ```

*** 

## Data Types
While a few other data types exist in JavaScript, in this course we will mostly use `Number`, `String`, `Boolean`, and `Object` data types.
- There are a few ways to convert text to numbers:
  - `Number()`: converts an entire string, including `null` values.
  - `parseInt()`: converts until it hits a non-numeric value. e.g. `12px` becomes `12`.
  - Once we have a `Number`, we can use [some of the built-in `Math` functions and constants.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math).
- All values are truthy or falsy.
  - **Falsy** values are: `false`, `0`, empty strings, `null`, `undefined`, and `NaN`.
  - Everything else is **truthy**.
- Strings can be concatenated with variables in a few different ways.
  - When used with a `String`, the plus symbol (`+`) glues together strings and numbers: `'Hello, ' + userName + '.'`
  - Or, we can use **template strings** to do **string interpolation**. That's a fancy way of saying to use placeholders to represent strings of text. e.g. `` `Hello, ${userName}.` ``
    - Notice we aren't using the usual `'` symbol around our string for this to work, but instead we must surround the string with backticks (`` ` ``).

    Both of these examples have the same output: `Hello, dmarsh.`

***

## Events
- To add an **event listener** to an element named `bob`:
  - `bob.addEventListener(eventType, functionName)` where `eventType` is something like `'click'` or `'submit'`, and `functionName` is a previously defined function.
  - If the function wasn't previously defined, replace `functionName` with this syntax:
    ```js
    (paramNameHere) => {
        // code to do stuff
    }
    ```
- If our function has `event` as a **parameter**, we can access **functions and properties** within the `event` object. e.g.
  - `event.target` (a reference to the element where the event happened)
  - `event.stopPropagation()`
  - `event.preventDefault()`

- **Classes** can be **added** using `.classList.add()` and **removed** with `.classList.remove()`. We can also **check** whether a certain class has been applied to an element by using `.classList.contains()`.

***


## Forms
- Assuming `form` is a variable that refers to a form element in our HTML document, and if the first field in the form is called `bob`, this is how we can access that specific field:
  - `form.elements.bob`
  - `form.elements["bob"]`
  - `form.elements[0]`
  - `document.querySelector("input[name=bob]")`
- Then, we can use `.value` to access the **value** entered into that form field!
- We can **focus** on a specific element with `.focus()`.
  - We can target a focussed element using `document.activeElement.tagName`.

***

## Decisions
- **Conditional operators** include:
  - `<`, `<=`, `>`, `>=`, `==`, `!=`, `===`, `!==`
- **Logical operators** include:
  - `&&`, `||`, `!`
- **Unary operators** include:
  - `++`, `--`, `typeof`
- `if` statement syntax:
  ```js
  if (someCondition) {
    // do something
  } else if (someOtherCondition) {
    // do another thing
  } else {
    // default thing
  }
  ```
- `switch` statement syntax:
  ```js
  switch (valueOrExpressionToCompare) {
    case value1:
      // do stuff;
      break;
    case value2:
      // do different stuff
      break;

    // other cases
    
    default:
      // if nothing else matches
    }
  ```

***

## Arrays
- Arrays can be created with the following syntax:
  ```js
  let cats = ["Lily", "Aïoli", "Spruce"];
  ```
- Individual elements can be accessed with square brackets. 
  - e.g. `cats[1]` refers to the element at index `1`.
- Built-in array methods include:

  Name | Parameter | Description
  -- | -- | --
  `length` | | returns largest index + 1
  `indexOf(x)` | element to find | returns index of that element
  `push(x)` | new element | adds element to **end**
  `unshift(x)` | new element | adds element to **start**
  `pop()` | | removes **last** element
  `shift()` | | removes **0th** element
  `slice(start, end)` | indexes | **copies** an array
  `includes` | element to find | returns `true` if that element is in the array
  `forEach()` | `function`(element, index, array) | see next section ⬇️ 
  `map()` | `function`(element, index, array) | creates a new array after a specified **transformation**
  `filter()` | `function`(element, index, array) |  **filters** an array based on a specified condition
  `reduce()` | `function`(accumulator, value, index, array), initial value | reduces the array into a **single value**

***

## Loops
- `while` loops:
  ```js
  while (someCondition) {
    // do things
  }
  ```
- `do while` loops:
  ```js
  do {
    // do things
  }
  while (someCondition);
  ```
- `for` loops:
  ```js
  for (initialize; condition; increment) {
    // do things
  }
  ```
- `for`/`of` loops:
  ```js
  // kitten is a variable name we choose that represents each element
  // cats is a collection that already exists

  for (let kitten of cats) { 
    // do things
  }
  ```
- `for`/`in` loops:
  These should not be used for arrays as per the Google Style Guide, but instead for iterating through properties of an **object**.
  ```js
  // catKey is a variable that represents each property name
  // catObject is an object that already exists

  for (let catKey in catObject) {
    console.log(catKey);            // shows each property's name
    console.log(catObject[catKey]); // show's each property's value
  }
  ```
- `forEach()` iterates through a collection and executes the specified function once **for each** element:
  ```js
  myArray.forEach( 
    (element) => { // we can pass in element, index, and array
      // do things
    }
  );
  ```
- `break` statements exit a loop.*
- `continue` skips to the next iteration.*

  \* ⚠️ Both `break` and `continue` are frequently used as a lazy way out instead of good code design. If you choose to use them, make sure their use is adding value and not making your code worse (i.e. harder to read, test, and maintain).

***

## Fetch
`fetch` is a way to **asynchronously** request data. There are a few different ways we can use it: either with the `Promise` syntax or the `async`/`await` syntax.

- The `Promise` syntax looks like this:
  ```js
  fetch(specifiedURL) // where to fetch the data from
    .then((response) => {
      return response.json(); // extract the JSON body
    }).then((json_data) => {
      // do something with json_data
  });
  ```

- Alternatively, we can use the `async`/`await` syntax:
  ```js
  // call fetch
  let response = await fetch(specifiedURL);

  // get the data 
  let json_data =  await response.json();

  // then do something with json_data
  ```

  If a function contains `await`, it **must** be marked as `async`.

## Timers
- `setTimeout()` **waits** for a specified amount of time, then calls a function.
  - e.g.
    ```js
    let timeOutExample = setTimeout(() => {
      console.log("hello, world");
    }, 10000);
    ```
- `clearTimeout()` **cancels** an existing timer created with `setTimeout`.
  - e.g.
    ```js
    let cancelTimeOutExample = setTimeout(function() {
      console.log("this won't print");
    }, 2000);

    clearTimeout(cancelTimeOutExample);
    ```
- `setInterval()` **repeatedly calls** a function at a specified interval.
  - e.g.
    ```js
    // Tick every 0.2s until the number of ticks is equal to ten:
    let ticks = 0;
    let clock = setInterval(() => {
      console.log("tick", ticks++);
      // when 10 ticks are reached we cancel.
      if (ticks === 10) {
        clearInterval(clock);
        console.log("stop.");
      }
    }, 200);
    ```
- `clearInterval()` **cancels** an existing timer created with `setInterval`.
  - e.g.
    ```js
    let tickElement = document.querySelector("h1");
    let ticks = 0;

    let clock = setInterval(() => {
      console.log("tick", ticks++);
      tickElement.innerHTML = `Ticks: ${10 - ticks}`
      if (ticks == 10) {
        clearInterval(clock);
        tickElement.innerHTML = "Boom";
        console.log("stop.");
      }
    }, 1000);
    ```

***

## Document Object Model
The DOM represents the logical structure of an HTML document. The structure is represented as a **tree** containing **nodes**. There are many types of nodes, but in this course we only need to worry about 2: HTML elements, and text. In other words, an `Element` is just a special type of `Node`.

### DOM Functions
There are functions which let us **create** new nodes:
- `document.createElement('HTML_TAG_NAME')`
  - This is how we can create a new HTML element, e.g. a new `div`.
  - It returns a **reference** to the **newly created element**.
- `document.createTextNode('hello')`
  - This is how we add **text**. It returns a reference to the newly created **node**.

***

There are functions that let us **add** an existing `Node` into a structure:
- `parentNodeName.appendChild(childNodeName)`
  - e.g. adding text to an element, or adding that `div` to a specific location on our page.
  - If the parent already has children, this child will be added to the **end of the list** of children.
- `parentElement.insertBefore(ELEMENT_TO_INSERT, elementXYZ)`
  - This will insert `ELEMENT_TO_INSERT` **before** `elementXYZ`. Both are now children of `parentElement`.

***

There are functions that let us **remove** nodes:
- `parentElement.removeChild(ELEMENT_TO_REMOVE)`
  - This will **remove** `ELEMENT_TO_REMOVE`.
- `ELEMENT_TO_REMOVE.remove()`
  - This is another way to **remove** `ELEMENT_TO_REMOVE`.

***

And there are an assortment of other useful functions like:
- `elementXYZ.setAttribute(ATTRIBUTE_NAME, NEW_VALUE)`
  - This is how we can **change** the value of an **attribute**. e.g. adding an ID to an element, or changing the `type` of an `input`.
- `nodeXYZ.hasChildNodes()`
  - This returns `true` if this node has any **child nodes** & `false` otherwise.

***

### DOM Properties
`Node`s and `Element`s also have properties we can view and/or change.


> 🌲 Remember that `Element`s are just a special type of `Node`.

***

We can access **child** nodes:
- `elementXYZ.children`
  - This returns a live HTML collection containing all the child **elements**.
- `nodeXYZ.childNodes`
  - This returns a live HTML collection containing all the child **nodes** (including text).
- `elementName.firstElementChild`
  - this returns the **first child** that is an `Element`
  - ⚠️ This is similar but not the same as `firstChild` in the `Node` class, which will return the first `Node` child, whether it's an HTML element or text or something else.
- `elementName.lastElementChild`
  - This returns the last child that is an `Element`.

***

We can access **parent** nodes:
- `nodeXYZ.parentNode`
  - This returns the current node's **parent**.

***

And **siblings**, which are nodes who share the same direct parent:

- `elementName.nextElementSibling`
- `elementName.previousElementSibling`

***

Finally, we have additional properties like:
- `nodeXYZ.textContent`
  - As the name suggests, this is the **text** content of a node & its descendants.
  - ⚠️ That means this should be used with caution. If the element is just text, this works similarly to `innerText`, but if there are child nodes, this property will concatenate them all together. [Learn more about the differences between this property, `innerText`, & `innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent#differences_from_innertext).

***

## NPM & Modules
Within JavaScript, we can **export** functions, variables, constants, and classes. 
  - e.g.	`export { var1, const2, function3 } ;`

Once they're exported from the module, we can import them into a script:
  - e.g. `import { var1, const2, function3 } from "./xyz.js";`

***

### Terminal Commands

- Check your current version of **node**: `node -v`
- Check your current version of **npm**: `npm -v`
- `npm init` sets up an npm package
  - 📄 This is what creates the `package.json` file.
  - After the file is created, we will manually add in `scripts` & run any necessary `npm install XYZ` commands.
- `npm install` will install a package defined by `package.json` and its dependencies.
- `npm run scriptXYZ` is how we can **run** scripts within a package defined by `package.json`.

***

## Objects
Objects are another type of **collection**: a collection of **properties**.  Each property has a **name** and a **value**.
> 💡 This is why `for`/`in` works on objects!

In JS, objects can be created in a variety of ways.
- Using an **object initializer**
  ```js
  const dog = {
    name: 'Moose',
    age: 2,
    'is a good boy': true
  };
  ```
- Creating then invoking a **constructor**:
  ```js
  function Dog(breed, age, name) {
    this.breed = breed;
    this.age = age;
    this.name = name;
  }
  ```
  ```js
  const myDog = new Dog('pitbull', 2, 'Moose');
  ```
- ⭐ Using `Object.create()`, which creates a new object using an existing object as a prototype.

We can access the values of each property by
  - dot notation: `myDog.breed` or
  - bracket notation: `myDog["breed"]`

### JSON
There is a specific format for representing JavaScript objects as **text strings**. It is the standard format for structured data and is commonly used across many APIs.

For example, let's create a JavaScript object:
```js
let obj = 
	{ name: 'value', count: 42 } ;
```
We can then turn it into a JSON string using `stringify`:
```js
let otherJsonString = JSON.stringify(obj);
```

It also works in reverse. Let's say we have a JSON string:
```js
let jsonString = 
	'{"name":"value", "count":32}'
```
Here is how we turn that string into a JavaScript object by calling `parse`:
```js
let obj = JSON.parse(jsonString);
```

***

### Prototypes
Every object has a prototype (though the prototype might be `null`).

⭐ To view an object's prototype:
- `Object.getPrototypeOf(objectXYZ)`
- `classXYZ.prototype`

⭐ To add a new property to an existing prototype:
- `classXYZ.prototype.functionXYZ = function() {…}`

***

### Classes
**Classes** are just a special type of function that are templates for creating **objects**. We can create them with expressions or declarations.

#### Class Declarations
```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

#### Class Expressions
We can create an anonymous class:

```js
const Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

Or a named class:

```js
const Rectangle = class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

#### Class Composition
Rather than classical inheritance with superclasses and subclasses, a common approach in JavaScript is to focus more on what something **does** rather than what it **is**. For example:
```js
// let's say we're working with this Dog class:
class Dog {
  constructor(name, color) {
    this.name = name;
    this.color = color;
  }
}
```
```js
// first, let's create the functionality we want to add:
const barkMixin = {
  bark() {
    console.log(`${this.name}: bark! bark!`);
  }
};
```

```js
// then, we can assign that mix-in to the class:
Object.assign(Dog.prototype, barkMixin);
```
***

## Documentation
The standard approach to JavaScript documentation is **JSDoc**. The general syntax is:
```js
/**
 * [someFunction description]
 * @param  {[type]} arg1 [description]
 * @param  {[type]} arg2 [description]
 * @return {[type]}      [description]
 */
let someFunction = function (arg1, arg2) {
	// do something...
};
```

For example:
```js
/**
 * Add two numbers together.
 * @param  {Number} num1 The first number
 * @param  {Number} num2 The second number
 * @return {Number}      The total of the two numbers
 */
let addTwoNumbers = function (num1, num2) {
	return num1 + num2;
};
```

> This is in addition to **comments** (e.g. a one-line comment before a section of complex code) & your `ReadMe` file, which should include:
- Project **description**
- **Installation** instructions & **dependencies**
- **Examples**
- Contribution / licensing guidelines

