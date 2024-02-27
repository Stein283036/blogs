# JavaScript getElementsByTagName

## Introduction to JavaScript `getElementsByTagName()` method

The `getElementsByTagName()` is a method of the `document` object or a specific DOM element.

The `getElementsByTagName()` method accepts a tag name and returns a live `HTMLCollection` of elements with the matching tag name in the order which they appear in the document.

```js
let elements = document.getElementsByTagName(tagName);
```

The return collection of the `getElementsByTagName()` is live, meaning that it is automatically updated when elements with the matching tag name are added and/or removed from the document.

Note that the `HTMLCollection` is an array-like object, like `arguments` object of a function.

## JavaScript `getElementsByTagName()` example

When you click the **Count H2** button, the page shows the number of H2 tags:

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript getElementsByTagName() Demo</title>
</head>
<body>
    <h1>JavaScript getElementsByTagName() Demo</h1>
    <h2>First heading</h2>
    <p>This is the first paragraph.</p>
    <h2>Second heading</h2>
    <p>This is the second paragraph.</p>
    <h2>Third heading</h2>
    <p>This is the third paragraph.</p>
    <button id="btnCount">Count H2</button>
    <script>
        let btn = document.getElementById('btnCount');
        btn.addEventListener('click', () => {
            let headings = document.getElementsByTagName('h2');
            alert(`The number of H2 tags: ${headings.length}`);
        });
    </script>
</body>
</html>
```