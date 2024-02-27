# JavaScript onload

## The window’s load event

For the `window` object, the `load` event is fired when the whole webpage (HTML) has loaded fully, including all dependent resources, including JavaScript files, CSS files, and images.

To handle the `load` event, you register an event listener using the `addEventListener()` method:

```js
window.addEventListener('load', (event) => {
    console.log('The page has fully loaded');
});
```

Or use the `onload` property of the `window` object:

```js
window.onload = (event) => {
    console.log('The page has fully loaded');
};
```



