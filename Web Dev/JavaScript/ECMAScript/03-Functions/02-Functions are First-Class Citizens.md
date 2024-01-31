# JavaScript Functions are First-Class Citizens

## Storing functions in variables

函数是 JavaScript 中的一等公民。换句话说，可以像对待其他类型的值一样对待函数。

```js
function add(a, b) {
    return a + b;
}

let sum = add;
```

在赋值语句中，我们在添加标识符末尾不包含左括号和右括号。我们也不执行该函数，而是引用该函数。

通过这样做，我们可以有两种方法来执行同一个函数。例如我们可以正常调用如下：

```js
let result = add(10, 20);
```

或者，我们可以通过 sum 变量来使用所有 add() 函数，如下所示：

```js
let result = sum(10,20);
```

## Passing a function to another function

因为函数是值，所以可以将一个函数作为参数传递给另一个函数。

下面声明了带有三个参数的average()函数。第三个参数是一个函数：

```js
function average(a, b, fn) {
    return fn(a, b) / 2;
}
```

现在，可以将 sum 函数传递给average() 函数，如下所示：

```js
let result = average(10, 20, sum);
```

## Returning functions from functions

由于函数是值，因此可以从另一个函数返回一个函数。

下面的compareBy()函数返回一个通过属性比较两个对象的函数：

```js
function compareBy(propertyName) {
  return function (a, b) {
    let x = a[propertyName],
      y = b[propertyName];

    if (x > y) {
      return 1;
    } else if (x < y) {
      return -1;
    } else {
      return 0;
    }
  };
}
```

假设有一个产品对象数组，其中每个产品对象都有两个属性：name 和 price。

```js
let products = [
    {name: 'iPhone', price: 900},
    {name: 'Samsung Galaxy', price: 850},
    {name: 'Sony Xperia', price: 700}
];
```

可以通过调用 sort() 方法对数组进行排序。 sort() 方法接受一个比较数组的两个元素的函数作为参数。

```js
console.log('Products sorted by name:');
products.sort(compareBy('name'));

console.table(products);
```









