# JavaScript Number Type

## Introduction to JavaScript Number type

Besides the primitive number type, JavaScript also provides the `Number` reference type for numeric values.

要创建 Number 对象，使用 Number 构造函数并传入一个数字值，如下所示：

```js
let numberObject = new Number(100);
```

要从 Number 对象中获取原始值，使用 valueOf() 方法：

```js
console.log(numberObject.valueOf()); // 100
```

要获取字符串形式的数字值，使用 toString() 或 toLocaleString() 方法。

toString() 方法接受一个可选参数，该参数确定显示数字的基数。

```js
let aNumber = new Number(10);
console.log(aNumber.toString()); // "10"
console.log(aNumber.toString(2)); // "1010"
```

如果对 primitive number value 调用方法，JavaScript 会将其暂时转换为 Number 对象。此功能在 JavaScript 中称为原始包装类型。

```js
let x = 10;
console.log(x.toString(16)); // "a"
```

## Formatting numbers

要格式化具有指定小数位数的数字，使用 toFixed() 方法。

toFixed() 方法接受一个参数，该参数指示应使用多少个小数点。

```js
numberObject.toFixed(decimalPlaces);
```

toFixed() 方法使用定点表示法返回数字的相应字符串。

```js
let pi = 3.1415926

console.log(pi.toFixed(2)) // 3.14
console.log(pi.toFixed(3)) // 3.142
console.log(pi.toFixed(4)) // 3.1416
```

需要注意的是，网络浏览器可能会使用不同的舍入方法。因此，在使用 toFixed() 方法时应该小心，特别是对于处理货币值的应用程序。

要以 e-notation 格式化数字，使用 toExponential() 方法。

```js
let x = 10, y = 100, z = 1000;

console.log(x.toExponential());
console.log(y.toExponential());
console.log(z.toExponential());

// "1e+1"
// "1e+2"
// "1e+3"
```

要获取指定精度的数字对象的字符串表示形式，使用 toPrecision() 方法。

```js
numberObject.toPrecision(precision);
```

精度参数决定有效位数。

toPrecision() 方法以指数表示法或四舍五入到精确有效数字的定点形式返回 Number 对象的字符串表示形式。

```js
let x = 9.12345;

console.log(x.toPrecision());    // '9.12345'
console.log(x.toPrecision(4));   // '9.123'
console.log(x.toPrecision(3));   // '9.12'
console.log(x.toPrecision(2));   // '9.1'
console.log(x.toPrecision(1));   // '9'

let y = 123.5;
console.log(y.toPrecision(2)); // "1.2e+2"
```