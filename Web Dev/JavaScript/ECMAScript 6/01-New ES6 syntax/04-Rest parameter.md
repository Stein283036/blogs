# JavaScript Rest Parameters

## Introduction to JavaScript rest parameters

ES6 提供了一种新的参数，称为 rest parameter，其前缀为三个点 (...)。rest parameter 允许将不定数量的参数表示为数组。

```js
function fn(a,b,...args) {
   //...
}
```

最后一个参数 (args) 以三个点 (...) 为前缀。它称为 rest parameter。

传递给函数的所有实参都将映射到参数列表。在上面的语法中，第一个参数映射到 a，第二个参数映射到 b，第三个、第四个等将作为数组存储在 rest parameter args 中。

```js
fn(1, 2, 3, "A", "B", "C");
```

args 数组存储以下值：

```js
[3,'A','B','C']
```

如果仅传递前两个参数，则 rest parameter 将为空数组：

```js
fn(1,2);
```

注意，rest parameter 必须出现在参数列表的末尾。以下代码将导致错误：

```js
function fn(a,...rest, b) {
 // error
}
SyntaxError: Rest parameter must be last formal parameter
```

## More JavaScript rest parameters examples

```js
function sum(...args) {
    let total = 0;
    for (const a of args) {
        total += a;
    }
    return total;
}

sum(1, 2, 3); // 6
```

在此示例中，args 在数组中。因此，可以使用 for..of 循环来迭代其元素并对它们求和。

假设 sum() 函数的调用者可以传递各种数据类型的参数，例如数字、字符串和布尔值，并且只想计算数字的总和：

```js
function sum(...args) {
  return args
    .filter(function (e) {
      return typeof e === 'number';
    })
    .reduce(function (prev, curr) {
      return prev + curr;
    });
}
```

以下脚本使用新的 sum() 函数仅对数字参数求和：

```js
let result = sum(10,'Hi',null,undefined,20); 
console.log(result); // 30
```

如果没有 rest parameter，必须使用函数的 arguments 对象。

但是，arguments 对象本身并不是 Array 类型的实例。因此，不能直接使用 filter() 方法。在 ES5 中，必须使用 Array.prototype.filter.call()，如下所示：

```js
function sum() {
  return Array.prototype.filter
    .call(arguments, function (e) {
      return typeof e === 'number';
    })
    .reduce(function (prev, curr) {
      return prev + curr;
    });
}
```

rest 参数使代码更加优雅。假设需要根据特定类型（例如数字、字符串、布尔值和 null）过滤参数。

```js
function filterBy(type, ...args) {
  return args.filter(function (e) {
    return typeof e === type;
  });
}
```

## JavaScript rest parameters and arrow function

箭头函数没有 arguments 对象。因此，如果要向箭头函数传递一些参数，则必须使用 rest parameter。

```js
const combine = (...args) => {
  return args.reduce(function (prev, curr) {
    return prev + ' ' + curr;
  });
};
// const combine = (...args) => args.reduce((prev, curr) => `${prev} ${curr}`)

let message = combine('JavaScript', 'Rest', 'Parameters'); // =>
console.log(message); // JavaScript Rest Parameters
```

## JavaScript rest parameter in a dynamic function

JavaScript 可以通过 Function 构造函数创建动态函数。并且可以在动态函数中使用 rest parameter。

```js
var showNumbers = new Function('...numbers', 'console.log(numbers)');
showNumbers(1, 2, 3); // [ 1, 2, 3 ]
```
