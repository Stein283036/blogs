## Nullish Coalescing Operator

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