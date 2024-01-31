# Arrays

## Introduction to JavaScript arrays

在 JavaScript 中，数组是值的有序列表。每个值称为由索引指定的元素：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/08/JavaScript-Array.svg)

JavaScript 数组具有以下特征：

- 数组存储的元素类型可以不同
- 数组的大小是动态的并且自动增长

## Creating JavaScript arrays

JavaScript 为提供了两种创建数组的方法。

`Array` 构造函数：

```js
let scores = new Array();
```

如果知道数组将容纳的元素数量，则可以创建一个具有初始大小的数组，如下例所示：

```js
let scores = Array(10);
```

要创建数组并使用一些元素对其进行初始化，将元素作为逗号分隔列表传递到 Array() 构造函数中。

```js
let scores = new Array(9,10,8,7,6);
```

JavaScript 允许在使用 Array() 构造函数时省略 new 运算符。例如，以下语句创建 Artists 数组。

```js
let artists = Array();
```

在实践中，很少会使用 Array() 构造函数来创建数组。

创建数组的更优选方法是使用数组字面量表示法：

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

```js
let mountains = ['Everest', 'Fuji', 'Nanga Parbat'];
console.log(mountains.length); // 3
```

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

要查找元素的索引，可以使用indexOf()或findLastIndex()方法：

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



























