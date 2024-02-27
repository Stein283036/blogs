# JavaScript DOMContentLoaded

The `DOMContentLoaded` fires when the DOM content is loaded, without waiting for images and stylesheets to finish loading.

You need to handle the `DOMContentLoaded` event when you place the JavaScript in the `head` of the page but referencing elements in the body, for example:

```html
<!DOCTYPE html>
<html>

<head>
    <title>JS DOMContentLoaded Event</title>
    <script>
        let btn = document.getElementById('btn');
        btn.addEventListener('click', (e) => {
            // handle the click event
            console.log('clicked');
        });
    </script>
</head>

<body>
    <button id="btn">Click Me!</button>
</body>

</html>
```

In this example, we reference the button in the `body` from the JavaScript in the `head`.

Because the DOM has not been loaded when the JavaScript engine parses the JavaScript in the `head`, the button with the id `btn` does not exist.

To fix this, you place the code inside an `DOMContentLoaded` event handler, like this:

```html
<!DOCTYPE html>
<html>

<head>
    <title>JS DOMContentLoaded Event</title>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            let btn = document.getElementById('btn');
            btn.addEventListener('click', () => {
                // handle the click event
                console.log('clicked');
            });
        });
    </script>
</head>

<body>
    <button id="btn">Click Me!</button>
</body>

</html>
```

When you place JavaScript in the header, it will cause bottlenecks and rendering delays, so it’s better to move the script before the `</body>` tag. In this case, you don’t need to place the code in the `DOMContentLoaded` event, like this:

```html
<!DOCTYPE html>
<html>

<head>
    <title>JS DOMContentLoaded Event</title>
</head>

<body>
    <button id="btn">Click Me!</button>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            let btn = document.getElementById('btn');
            btn.addEventListener('click', () => {
                // handle the click event
                console.log('clicked');
            });
        });
    </script>
</body>
</html>
```





