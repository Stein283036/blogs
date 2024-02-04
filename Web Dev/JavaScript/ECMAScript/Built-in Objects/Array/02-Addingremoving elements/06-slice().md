# 3 Pragmatic Uses of JavaScript Array slice() Method

## Introduction to JavaScript Array slice() method

```js
slice(start?: number, end?: number): any[]
// start: The beginning index of the specified portion of the array. If start is undefined, then the slice begins at index 0.
// The end index of the specified portion of the array. This is exclusive of the element at the index 'end'. If end is undefined, then the slice extends to the end of the array.
// Returns a copy of a section of an array. For both start and end, a negative index can be used to indicate an offset from the end of the array. For example, -2 refers to the second to last element of the array.
```

slice() 方法仅将元素浅复制到新数组并返回。此外，它不会更改源数组。

## Clone an array

```js
const numbers = [1,2,3,4,5];
const newNumbers = numbers.slice();
```

## Copy a portion of an array

The typical use of the `slice()` method is to copy a portion of an array without modifying the source array.

```js
const colors = ['red','green','blue','yellow','purple'];
const rgb = colors.slice(0,3);
console.log(rgb); // ["red", "green", "blue"]
```

## Convert array-like objects into arrays

```js
function toArray() {
  return Array.prototype.slice.call(arguments);
}
const classification = toArray('A','B','C');
console.log(classification); // ["A", "B", "C"]
```

经常看到的另一个典型示例是将 NodeList（返回的是伪数组对象） 转换为数组：

```js
const p = document.querySelectorAll('p');
const list = Array.prototype.slice.call(p);
```