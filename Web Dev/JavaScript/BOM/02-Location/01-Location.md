# JavaScript Location

The `Location` object represents the current location (URL) of a document. You can access the `Location` object by referencing the `location` property of the `window` or `document` object.

## JavaScript Location properties

Suppose that the current URL is:

```js
http://localhost:8080/js/index.html?type=listing&page=2#title
```

### Location.href

The `location.href` is a string that contains the entire URL.

```js
"http://localhost:8080/js/index.html?type=listing&page=2#title"
```

### Location.protocol

The `location.protocol` represents the protocol scheme of the URL including the final colon (`:`).

```js
'http:'
```

### Location.host

The `location.host` represents the hostname:

```js
"localhost:8080"
```

### Location.port

The `location.port` represents the port number of the URL.

```js
"8080"
```

### Location.pathname

The `location.pathname` contains an initial `'/'` followed by the path of the URL.

### Location.search

The `location.search` is a string that represents the query string of the URL:

```js
"?type=listing&page=2"
```

### Location.hash

The `location.hash` returns a string that contains a ‘#’ followed by the fragment identifier of the URL.

```js
"#title"
```

### Location.origin

The `location.origin` is a string that contains the canonical form of the origin of the specific location.

```js
"http://localhost:8080"
```

## Manipulating the location

The `Location` object has a number of useful methods: `assign()`, `reload()`, and `replace()`.

###  `assign()`

The `assign()` method accepts an URL, navigate to the URL immediately, and make an entry in the browser’s history stack.

```js
location.assign('https://www.javascripttutorial.net');
```

当 window.location 或 location.href 设置为 URL 时，将隐式调用 allocate() 方法：

```js
window.location = 'https://www.javascripttutorial.net';
location.href = 'https://www.javascripttutorial.net';
```

If you change `hostname`, `pathname`, or `port` property, the page reloads with the new value. Note that changing `hash` property doesn’t reload the page but does record a new entry in the browser’s history stack.

### `replace()`

The `replace()` method is similar to the `assign()` method except it doesn’t create a new entry in the browser’s history stack. Therefore, you cannot click the back button to go to the previous page.

```js
setTimeout(() => {
    location.replace('https://www.javascripttutorial.net');
}, 3000);
```

### `reload()`

The `reload()` method reloads the currently displayed page. When you call the `reload()` method with no argument, the browser will reload the page in the most efficient way e.g., it loads the page resources from the browser’s cache if they haven’t changed since the last request.

```js
reload();
```

To force a reload from the server, you pass true to the `reload()` method:

```
reload(true);
```

Note that the code after the `reload()` may or may not execute, depending on many factors like network latency and system resources. Therefore, it is a good practice to place the `reload()` as the last line in the code.
