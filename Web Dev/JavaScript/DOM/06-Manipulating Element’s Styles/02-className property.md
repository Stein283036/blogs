# JavaScript className

## Introduction to the JavaScript className

The `className` is the property of an element that returns a space-separated list of CSS classes of the element as a string:

```js
element.className
```

Suppose that you have the following `ul` element:

```html
<ul id="menu" class="vertical main">
   <li>Homepage</li>
   <li>Services</li>
   <li>About</li>
   <li>Contact</li>
</ul>
```

The following shows the classes of the `ul` element in the console window:

```js
let menu = document.querySelector('#menu');
console.log(menu.className); // vertical main
```

To add a new class to an element using the `className` property, you can concatenate the existing class name with a new one:

```js
element.className += newClassName; 
```

The `+=` operator **concatenates** `newClassName` to the existing class list of the element. Therefore, you need to prefix the new class name with a space like this:

```js
let menu = document.querySelector('#menu');
menu.className += ' new';
console.log(menu.className); // 'vertical main new'
```

To completely overwrite all the classes of an element, you use a simple assignment operator.

```js
element.className = "class1 class2";
```

To get a complete list of classes of an element, you just need to access the `className` property:

```js
let classes = element.className;
```

Because the `class` is a keyword in JavaScript, the name `className` is used instead of the `class`.

Also the `class` is an HTML attribute:

```html
<div id="note" class="info yellow-bg red-text">JS className</div>
```

while `className` is a DOM property of the element:

```js
let note = document.querySelector('#note');
console.log(note.className); // info yellow-bg red-text
```