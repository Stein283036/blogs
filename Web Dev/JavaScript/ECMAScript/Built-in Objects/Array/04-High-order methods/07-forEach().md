# JavaScript Array forEach: Executing a Function on Every Element

## Introduction to JavaScript Array `forEach()` method

Typically, when you want to execute a function on every element of an array, you use a for loop statement.

```js
let ranks = ['A', 'B', 'C'];
for (let i = 0; i < ranks.length; i++) {
    console.log(ranks[i]);
}
```

JavaScript Array provides the `forEach()` method that allows you to run a function on every element.

```js
let ranks = ['A', 'B', 'C'];
ranks.forEach(function (e) {
    console.log(e);
});
```

The `forEach()` method iterates over elements in an array and executes a predefined function once per element.

forEach() 方法的语法：

```js
forEach(callbackfn: (value: any, index: number, array: any[]) => void, thisArg?: any): void
// callbackfn: A function that accepts up to three arguments. forEach calls the callbackfn function one time for each element in the array.
// An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
// Performs the specified action for each element in an array.
```

与 for 循环相比，forEach() 方法的一个限制是不能使用 break 或 continue 语句来控制循环。

要终止 forEach() 方法中的循环，必须在回调函数内抛出异常。









