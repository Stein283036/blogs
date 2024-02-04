# JavaScript Array Pop

## Introduction to the JavaScript Array pop() method

The `Array.prototype.pop()` method removes the last element from an array and returns the removed element

```js
array.pop()
```

The `pop()` method changes the `length` property of the array. If the array is empty, the `pop()` returns `undefined`.

## JavaScript pop() method example

### Using the JavaScript array pop() method to remove the last element of an array

```js
const numbers = [10, 20, 30];
const last = numbers.pop();
console.log(last); // 30
console.log(numbers.length); // 2
```

### Using the JavaScript array pop() method with an empty array

```js
const numbers = [];
const last = numbers.pop();
console.log(last); // undefined
console.log(numbers.length); // 0
```

## Using JavaScript pop() method with array-like objects

The `pop()` method is generic. Therefore, you can use the `call()` or `apply()` to call the `pop()` method on the array-like object. Internally, the `pop()` uses the `length` property of the array-like object to determine the last element to remove.

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  2: 'Howdy',
  length: 3,
  removeLast() {
    return Array.prototype.pop.call(this)
  },
}
let greting = greetings.removeLast()
console.log(greting)
console.log(greetings)
```

输出：

```js
Howdy
{
  '0': 'Hi',
  '1': 'Hello',
  length: 2,
  removeLast: [Function: removeLast]   
}
```