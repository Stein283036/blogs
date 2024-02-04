# JavaScript BigInt

## Introduction to the JavaScript BigInt

ES2020 引入了一个名为 BigInt 的新内置对象，表示大于 2^53 - 1 的整数。

bigint 是基本类型，如 number、string、symbol、boolean、undefined 和 null。

要创建 BigInt，将 n 附加到数字字面量的末尾：

```js
let bigInt = 9007199254740991n;
```

或者，可以调用函数 BigInt()：

```js
let bigInt = BigInt(9007199254740991);
```

```js
let x = Number.MAX_SAFE_INTEGER;
x = x + 1; // 9007199254740992
x = x + 1; // 9007199254740992 (same as above)
```

```js
let x = BigInt(Number.MAX_SAFE_INTEGER);
x = x + 1n; // 9007199254740992n
x = x + 1n; // 9007199254740993n (correct now)
```

### Type

BigInt 的类型是bigint。

```js
console.log(typeof bigInt); // bigint
console.log(typeof BigInt(100) === 'bigint'); // true
```

### Operators

The `BigInt` supports the following operator `+`, `*`, `-`, `**`, `%`, bitwise operators except `>>>` (zero-fill right shift). It doesn’t support the unary operator (`+`).

The `/` operator will also work with the whole numbers. However, the result will not return any fractional digits. 

```js
let result = 3n / 2n;
console.log(result); // 1n, not 1.5n
```

### Comparisons

A `BigInt` is not strictly equal (`===`) to a `Number`:

```js
console.log(1n === 1); // false
```

However, a `BigInt` is loosely equal to a number when you use the `==` operator:

```js
console.log(1n == 1); // true
```

可以使用 <、<=、>、>= 将 BigInt 与 Number 进行比较：

```js
console.log(1n < 2); // true
console.log(2n > 1); // true
console.log(2n >= 2); // true
```

### Conditionals

BigInt 通过 if 语句或逻辑运算符 ||、&&、! 等条件中的 Boolean() 函数转换为布尔值。换句话说，在这些情况下它的工作方式就像一个数字。

```js
let count = 0n;

if(count) {
    console.log(true);
} else {
    console.log(false);
}
```