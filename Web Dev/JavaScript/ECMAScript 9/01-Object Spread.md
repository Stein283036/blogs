## JavaScript Object Spread

在 ES6 中，可以使用扩展运算符 (...) 来解包数组的元素。ES2018 扩展了展开运算符 (...)，使其能够与对象自身的可枚举属性一起使用。假设您有一个具有一个属性 radius 的 circle 对象：

```js
const circle = {
    radius: 10
};
```

以下示例使用展开运算符 (...) 创建一个 colorCircle 对象，该对象具有 circle 对象的所有属性以及一个附加属性 color：

```js
const coloredCircle = {
    ...circle,
    color: 'black'
};
console.log(coloredCircle);
// 输出
{
    radius: 10,
    color: 'black'
}
```

### JavaScript Object spread operator use cases

#### clone an object

可以使用扩展运算符来克隆对象自己的**可枚举**属性：

```js
const circle = {
    radius: 10
};

const clonedCircle = {...circle};

console.log(clonedCircle); // { radius: 10 }
```

请注意，克隆始终是浅克隆。

```js
const circle = {
    radius: 10,
    style: {
        color: 'blue'
    }
};
const clonedCircle = {
    ...circle
};
circle.style.color = 'red';
console.log(clonedCircle.style.color); // red
```

#### Merging objects

```js
const circle = {
    radius: 10
};
const style = {
    backgroundColor: 'red'
};
const solidCircle = {
    ...circle,
    ...style
};
console.log(solidCircle); // { radius: 10, backgroundColor: 'red' }
```

### Spread operator vs. `Object.assign()`

展开运算符 (...) 在目标对象中定义新属性，而 Object.assign() 方法则对它们进行分配。它有两个副作用。

#### Target objects with setters

Object.assign() 调用目标对象上的 setter，而展开运算符则不会。

```js
class Circle {
    constructor(radius) {
        this.radius = radius;
    }
    set diameter(value) {
        this.radius = value / 2;
        console.log('SET ', value);
    }
    get diameter() {
        return this.radius * 2;
    }
}

let circle = new Circle(100);
let cloneCircle1 = Object.assign(circle, {
    diameter: 200
});
let cloneCircle2 = {
    ...circle
};
// 输出
SET  200
```

#### Target objects with read-only properties

如果目标对象具有只读属性，则无法使用 Object.assign() 方法为该属性分配新值。但是，展开运算符 (...) 可以定义新属性。假设您有一个名为 blueSquare 的对象，其颜色属性是只读的：

```js
const blueSquare = {
    length: 100,
    color: 'blue'
};

Object.defineProperty(blueSquare, 'color', {
    value: 'blue',
    enumerable: true,
    writable: false

});

console.log(blueSquare); // { length: 100, color: 'blue' }
```

下面使用展开运算符 (...) 来合并style和 blueSquare 对象：

```js
// merge style and blueSquare objects:
const style = {
    color: 'green'
};

const greenSquare = {
    ...blueSquare,
    ...style
};

console.log(greenSquare); // { length: 100, color: 'green' }
```

然而，如果使用Object.assign()方法，你会得到一个错误：

```js
// merge style and redSquare objects: ERROR
const redSquare = Object.assign(blueSquare, {
    color: 'red'
});
TypeError: Cannot assign to read only property 'color' of object '#<Object>'
```