# Demystifying the JavaScript this Keyword

在 JavaScript 中，可以在全局和函数上下文中使用 this 关键字。此外，this 关键字的行为在严格模式和非严格模式之间变化。

## What is this keyword

一般来说，this 引用该函数是其属性的对象。换句话说，this 引用当前正在调用该函数的对象。

假设有一个对象 counter，它有一个方法 next()。当调用next()方法时，就可以访问this对象。

```js
let counter = {
  count: 0,
  next: function () {
    return ++this.count;
  },
};

counter.next();
```

在 next() 函数中， this 引用计数器对象。请参阅以下方法调用：

```js
counter.next();
```

next() 是一个函数，它是 counter 对象的属性。因此，在 next() 函数内部， this 引用了计数器对象。

## Global context

在全局上下文中，this 引用全局对象，即 Web 浏览器上的 window 对象或 Node.js 上的全局对象。

此行为在严格模式和非严格模式下都是一致的。这是网络浏览器上的输出：

```js
console.log(this === window); // true
```

如果在全局上下文中为该对象分配属性，JavaScript 会将该属性添加到全局对象，如下例所示：

```js
this.color= 'Red';
console.log(window.color); // 'Red'
```

## Function context

在 JavaScript 中，可以通过以下方式调用函数：

- Function invocation
- Method invocation
- Constructor invocation
- Indirect invocation

每个函数调用都定义其自己的上下文。因此， this 的行为有所不同。

### Simple function invocation

在非严格模式下，函数调用时this引用全局对象，如下：

```js
function show() {
   console.log(this === window); // true
}

show();
```

当调用 show() 函数时， this 引用全局对象，该对象在 Web 浏览器中是 window ，在 Node.js 中是 global 。

调用 show() 函数与以下内容相同：

```js
window.show();
```

在严格模式下，JavaScript 将函数内的 this 设置为 `undefined`。例如：

```js
"use strict";
function show() {
    console.log(this === undefined);
}
show();
```

要启用严格模式，请在 JavaScript 文件的开头使用指令“use strict”。如果只想将严格模式应用于特定函数，请将其放置在函数体的顶部。

请注意，严格模式自 ECMAScript 5.1 起就可用。严格模式适用于函数和嵌套函数。例如：

```js
function show() {
    "use strict";
    console.log(this === undefined); // true
    function display() {
        console.log(this === undefined); // true
    }
    display();
}
show();
```

### Method invocation

当调用对象的方法时，JavaScript 将 this 设置为拥有该方法的对象。请参阅以下 `car` 对象：

```js
let car = {
    brand: 'Honda',
    getBrand: function () {
        return this.brand;
    }
}
console.log(car.getBrand()); // Honda
```

在此示例中，getBrand() 方法中的 this 对象引用了 car 对象。

由于方法是对象的属性值，因此可以将其存储在变量中。

```js
let brand = car.getBrand;
```

然后通过变量调用方法

```js
console.log(brand()); // undefined
```

你会得到 undefined 而不是“Honda”，因为当你调用一个方法而不指定其对象时，JavaScript 在非严格模式下将其设置为全局对象，在严格模式下将其设置为 undefined。

要解决此问题，可以使用 Function.prototype 对象的 bind() 方法。 bind() 方法创建一个新函数，该函数的 this 关键字设置为指定值。

```js
let brand = car.getBrand.bind(car);
console.log(brand()); // Honda
```

在此示例中，当调用brand()方法时，this关键字将绑定到 `car` 对象。例如：

```js
let car = {
    brand: 'Honda',
    getBrand: function () {
        return this.brand;
    }
}
let bike = {
    brand: 'Harley Davidson'
}
let brand = car.getBrand.bind(bike);
console.log(brand()); // Harley Davidson
```

在此示例中，bind() 方法将 this 设置为 `bike` 对象，因此，可以在控制台上看到 `bike` 对象的品牌属性的值。

### Constructor invocation

当使用 new 关键字创建函数对象的实例时，将该函数用作构造函数。

以下示例声明一个 Car 函数，然后将其作为构造函数调用：

```js
function Car(brand) {
    this.brand = brand;
}
Car.prototype.getBrand = function () {
    return this.brand;
}
let car = new Car('Honda');
console.log(car.getBrand());
```

表达式 new Car('Honda') 是 Car 函数的构造函数调用。

JavaScript 创建一个新对象并将 `this` 设置为新创建的对象。这种模式在只有一个潜在问题时效果很好。

现在，可以将 Car() 作为函数或构造函数调用。如果省略 new 关键字，如下所示：

```js
var bmw = Car('BMW');
console.log(bmw.brand);
// => TypeError: Cannot read property 'brand' of undefined
```

由于 Car() 中的 this 值设置为全局对象，因此 bmw.brand 返回  undefined。

为了确保始终使用构造函数调用来调用 Car() 函数，请在 Car() 函数的开头添加一个检查，如下所示：

```js
function Car(brand) {
    if (!(this instanceof Car)) {
        throw Error('Must use the new operator to call the function');
    }
    this.brand = brand;
}
```

ES6 引入了一个名为 new.target 的元属性，它允许检测函数是作为简单调用还是作为构造函数来调用。

```js
function Car(brand) {
    if (!new.target) {
        throw Error('Must use the new operator to call the function');
    }
    this.brand = brand;
}
```

### Indirect Invocation

在 JavaScript 中，函数是一等公民。换句话说，函数是对象，是 Function 类型的实例。

Function 类型有两个方法： call() 和 apply() 。这些方法允许在调用函数时设置 this 值。例如：

```js
function getBrand(prefix) {
    console.log(prefix + this.brand);
}
let honda = {
    brand: 'Honda'
};
let audi = {
    brand: 'Audi'
};
getBrand.call(honda, "It's a ");
getBrand.call(audi, "It's an ");
It's a Honda
It's an Audi
```

在此示例中，我们使用 getBrand 函数的 call() 方法间接调用 getBrand() 函数。我们将 honda 和 audi 对象作为 call() 方法的第一个参数传递，因此，我们在每次调用中都得到了相应的品牌。

apply() 方法与 call() 方法类似，只是它的第二个参数是参数数组。

```js
getBrand.apply(honda, ["It's a "]); // "It's a Honda"
getBrand.apply(audi, ["It's an "]); // "It's a Audi"
```

## Arrow function

ES6 引入了一个新概念，称为箭头函数。在箭头函数中，JavaScript 按词法设置 this。

这意味着箭头函数不会创建自己的执行上下文，而是从定义箭头函数的外部函数继承 this 。请参见以下示例：

```js
let getThis = () => this;
console.log(getThis() === window); // true
```

在此示例中， this 值设置为全局对象，即 Web 浏览器中的 window。

由于箭头函数不会创建自己的执行上下文，因此使用箭头函数定义方法会导致问题。例如：

```js
function Car() {
  this.speed = 120;
}
Car.prototype.getSpeed = () => {
  return this.speed;
};
var car = new Car();
console.log(car.getSpeed()); // 👉 undefined
```

在 getSpeed() 方法中， this 值引用全局对象，而不是 Car 对象，但全局对象没有名为 speed 的属性。因此，getSpeed()方法中的this.speed返回undefined。