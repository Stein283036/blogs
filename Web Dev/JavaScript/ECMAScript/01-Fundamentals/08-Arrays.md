# Arrays

## Introduction to JavaScript arrays

在 JavaScript 中，数组是值的有序列表。每个值称为由索引指定的元素：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/08/JavaScript-Array.svg)

JavaScript 数组具有以下特征：

- 数组存储的元素类型可以不同
- 数组的大小是动态的并且自动增长

数组是一种特殊的对象。使用方括号来访问属性 `arr[0]` 实际上是来自于对象的语法。它其实与 `obj[key]` 相同，其中 `arr` 是对象，而数字用作键（key）。

它们扩展了对象，提供了特殊的方法来处理有序的数据集合以及 `length` 属性。但从本质上讲，它仍然是一个对象。

## Creating JavaScript arrays

JavaScript 提供了两种创建数组的方法。

`Array` 构造函数：

```js
let scores = new Array();
```

如果知道数组将容纳的元素数量，则可以创建一个具有初始大小的数组：

```js
let scores = Array(10);
```

要创建数组并使用一些元素对其进行初始化，将元素作为逗号分隔列表传递到 Array() 构造函数中。

```js
let scores = new Array(9,10,8,7,6);
```

JavaScript 允许在使用 Array() 构造函数时省略 new 运算符。

```js
let artists = Array();
```

在实践中，很少会使用 Array() 构造函数来创建数组。

创建数组的更优选方法是使用数组字面量表示法 []：

```js
let arrayName = [element1, element2, element3, ...];
```

## Accessing JavaScript array elements

JavaScript 数组是从零开始索引的。

要访问数组中的元素，请在方括号 [] 中指定索引：

```js
arrayName[index]
```

## Getting the array size

通常，数组的 length 属性返回元素的数量。

当我们修改数组的时候，`length` 属性会自动更新。准确来说，它实际上不是数组里元素的个数，而是最大的数字索引值加一。

```js
let mountains = ['Everest', 'Fuji', 'Nanga Parbat'];
console.log(mountains.length); // 3
```

`length` 属性的另一个有意思的点是它是可写的。

如果我们手动增加它，则不会发生任何有趣的事儿。但是如果我们减少它，数组就会被截断。

```javascript
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // 截断到只剩 2 个元素
alert( arr ); // [1, 2]

arr.length = 5; // 又把 length 加回来
alert( arr[3] ); // undefined：被截断的那些数值并没有回来
```

所以，清空数组最简单的方法就是：`arr.length = 0;`。

## Basic operations on arrays

### Adding an element to the end of an array

要将元素添加到数组末尾，可以使用 push() 方法：

```js
let seas = ['Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea'];
seas.push('Red Sea');

console.log(seas); 
[ 'Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea', 'Red Sea' ]
```

### Adding an element to the beginning of an array

要将元素添加到数组的开头，可以使用 unshift() 方法：

```js
let seas = ['Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea'];
seas.unshift('Red Sea');

console.log(seas);
[ 'Red Sea', 'Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea' ]
```

### Removing an element from the end of an array

要从数组末尾删除元素，可以使用 pop() 方法：

```js
let seas = ['Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea'];
const lastElement = seas.pop();
console.log(lastElement); 
Baltic Sea
```

### Removing an element from the beginning of an array

要从数组开头删除元素，可以使用 shift() 方法：

```js
let seas = ['Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea'];
const firstElement = seas.shift();

console.log(firstElement);
Black Sea
```

### Finding an index of an element in the array

要查找元素的索引，可以使用 indexOf() 或 findIndex() 方法：

```js
let seas = ['Black Sea', 'Caribbean Sea', 'North Sea', 'Baltic Sea'];
let index = seas.indexOf('North Sea');
console.log(index); // 2
```

### Check if a value is an array

要检查值是否为数组，请使用 Array.isArray() 方法：

```js
console.log(Array.isArray(seas)); // true
```

## Array-like Object

在 JavaScript 中，"伪数组"（array-like object）是指具有类似数组的特性，但不是真正的数组对象的对象。它们通常具有一个 `length` 属性和一系列按顺序排列的数字索引属性，但没有继承自 `Array` 的方法。伪数组在 JavaScript 中经常出现，例如函数的参数对象 `arguments`、DOM 元素列表、NodeList、以及某些原生 API 返回的结果等。

伪数组的键通常是数字，而不是字符串。这是因为伪数组通常用于模拟数组的行为，其中索引是数字，并且根据数字索引来访问元素。

```js
let arrayLike = {
  0: 'foo',
  1: 'bar',
  2: 'baz',
  length: 3
};

console.log(arrayLike[0]); // 输出 'foo'
console.log(arrayLike[1]); // 输出 'bar'
console.log(arrayLike[2]); // 输出 'baz'
console.log(arrayLike.length); // 输出 3
```

虽然键的类型是数字，但 JavaScript 中的对象属性名可以是字符串或者符号，因此 JavaScript 引擎会自动将数字索引属性转换为字符串形式存储。

可以使用 Array.from() 方法将一个 array-like 对象转化为数组对象。
