# JavaScript Array shift

## Introduction to the JavaScript Array shift() function

The `Array.prototype.shift()` method removes the first element from an array and returns that element.

```js
array.shift()
```

If the array is empty, the `shift()` method returns `undefined`. Otherwise, it returns the removed element. Also, the `shift()` method reduces the `length` property of the array by one.

> Note that the `shift()` method has to reindex all the remaining elements of an array. Therefore, it’s slower in comparison with the `pop()` method.

## JavaScript Array shift() method examples

### Using the JavaScript array shift() method example

```js
const numbers = [10, 20, 30];
let number = numbers.shift();
console.log({ number });
console.log({ numbers });
console.log({ length: numbers.length });
```

## Using the JavaScript array shift() with array-like object

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  2: 'Howdy',
  length: 3,
  removeFirst() {
    return Array.prototype.shift.call(this)
  },
}
const greeting = greetings.removeFirst()
console.log(greeting)
console.log(greetings)
```

输出：

```js
Hi
{
  '0': 'Hello',
  '1': 'Howdy',
  length: 2,
  removeFirst: [Function: removeFirst]
}
```