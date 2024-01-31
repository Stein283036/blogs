# Numeric Separator

## JavaScript 数字分隔符简介

数字分隔符允许您使用下划线 (_) 作为分隔符在数字组之间创建视觉分隔。

例如，以下数字非常难以阅读，尤其是当它包含长数字重复时：

```js
const budget = 1000000000;
```

数字分隔符解决了这个可读性问题，如下所示：

```js
const budget = 1_000_000_000;
```

JavaScript 允许对整数和浮点数使用数字分隔符。例如：

```js
let amount = 120_201_123.05; // 120201123.05
let expense = 123_450; // 123450
let fee = 12345_00; // 1234500
```

需要注意的是，JavaScript 中的所有数字都是浮点数。

use the numeric separator for bigint literal, binary literal, octal literal, and hex literal. For example:

```js
// BigInt
const max = 9_223_372_036_854_775_807n;

// binary
let nibbles = 0b1011_0101_0101;

// octal
let val = 0o1234_5670;

// hex
let message = 0xD0_E0_F0;
```











