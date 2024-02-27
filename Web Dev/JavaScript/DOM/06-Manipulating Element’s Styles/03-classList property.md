# JavaScript classList

## Introduction to JavaScript `classList` property

The `classList` is a read-only property of an element that returns a live collection of CSS classes:

```js
const classes = element.classList;
```

The `classList` is a `DOMTokenList` object that represents the contents of the element’s class attribute.

Even though the `classList` is read-only, but you can manipulate the classes it contains using various methods.

## JavaScript `classList` examples

### Get the CSS classes of an element

Suppose that you have a `div` element with two classes: `main` and `red`.

```html
<div id="content" class="main red">JavaScript classList</div>   
```

The following code displays the class list of the `div` element in the Console window:

```js
let div = document.querySelector('#content');
for (let cssClass of div.classList) {
    console.log(cssClass);
}
```

输出：

```js
main
red
```

### Add one or more classes to the class list of an element

To add one or more CSS classes to the class list of an element, you use the `add()` method of the `classList`.

For example, the following code adds the `info` class to the class list of the `div` element with the id `content`:

```js
let div = document.querySelector('#content');
div.classList.add('info');
```

The following example adds multiple CSS classes to the class list of an element:

```js
let div = document.querySelector('#content');
div.classList.add('info','visible','block');
```

### Remove element’s classes

To remove a CSS class from the class list of an element, you use the `remove()` method:

```js
let div = document.querySelector('#content');
div.classList.remove('visible');
```

Like the `add()` method, you can remove multiple classes once:

```js
let div = document.querySelector('#content');
div.classList.remove('block','red');
```

### Replace a class of an element

To replace an existing CSS class with a new one, you use the `replace()` method:

```js
let div = document.querySelector('#content');
div.classList.replace('info','warning');
```

### Check if an element has a specified class

To check if the element has a specified class, you use the `contains()` method:

```js
let div = document.querySelector('#content');
div.classList.contains('warning'); // true
```

### Toggle a class

If the class list of an element contains a specified class name, the toggle() method removes it. If the class list doesn’t contain the class name, the toggle() method adds it to the class list.

The following example uses the `toggle()` method to toggle the `visible` class of an element with the id `content`:

```js
let div = document.querySelector('#content');
div.classList.toggle('visible');
```