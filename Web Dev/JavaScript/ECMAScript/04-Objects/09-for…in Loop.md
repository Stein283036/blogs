# JavaScript for…in Loop

## Introduction to JavaScript for…in loop

for...in 循环遍历由对象字符串作为键的可枚举属性。注意，属性可以通过字符串（string）或符号（symbol）作为键。

当属性的内部可枚举（enumerable）标志设置为 true 时，该属性是可枚举的。

当通过简单赋值或属性初始值设定项创建属性时，可枚举标志默认为 true：

```js
object.propertyName = value;

let obj = {
    propertyName: value,
    ...
};
```

for...in 循环的语法：

```js
for(const propertyName in object) {
    // ...
}
```

for...in 允许访问对象的每个可迭代属性和值，而无需知道属性的具体名称。例如：

```js
var person = {
    firstName: 'John',
    lastName: 'Doe',
    ssn: '299-24-2351'
};
for(var prop in person) {
    console.log(prop + ':' + person[prop]);
}
firstName:John
lastName:Doe
ssn:299-24-2351
```

## The `for...in` loop & Inheritance

When you loop over the properties of an object that inherits from another object, the `for...in` statement goes up in the prototype chain and enumerates inherited properties. Consider the following example:

```js
var decoration = {
    color: 'red'
};
var circle = Object.create(decoration);
circle.radius = 10;
for(const prop in circle) {
    console.log(prop);
}
radius
color
```

The `circle` object has its own prototype that references the `decoration` object. Therefore, the `for...in` loop displays the properties of the `circle` object and its prototype.

如果只想枚举对象自己的属性，可以使用 hasOwnProperty() 方法：

```js
for(const prop in circle) {
    if(circle.hasOwnProperty(prop)) {
        console.log(prop);
    }
}
radius
```

## The for…in loop and Array

最好不要使用 for...in 来迭代数组，特别是当数组元素的顺序很重要时。

下面的例子可以完美地工作：

```js
const items = [10 , 20, 30];
let total = 0;
for(const item in items) {
    total += items[item];
}
console.log(total); // 60
```

但是，有人可能会在其库中设置内置数组类型的属性，如下所示：

```js
Array.prototype.foo = 100;
```

因此，for...in 将无法正常工作。例如：

```js
// somewhere else
Array.prototype.foo = 100;
const items = [10, 20, 30];
let total = 0;
for (var prop in items) {
  console.log({ prop, value: items[prop] });
  total += items[prop];
}
console.log(total);
{ prop: '0', value: 10 }
{ prop: '1', value: 20 }
{ prop: '2', value: 30 }
{ prop: 'foo', value: 100 }
160
```

另一个例子：

```js
var arr = [];
// set the third element to 3, other elements are `undefined`
arr[2] = 3; 
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);    
}
// 输出显示了数组的三个元素，这是正确的：
undefined
undefined
3
```

但是，for...in 循环忽略前两个元素：

```js
for (const key in arr) {
    console.log(arr[key]);
}
// 3
```



































