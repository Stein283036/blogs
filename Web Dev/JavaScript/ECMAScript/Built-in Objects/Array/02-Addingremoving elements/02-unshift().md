# JavaScript Array unshift

## Introduction to the JavScript Array unshift() method

Array.prototype.unshift() 方法将一个或多个元素添加到数组的开头并返回新数组的长度。

unshift() 方法的语法：

```js
unshift(element);
unshift(element1, element2);
unshift(element1, element2,...elementN);
```

Because the `unshift()` method needs to reindex the existing elements, it is slow if the array has many elements.

## JavaScript Array unshift() method examples

### Using the JavaScript Array unshift() method to prepend an element to an array

```js
let numbers = [30, 40];
const length = numbers.unshift(20);
console.log({ length }); // { length: 3 }
console.log({ numbers }); // { numbers: [ 20, 30, 40 ] }
```

### Using the JavaScript Array unshift() method to prepend multiple elements to an array

```js
let numbers = [30, 40];
const length = numbers.unshift(10, 20);
console.log({ length });
console.log({ numbers });
```

### Using the JavaScript array unshift() to add elements of an array to another array

```js
let days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'];
let weekends = ['Sat', 'Sun'];
days.unshift(...weekends);
console.log(days);
```

## Using the JavaScript Array unshift() method with array-like objects

unshift() 方法是通用的。因此，它可以很好地处理类似数组的对象。要从类似数组的对象调用 unshift() 方法，可以使用 call() 或 apply() 方法从数组对象借用该方法。

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  2: 'Howdy',
  length: 3,
  prepend(message) {
    Array.prototype.unshift.call(this, message);
    return this.length;
  },
};
greetings.prepend('Good day');
console.log(greetings);
```