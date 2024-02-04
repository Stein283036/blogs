# JavaScript Object.assign()

Object.assign() 方法的语法：

```js
Object.assign(target, ...sources)
```

Copy the values of all of the enumerable own properties from one or more source objects to a target object. Returns the target object.

Object.assign() 调用源对象上的 getter 和目标对象上的 setter。It assigns properties only, not copying or defining new properties.

## Using JavaScript Object.assign() to clone an object

以下示例使用 Object.assign() 方法克隆对象。

```js
let widget = {
    color: 'red'
};

let clonedWidget = Object.assign({}, widget);

console.log(clonedWidget);
```

`Object.assign()` 方法执行的是浅拷贝（shallow copy），即只复制对象的属性的引用而不是属性的值。如果源对象的属性值是对象或数组等引用类型，那么目标对象的属性将与源对象的属性共享相同的引用，因此对其中一个对象的修改会影响另一个对象。

## Using JavaScript Object.assign() to merge objects

Object.assign() 可以将源对象合并为目标对象，目标对象的属性由所有源对象的属性组成。

```js
let box = {
    height: 10,
    width: 20
};
let style = {
    color: 'Red',
    borderStyle: 'solid'
};
let styleBox = Object.assign({}, box, style);
console.log(styleBox); // { height: 10, width: 20, color: 'Red', borderStyle: 'solid' }
```

如果源对象具有相同的属性，则后一个对象的属性将覆盖前一个对象的属性：

```js
let box = {
    height: 10,
    width: 20,
    color: 'Red'
};
let style = {
    color: 'Blue',
    borderStyle: 'solid'
};
let styleBox = Object.assign({}, box, style);
console.log(styleBox); // { height: 10, width: 20, color: 'Blue', borderStyle: 'solid' }
```