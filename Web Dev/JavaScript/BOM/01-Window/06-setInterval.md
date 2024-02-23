# JavaScript setInterval

## Introduction to JavaScript `setInterval()`

The `setInterval()` is a method of the `window` object. The `setInterval()` repeatedly calls a function with a fixed delay between each call.

```js
let intervalID = setInterval(handler: TimerHandler, timeout?: number, ...arguments: any[]): number
```

The `setInterval()` returns a numeric, non-zero number that identifies the created timer. You can pass the `intervalID` to the `clearInterval()` to cancel the timeout.

Note that the `setInterval()` works like the `setTimeout()` but it repeatedly executes a callback once every specified delay.

## JavaScript `setInterval()` example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>JavaScript setInterval Demo</title>
  <script>
    let intervalID;
 
    function toggleColor() {
      let e = document.getElementById('flashtext');
      e.style.color = e.style.color == 'red' ? 'blue' : 'red';
    }

    function stop() {
      clearInterval(intervalID);
    }

    function start() {
       intervalID = setInterval(toggleColor, 1000); 
    }
  </script>
</head>
<body>
  <p id="flashtext">JavScript setInterval Demo</p>
  <button onclick="start()">Start</button>
  <button onclick="stop()">Stop</button>
</body>
</html>
```