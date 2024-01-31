# Numbers

JavaScript uses the `number` type to represent both integers and floating-point values. Technically, the JavaScript `number `type uses the **IEEE-754** format.

ES2020 引入了一种新的原始类型 bigint ，表示值大于 2^53^ – 1 的大整数。

## Integer numbers

声明一个保存十进制整数的变量：

```js
let counter = 100;
```

整数可以用以下格式表示：

- Octal (base 8)
- Hexadecimal (based 16)

当您在算术运算中使用八进制和十六进制数时，JavaScript 将它们视为十进制数。

### Binary Numbers

在 ES5 中，JavaScript 没有提供任何二进制数字的字面形式。

要解析二进制字符串，使用 parseInt() 函数，如下所示：

```js
let e = parseInt('111',2);
console.log(e); // 7
```

ES6 通过使用 0b 前缀后跟一系列二进制数字（0 和 1）来添加对二进制文字的支持。

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

可以在非严格模式下使用八进制文字。如果在严格模式下使用它们，JavaScript 将抛出错误。

```js
"use strict"
let b = 058; // invalid octal 
console.log(b);
SyntaxError: Decimals with leading zeros are not allowed in strict mode.
```

这种隐式行为可能会导致问题。因此，ES6 引入了一种新的八进制文字，它以 0o 开头，后跟一系列八进制数字（从 0 到 7）。例如：

```js
let num = 0o71;
console.log(num);
57
```

如果 0o 之后有无效数字，JavaScript 将发出如下语法错误：

```js
let num = 0o80;
console.log(num);
let num = 0o80;
          ^^
SyntaxError: Invalid or unexpected token
```

### Hexadecimal numbers

十六进制数字以 0x 或 0X 开头，后跟任意数量的十六进制数字（0 到 9、a 到 f）。

```js
let num = 0x1a;
console.log(num);
26
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
console.log(amount);
31400000
```

此外，JavaScript 会自动将小数点后至少有六个零的任何浮点数转换为E记数法。

```js
let amount = 0.0000005;
console.log(amount);
5e-7
```

浮点数精确到小数点后 17 位。当您对浮点数执行算术运算时，通常会得到近似结果。

```js
let amount = 0.2 + 0.1;
console.log(amount);
0.30000000000000004
```

## Big Integers

JavaScript 从 ES2022 开始引入了 bigint 类型。bigint 类型存储值大于 2^53^ – 1 的整数，bigint 类型只能与 bigint 类型进行算数运算。

大整数文字的末尾有 n 字符，如下所示：

```js
let pageView = 9007199254740991n;
```





























