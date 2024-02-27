# Numbers

JavaScript uses the `number` type to represent both integers and floating-point values. Technically, the JavaScript `number `type uses the **IEEE-754** format.

在内部，数字是以 64 位格式 IEEE-754 表示的，所以正好有 64 位可以存储一个数字：其中 52 位被用于存储这些数字，其中 11 位用于存储小数点的位置，而 1 位用于符号。

## Integer numbers

声明一个保存十进制整数的变量：

```js
let counter = 100;
```

整数可以用以下格式表示：

- Octal (base 8)
- Hexadecimal (based 16)

当您在算术运算中使用八进制和十六进制数时，JavaScript 将它们视为十进制数。

假如我们需要表示 10 亿。显然，我们可以这样写：

```javascript
let billion = 1000000000;
```

我们也可以使用下划线 `_` 作为分隔符：

```javascript
let billion = 1_000_000_000;
```

这里的下划线 `_` 扮演了“语法糖”的角色，使得数字具有更强的可读性。JavaScript 引擎会直接忽略数字之间的 `_`，所以 上面两个例子其实是一样的。

在 JavaScript 中，我们可以通过在数字后面附加字母 `"e"` 并指定零的个数来缩短数字：

```javascript
let billion = 1e9;  // 10 亿，字面意思：数字 1 后面跟 9 个 0

alert( 7.3e9 );  // 73 亿（与 7300000000 和 7_300_000_000 相同）
```

换句话说，`e` 把数字乘以 `1` 后面跟着给定数量的 0 的数字。

```javascript
1e3 === 1 * 1000; // e3 表示 *1000
1.23e6 === 1.23 * 1000000; // e6 表示 *1000000
```

现在让我们写一些非常小的数字。例如，1 微秒（百万分之一秒）：

```javascript
let mcs = 0.000001;
```

就像以前一样，可以使用 `"e"` 来完成。如果我们想避免显式地写零，我们可以这样写：

```javascript
let mcs = 1e-6; // 1 的左边有 6 个 0
```

### Binary Numbers

在 ES5 中，JavaScript 没有提供任何二进制数字的字面形式。

要解析二进制字符串，使用 parseInt() 函数，如下所示：

```js
let e = parseInt('111',2);
console.log(e); // 7
```

ES6 通过使用 0b 前缀后跟一系列二进制数字（0 和 1）来添加对二进制数字的支持。

```js
let f = 0b111;
console.log(f); // 7
```

### Octal numbers

八进制数字以数字零 (0) 开头，后跟一系列八进制数字（从 0 到 7 的数字）。

```js
let num = 071;
console.log(num);
57
```

如果八进制数包含不在 0 到 7 范围内的数字，JavaScript 引擎会忽略 0 并将该数字视为十进制。例如：

```js
let num = 080;
console.log(num);
80
```

可以在非严格模式下使用八进制数字。如果在严格模式下使用它们，JavaScript 将抛出错误。

```js
"use strict"
let b = 058; // invalid octal 
console.log(b);
SyntaxError: Decimals with leading zeros are not allowed in strict mode.
```

这种隐式行为可能会导致问题。因此，ES6 引入了一种新的八进制数字，它以 0o 开头，后跟一系列八进制数字（从 0 到 7）。例如：

```js
let num = 0o71;
console.log(num);
57
```

如果 0o 之后有无效数字，JavaScript 将发出如下语法错误：

```js
let num = 0o80;
console.log(num);
SyntaxError: Invalid or unexpected token
```

### Hexadecimal numbers

十六进制 数字在 JavaScript 中被广泛用于表示颜色，编码字符以及其他许多东西。

十六进制数字以 0x 或 0X 开头，后跟任意数量的十六进制数字（0 到 9、a 到 f）。

```js
let num = 0x1a;
console.log(num); // 26
```

## Floating-point numbers

要定义浮点字面量数字，需要包含一个小数点和其后至少一个数字。

```js
let price = 9.99;
let tax = 0.08;
let discount = .05; // valid but not recommeded
```

当数字非常大时，可以使用科学计数法 e。E 表示法表示一个数字应乘以 10 的给定幂。

```js
let amount = 3.14e7;
console.log(amount); // 31400000
```

此外，JavaScript 会自动将小数点后至少有六个零的任何浮点数转换为E记数法。

```js
let amount = 0.0000005;
console.log(amount); // 5e-7
```

浮点数精确到小数点后 17 位。当对浮点数执行算术运算时，通常会得到近似结果。

```js
let amount = 0.2 + 0.1;
console.log(amount); // 0.30000000000000004
```

## Big Integers

JavaScript 从 ES2022 开始引入了 bigint 类型，bigint 类型只能与 bigint 类型进行算数运算。

大整数数字的末尾有 n 字符，如下所示：

```js
let pageView = 9007199254740991n;
```
