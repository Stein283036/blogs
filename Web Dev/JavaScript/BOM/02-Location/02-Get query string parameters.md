# How To Get Query String in JavaScript

To get a query string you can access the `search` property of the `location` object:

```js
location.search
```

Assuming that the value of the `location.search` is:

```js
'?type=list&page=20'
```

To work with the query string, you can use the `URLSearchParams` object.

```js
const urlParams = new URLSearchParams(location.search);
```

The `URLSearchParams` is an iterable object, therefore you can use the `for...of` structure to iterate over its elements which are query string parameters:

```js
const urlParams = new URLSearchParams(location.search);

for (const [key, value] of urlParams) {
    console.log(`${key}:${value}`);
}
type:list
page:20
```

## Useful `URLSearchParams` methods

The `URLSearchParams` has some useful methods that return iterators of parameter keys, values, and entries:

- `keys()` returns an iterator that iterates over the parameter keys.
- `values()` returns an iterator that iterates over the parameter values.
- `entries()` returns an iterator that iterates over the (key, value) pairs of the parameters.

## Check if a query string parameter exists

The `URLSearchParams.has()` method returns `true` if a parameter with a specified name exists.

```js
const urlParams = new URLSearchParams('?type=list&page=20');
console.log(urlParams.has('type')); // true
console.log(urlParams.has('foo'));  // false
```