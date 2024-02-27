# JavaScript Get the Parent Element parentNode

## Introduction to parentNode attribute

To get the parent node of a specified node in the DOM tree, you use the `parentNode` property:

```js
let parent = node.parentNode;
```

The `parentNode` is read-only.

The `Document` and `DocumentFragment` nodes do not have a parent. Therefore, the `parentNode` will always be `null`.

If you create a new node but haven’t attached it to the DOM tree, the `parentNode` of that node will also be `null`.

## JavaScript parentNode example

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>JavaScript parentNode</title>
</head>
<body>
    <div id="main">
        <p class="note">This is a note!</p>
    </div>

    <script>
        let note = document.querySelector('.note');
        console.log(note.parentNode);
    </script>
</body>
</html>
```