# JavaScript querySelector

## Introduction to JavaScript querySelector() and querySelectorAll() methods

The `querySelector()` is a method of the `Element` interface. The `querySelector()` method allows you to select the first element that matches one or more CSS selectors.

```js
let element = parentNode.querySelector(selector);
```

If the `selector` is not valid CSS syntax, the method will raise a `SyntaxError` exception.

If no element matches the CSS selectors, the `querySelector()` returns `null`.

> The `querySelector()` method is available on the `document` object or any `Element` object.

Besides the `querySelector()`, you can use the `querySelectorAll()` method to select all elements that match a CSS selector or a group of CSS selectors:

```js
let elementList = parentNode.querySelectorAll(selector);
```

The `querySelectorAll()` method returns a static `NodeList` of elements that match the CSS selector. If no element matches, it returns an empty `NodeList`.

> Note that the `NodeList` is an array-like object, not an array object. However, in modern web browsers, you can use the `forEach()` method or the `for...of` loop.

To convert the `NodeList` to an array, you use the `Array.from()` method like this:

```js
let nodeList = document.querySelectorAll(selector);
let elements = Array.from(nodeList);
```

## Basic selectors

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>querySelector() Demo</title>
</head>
<body>
    <header>
        <div id="logo">
            <img src="img/logo.jpg" alt="Logo" id="logo">
        </div>
        <nav class="primary-nav">
            <ul>
                <li class="menu-item current"><a href="#home">Home</a></li>
                <li class="menu-item"><a href="#services">Services</a></li>
                <li class="menu-item"><a href="#about">About</a></li>
                <li class="menu-item"><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <h1>Welcome to the JS Dev Agency</h1>

        <div class="container">
            <section class="section-a">
                <h2>UI/UX</h2>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Autem placeat, atque accusamus voluptas
                    laudantium facilis iure adipisci ab veritatis eos neque culpa id nostrum tempora tempore minima.
                    Adipisci, obcaecati repellat.</p>
                <button>Read More</button>
            </section>
            <section class="section-b">
                <h2>PWA Development</h2>
                <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Magni fugiat similique illo nobis quibusdam
                    commodi aspernatur, tempora doloribus quod, consectetur deserunt, facilis natus optio. Iure
                    provident labore nihil in earum.</p>
                <button>Read More</button>
            </section>
            <section class="section-c">
                <h2>Mobile App Dev</h2>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Animi eos culpa laudantium consequatur ea!
                    Quibusdam, iure obcaecati. Adipisci deserunt, alias repellat eligendi odit labore! Fugit iste sit
                    laborum debitis eos?</p>
                <button>Read More</button>
            </section>
        </div>
    </main>
    <script src="js/main.js"></script>
</body>
</html>
```

### Universal selector

The universal selector is denoted by `*` that matches all elements of any type:

```js
*
```

The following example uses the `querySelector()` selects the first element in the document:

```js
let element = document.querySelector('*');
```

And this select all elements in the document:

```js
let elements = document.querySelectorAll('*');
```

### Type selector

To select elements by node name, you use the type selector e.g., `a` selects all `<a>` elements:

```js
elementName
```

The following example finds the first `h1` element in the document:

```js
let firstHeading = document.querySelector('h1');
```

And the following example finds all `h2` elements:

```js
let heading2 = document.querySelectorAll('h2');
```

### Class selector

To find the element with a given CSS class, you use the class selector syntax:

```js
.className
```

The following example finds the first element with the `menu-item` class:

```js
let note = document.querySelector('.menu-item');
```

And the following example finds all elements with the `menu` class:

```js
let notes = document.querySelectorAll('.menu-item');
```

### ID Selector

To select an element based on the value of its id, you use the id selector syntax:

```js
#id
```

The following example finds the first element with the id `#logo`:

```js
let logo = document.querySelector('#logo');
```

## Grouping selectors

To group multiple selectors, you use the following syntax:

```js
selector, selector, ...
```

The selector list will match any element with one of the selectors in the group.

The following example finds all `<div>` and `<p>` elements:

```js
let elements = document.querySelectorAll('div, p');
```