# JavaScript Array Join

## Introduction to the JavaScript array join() method

The `join()` method allows you to concatenate all elements of an array and returns a new string:

```js
join(separator?: string): string
// separator: A string used to separate one element of the array from the next in the resulting string. If omitted, the array elements are separated with a comma.
// Adds all the elements of an array into a string, separated by the specified separator string.
```

In case the array has one element, the `join()` method returns that element as a string without using the `separator`.

如果数组为空，则 join() 方法返回一个空字符串。

当数组的元素不是字符串时， join() 方法会在连接之前将它们转换为字符串。

请注意，join() 方法将 undefined、null 和空数组 [] 转换为空字符串。

## JavaScript Array join() method examples

```js
let arr = [1, 'b', null, undefined, NaN, [], {}, Infinity]
let arrstr = arr.join('-')
console.log(arrstr) // 1-b---NaN--[object Object]-Infinity
```

### Using the JavaScript Array join() method to join CSS classes

```js
const cssClasses = ['btn', 'btn-primary', 'btn-active'];
const btnClass = cssClasses.join(' ');
console.log(btnClass); // btn btn-primary btn-active
```

### Using the JavaScript Array join() method to replace all occurrences of a string

This example uses the JavaScript Array `join()` method to replace all occurrences of the space `' '` by the hyphen (`-`):

```js
const title = 'JavaScript array join example'
const url = title.split(' ').join('-').toLowerCase()
console.log(url) // javascript-array-join-example
```