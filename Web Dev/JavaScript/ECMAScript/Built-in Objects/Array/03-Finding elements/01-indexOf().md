# JavaScript Array indexOf and lastIndexOf: Locating an Element in an Array

## Introduction to the JavaScript array `indexOf()` method

```js
indexOf(searchElement: any, fromIndex?: number): number
// searchElement: The value to locate in the array.
// fromIndex: The array index at which to begin the search. If fromIndex is omitted, the search starts at index 0.
// Returns the index of the first occurrence of a value in an array, or -1 if it is not present.
```

Notice that the `indexOf()` method uses the strict equality comparison algorithm that is similar to the triple-equals operator (`===`) when comparing the `searchElement` with the elements in the array.

## The JavaScript array `indexOf()` method examples

```js
var scores = [10, 20, 30, 10, 40, 20];
console.log(scores.indexOf(10)); // 0
console.log(scores.indexOf(30)); // 2
console.log(scores.indexOf(50)); // -1
console.log(scores.indexOf(20)); // 1
```

```js
console.log(scores.indexOf(20, -1)) // 5
console.log(scores.indexOf(20, -5)) // 1 
```

Assuming that you have the following array of objects, where each object has two properties: `name` and `age`.

```js
var guests = [
    {name: 'John Doe', age: 30},
    {name: 'Lily Bush', age: 20},
    {name: 'William Gate', age: 25}
];
```

The following statement returns `-1` even though the first element of the `guests` array and the `searchElement` have the same values in the `name` and `ages` properties. This is because they are two different objects.

```js
console.log(guests.indexOf({
    name: 'John Doe',
    age: 30
})); // -1
```

## JavaScript array `lastIndexOf()` method

```js
lastIndexOf(searchElement: any, fromIndex?: number): number
// Returns the index of the last occurrence of a specified value in an array, or -1 if it is not present.
```

lastIndexOf() 方法返回 searchElement 在数组中最后一次出现的索引。如果找不到该元素，则返回 -1。

```js
console.log(scores.lastIndexOf(10));// 3
console.log(scores.lastIndexOf(20));// 5
```