# JavaScript Object.is()

Object.is() 的行为类似于 === 运算符，但有两点不同：

- -0 and +0
- NaN

```js
console.log(Object.is(+0, -0)) // false
console.log(+0 === -0) // true
console.log(Object.is(NaN, NaN)) // true
console.log(NaN === NaN) // false
```