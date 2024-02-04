# A Quick Look at Octal and Binary Literals in ES6

ES5 提供了八进制（前缀 0）、十进制（无前缀）和十六进制 (0x) 的数字字面量。 ES6 添加了对二进制数字字面量的支持，并更改了它表示八进制数字字面量的方式。

## Octal literals

要在 ES5 中表示八进制字面量，使用零前缀 (0)，后跟八进制数字序列（从 0 到 7）：

> 浏览器的严格模式下以及在 Node.js 中前导 0 是非法的。
>
> ```js
> SyntaxError: Decimals with leading zeros are not allowed in strict mode.
> ```

```js
let a = 051;
console.log(a); // 41
```

如果八进制文字包含超出范围的数字，JavaScript 会忽略前导 0 并将八进制字面量视为十进制：

```js
let b = 058; // invalid octal
console.log(b); // 58
```

ES6 允许使用前缀 0o 后跟从 0 到 7 的八进制数字序列来指定八进制字面量：

```js
let c = 0o51;
console.log(c); // 41 
```

如果在八进制字面量中使用无效数字，JavaScript 将抛出语法错误：

```js
SyntaxError: Invalid or unexpected token
```

## Binary literals

在 ES5 中，JavaScript 没有提供任何二进制数字的字面量形式。要解析二进制字符串，使用 parseInt() 函数：

```js
let e = parseInt('111',2);
console.log(e); // 7
```

ES6 通过使用 0b 前缀后跟一系列二进制数字（0 和 1）来添加对二进制字面量的支持。

```js
let f = 0b111;
console.log(f); // 7
```