# JavaScript Window

## The `window` object is global

The global object of JavaScript in the web browser is the `window` object. It means that all variables and functions declared globally with the `var` keyword become the properties and methods of the `window` object.

```js
var counter = 1;
var showCounter = () => console.log(counter);
console.log(window.counter); // 1
window.showCounter(); // 1
```

## The `window` object exposes the browser’s functionality

The `window` object exposes the functionality of the web browser to the webpage.

### Window size

The `window` object has four properties related to the size of the window:

- The `innerWidth` and `innerHeight` properties return the size of the page viewport inside the browser window (not including the borders and toolbars).
- The `outerWidth` and `outerHeight` properties return the size of the browser window itself.

Also, `document.documentElement.clientWidth` and `document.documentElement.clientHeight` properties indicate the width and height of the page viewport.

```js
const width = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;
const height = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight; 
```

### Open a new window

To open a new window or tab, you use the `window.open()` method:

```js
window.open(url, windowName, [windowFeatures]);
```

The `window.open()` method accepts three arguments: the URL to load, the window target and a string of window features.

The third argument is a command-delimited string of settings specifying displaying information for the new window such as width, height, menubar, and resizable.

The `window.open()` method returns a `WindowProxy` object, which is a thin wrapper of the `window` object. In case the new window cannot be opened, it returns `null`.

For example, to open a new window that loads the page `about.html` at localhost, you use the following code:

```js
let url = 'file:///D:/front-end-learning/03-Javascript/demo.html';
let jsWindow = window.open(url,'about');
```

The code opens the page `about.html` in a new tab. If you specify the `height` and `width` of the window, it will open the URL in a new separated window instead of a new tab:

```js
let features = 'height=600,width=800',
    url = 'file:///D:/front-end-learning/03-Javascript/demo.html';
let jsWindow = window.open(url, 'about', features);
```

### Resize a window

To resize a window you use the `resizeTo()` method of the `window` object:

```js
window.resizeTo(width,height);
```

The following example opens a new window that loads the `file:///D:/front-end-learning/03-Javascript/demo.html` page and resize it to `(600,300)` after 3 seconds:

```js
let jsWindow = window.open(
    'file:///D:/front-end-learning/03-Javascript/demo.html',
    'about',
    'height=600,width=800');

setTimeout(() => {
    jsWindow.resizeTo(600, 300);
}, 3000);
```

The `window.resizeBy()` method allows you to resize the current window by a specified amount:

```js
window.resizeBy(deltaX,deltaY);
```

```js
let jsWindow = window.open(
    'file:///D:/front-end-learning/03-Javascript/demo.html',
    'about',
    'height=600,width=600');

// shrink the window, or resize the window 
// to 500x500
setTimeout(() => {
    jsWindow.resizeBy(-100, -100);
}, 3000);
```

### Move a window

To move a window to a specified coordinate, you use the `moveTo()` method:

```js
window.moveTo(x, y);
```

在此方法中，x 和 y 是要移动到的水平和垂直坐标。以下示例打开一个新窗口并在 3 秒后将其移动到 (0,0) 坐标：

```js
let jsWindow = window.open(
    'file:///D:/front-end-learning/03-Javascript/demo.html',
    'about',
    'height=600,width=600');

setTimeout(() => {
    jsWindow.moveTo(500, 500);
}, 3000);
```

同样，可以将当前窗口移动指定的量：

```js
let jsWindow = window.open(
    'file:///D:/front-end-learning/03-Javascript/demo.html',
    'about',
    'height=600,width=600');

setTimeout(() => {
    jsWindow.moveBy(100, 100);
}, 3000);
```

### Close a window

To close a window, you use the `window.open()` method:

```js
window.open()
```

```js
let jsWindow = window.open(
    'file:///D:/front-end-learning/03-Javascript/demo.html',
    'about',
    'height=600,width=600');

setTimeout(() => {
    jsWindow.close();
}, 3000);
```

### The `window.opener` property

A newly created window can reference back to the window that opened it via the `window.opener` property. This allows you to exchange data between the two windows.
