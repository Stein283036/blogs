# JavaScript Array Push

## Introduction to the JavaScript Array push() method

The `Array.prototype.push()` method adds one or more elements to the **end** of an array and returns the new array’s length.

```js
push(newElement);
push(newElement1,newElement2);
push(newElement1,newElement2,...,newElementN);
```

### JavaScript Array push() method examples

### Using the array push() to append one element to an array

```js
let numbers = [10, 20, 30];

const length = numbers.push(40);

console.log(length); // 4
console.log(numbers); // [10, 20, 30, 40]
```

### Using the array push() to add multiple elements to the end of an array

```js
let numbers = [10, 20, 30];
const length = numbers.push(40, 50);
console.log(length); // 5
console.log(numbers); // [10, 20, 30, 40, 50]
```

### Using the push() to append elements of an array to another array

```js
let colors = ['red', 'green', 'blue'];
let cmyk = ['cyan', 'magenta', 'yellow', 'back'];
colors.push(...cmyk);
console.log(colors);
```

## Using JavaScript Array push() method with array-like objects

The `Array.prototype.push()` method is designed to be generic on purpose. Therefore, you can call the `push()` method with the `call()` or `apply()` on the array-like objects.

Under the hood, the `push()` method uses the `length` property to determine the position for inserting the elements. If the `push()` method cannot convert the `length` property into a number, it’ll use `0` as the value for the index.

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  length: 2,
  append(message) {
    Array.prototype.push.call(this, message)
  },
}
greetings.append('你好')
greetings.append('Bonjour')
console.log(greetings)
```

首先，定义具有三个属性 0、1 和 length 以及一个方法 append() 的 greetings 对象：

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  length: 2,
  append(message) {
    Array.prototype.push.call(this, message)
  },
}
```

The `append()` method calls the `push()` method of an array object to append the `message` to the `greetings` object.

其次，调用 greetings 对象的 append() 方法：

```js
greetings.append('你好')
greetings.append('Bonjour')
```

在每次调用中，push() 使用 greetings 对象的 length 属性来确定附加新元素的位置，并将 length 属性加一。因此，greetings 对象在索引 2 和 3 处多了两个元素。调用后，length 属性为 4。

输出：

```js
{
  '0': 'Hi',
  '1': 'Hello',
  '2': '你好',
  '3': 'Bonjour',
  length: 4,
  append: [Function: append]
}
```

To allow the append() method to accepts a number of messages, you can modify the method like this:

```js
let greetings = {
  0: 'Hi',
  1: 'Hello',
  length: 2,
  append() {
    Array.prototype.push.call(this, ...arguments);
  },
};
greetings.append('Howdy', 'Bonjour');
console.log(greetings);
```