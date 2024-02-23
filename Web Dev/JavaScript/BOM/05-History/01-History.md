# JavaScript History

## Introduction to the JavaScript `history` object.

When you launch the web browser and open a new webpage, the web browser creates a new entry in its history stack.

If you navigate to another webpage, the web browser also creates a new entry in the history stack.

The history stack stores the current page and previous pages that you visited.

For the security reason, it’s not possible to query the pages that a user have visited. However, you can use the `history` object to navigate back and forth without knowing the exact URL.

## Using JavaScript `history` for navigation

The history object provides three methods for navigating between pages in the history stack:

-  `back()`
-  `forward()`
-  `go()`

### Move backward

To move backward through history, you use the `back()` method:

```js
history.back();
```

This behaves like you click the **Back** button in the toolbar of the web browser.

### Move forward

Similarly, you can move forward by using the `forward()` method:

```js
history.forward();
```

It works like when you click the **Forward** button.

### Move to a specific URL in the history

To move to a specific URL in the history stack, you use the `go()` method. The `go()` method accepts an integer that is the relative position to the current page. The current page’s position is 0.

For example, to move backward you use:

```js
history.go(-1);Code language: CSS (css)
```

It is like the `back()` method.

To move forward a page, you just call:

```js
history.go(1);
```

To refresh the current page, you either pass 0 or no argument to the `go()` method:

```js
history.go(0);
history.go();
```

To determine the number of URLs in the history stack, you use the `length` property:

```js
history.length
```