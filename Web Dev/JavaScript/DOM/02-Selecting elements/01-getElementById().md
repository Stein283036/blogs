# JavaScript getElementById

## Introduction to JavaScript getElementById() method

The `document.getElementById()` method returns an `Element` object that represents an HTML element with an id that matches a specified string.

If the document has no element with the specified id, the `document.getElementById()` returns `null`.

Because the id of an element is unique within an HTML document, the `document.getElementById()` is a quick way to access an element.

Unlike the `querySelector()` method, the `getElementById()` is only available on the `document` object, not other elements.

```js
const element = document.getElementById(id);
```

In this syntax, the id is a string that represents the id of the element to select. The id is case-sensitive. For example, the `'root'` and `'Root'` are totally different.

## JavaScript getElementById() method example

```js
<html>
    <head>
        <title>JavaScript getElementById() Method</title>
    </head>
    <body>
        <p id="message">A paragraph</p>
    </body>
</html>
```

The document contains a `<p>` element that has the `id` attribute with the value `message`:

```js
const p = document.getElementById('message');
console.log(p); // <p id="message">A paragraph</p>
```