## Nullish Coalescing Operator

纵观 JavaScript 发展史，或 `||` 运算符先于 `??` 出现。它自 JavaScript 诞生就存在了，因此开发者长期将其用于这种目的。

另一方面，空值合并运算符 `??` 是最近才被添加到 JavaScript 中的，它的出现是因为人们对 `||` 不太满意。

它们之间重要的区别是：

- `||` 返回第一个 **真** 值。
- `??` 返回第一个 **已定义的** 值。

换句话说，`||` 无法区分 `false`、`0`、空字符串 `""` 和 `null/undefined`。它们都一样 —— 假值（falsy values）。

### Introduction to the JavaScript nullish coalescing operator

ES2020 引入了用双问号 (??) 表示的空合并运算符。空合并运算符是一个接受两个值的逻辑运算符：

```js
value1 ?? value2
```

The nullish coalescing operator returns the second value (`value2`) if the first value (`value2`) is `null` or `undefined`. Technically, the nullish coalescing operator is equivalent to the following block:

```js
const result = value1;
if(result === null || result === undefined) {
   result = value2;
}
```

> A nullish value is a value that is either `null` or `undefined`.

```js
const name = null ?? 'John';
console.log(name); // 'John'
```

### The nullish coalescing operator is short-circuited

Similar to the logical OR and AND operators, the nullish coalescing operator does not evaluate the second value if the first operand is neither undefined nor null.

```js
let result = 1 ?? console.log('Hi');
```

In this example, the operator `??` does not evaluate the second expression that displays the “Hi” to the console because the first value is `1`, which is not `null` or `undefined`.

### Chaining with the AND or OR operator

A `SyntaxError` will occur if you combine the logical AND or OR operator directly with the nullish coalescing operator like this:

```js
const result = null || undefined ?? 'OK'; // SyntaxError
```

However, you can avoid this error by wrapping the expression on the left of the `??` operator in parentheses to explicitly specify the operator precedences:

```js
const result = (null || undefined) ?? 'OK'; 
console.log(result); // 'OK'
```