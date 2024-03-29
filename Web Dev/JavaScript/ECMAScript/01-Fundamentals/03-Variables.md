# Variables

## Declare a variable

声明变量可以使用：

- `var`
- `let`
- `const`

```javascript
var message;
```

默认情况下，如果尚未为其分配值，则变量具有 `undefined` 的特殊值。

JavaScript 是一种动态类型语言。这意味着不需要像其他静态类型语言那样在声明中指定变量的类型。

## Variable Naming Convention

## Initialize a variable

JavaScript 允许使用单个语句声明两个或多个变量。要分隔两个变量声明，可以使用逗号 (,)，如下所示：

```js
let message = "Hello",
    counter = 100;
```

## Constants

常量保存一个不会改变的值。要声明常量，可以使用 const 关键字。定义常量时，必须用一个值对其进行初始化。一旦定义了常量，就无法更改其值。
