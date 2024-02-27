# JavaScript CreateElement

To create an HTML element, you use the `document.createElement()` method:

```js
let element = document.createElement(htmlTag);
```

## Creating a new div example

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>JS CreateElement Demo</title>
</head>
<body>
</body>
</html>
```

The following example uses the `document.createElement()` to create a new `<div>` element:

```js
let div = document.createElement('div');
```

And add an HTML snippet to the `div`:

```js
div.innerHTML = '<p>CreateElement example</p>';
```

To attach the `div` to the document, you use the `appendChild()` method:

```js
document.body.appendChild(div);
```

### Adding an id to the div

If you want to add an id to a `div`, you set the `id` attribute of the element to a value, like this:

```js
let div = document.createElement('div');
div.id = 'content';
div.innerHTML = '<p>CreateElement example</p>';
document.body.appendChild(div);
```

### Adding a class to the div

The following example set the CSS class of a new div `note`:

```js
let div = document.createElement('div');
div.id = 'content';
div.className = 'note';
div.innerHTML = '<p>CreateElement example</p>';
document.body.appendChild(div);
```

### Adding text to a div

To add a piece of text to a `<div>`, you can use the `innerHTML` property as the above example, or create a new `Text` node and append it to the `div`:

```js
// create a new div and set its attributes
let div = document.createElement('div');
div.id = 'content';
div.className = 'note';
// create a new text node and add it to the div
let text = document.createTextNode('CreateElement example');
div.appendChild(text);
// add div to the document
document.body.appendChild(div);
```

### Adding an element to a div

To add an element to a `div`, you create an element and append it to the `div` using the `appendChild()` method:

```js
let div = document.createElement('div');
div.id = 'content';
div.className = 'note';

// create a new heading and add it to the div
let h2 = document.createElement('h2');
h2.textContent = 'Add h2 element to the div';
div.appendChild(h2);

// add div to the document
document.body.appendChild(div);
```

## Creating new list items (`li`) example

```html
<ul id="menu">
    <li>Home</li>
</ul>
```

The following code adds two `li` elements to the `ul`:

```js
const menu = document.querySelector('#menu')
let li1 = document.createElement('li')
li1.textContent = 'Products'
menu.appendChild(li1)
let li2 = document.createElement('li')
li2.textContent = 'About Us'
menu.appendChild(li2)
```

## Creating a `script` element example

Sometimes, you may want to load a JavaScript file dynamically. To do this, you can use the `document.createElement()` to create the `script` element and add it to the document.

The following example illustrates how to create a new `script` element and loads the `/lib.js` file to the document:

```js
let script = document.createElement('script');
script.src = '/lib.js';
document.body.appendChild(script);
```