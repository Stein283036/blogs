# JavaScript Prototype

## Introduction to JavaScript prototype

在 JavaScript 中，对象可以通过原型继承彼此的功能。每个对象都有自己的属性，称为 `prototype`。

因为原型本身也是另一个对象，所以原型有自己的原型。这创建了一个称为原型链的东西。当原型的自身原型为空时，原型链结束。

假设有一个对象 person，其属性名为 name：

```js
let person = {'name' : 'John'}
```

当在控制台中检查 person 对象时，您会发现 person 对象有一个名为 prototype 的属性，用 [[Prototype]] 表示：

![img](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\04-Objects\assets\JavaScript-Prototype.png)



原型本身是一个具有自己属性的对象：

![img](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\04-Objects\assets\JavaScript-Prototype-object.png)

当您访问对象的属性时，如果该对象具有该属性，它将返回该属性值。

但是，如果您访问对象中不存在的属性，JavaScript 引擎将在该对象的原型中搜索。

如果 JavaScript 引擎在对象的原型中找不到该属性，它将在原型的原型中搜索，直到找到该属性或到达原型链的末尾。

## JavaScript prototype illustration

JavaScript 具有内置的 Object() 函数。如果将 Object 函数传递给 typeof 运算符，则它会返回“function”。例如：

```js
typeof(Object) // 'function'
```

此外，JavaScript 提供了一个匿名对象，可以通过 Object() 函数的原型属性来引用：

```js
console.log(Object.prototype);
```

![img](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\04-Objects\assets\JavaScript-Prototype-Object.prototype.png)

Object.prototype 对象具有一些有用的属性和方法，例如 toString() 和 valueOf()。

Object.prototype 还有一个重要的属性：constructor，它引用 Object() 函数。

以下语句确认 Object.prototype.constructor 属性引用了 Object 函数：

```js
console.log(Object.prototype.constructor === Object); // true
```

首先，定义一个名为 Person 的构造函数，如下所示：

```js
function Person(name) {
    this.name = name;
}
```

在此示例中，Person() 函数接受一个 name 参数并将其分配给 this 对象的 name 属性。

JavaScript 在幕后创建了一个新函数 Person() 和一个匿名对象：

![JS prototype- Person type](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-Person-type.svg)

与 Object() 函数一样，Person() 函数有一个名为 prototype 的属性，该属性引用匿名对象。匿名对象具有引用 Person() 函数的构造函数属性。

![img](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\04-Objects\assets\JavaScript-Prototype-Person-function.png)

**此外，JavaScript 通过 [[Prototype]] 将 Person.prototype 对象链接到 Object.prototype 对象，这称为原型链接。**

原型链接在下图中用[[Prototype]]表示：

![JS prototype- Person prototype](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-Person-prototype.svg)

## Defining methods in the JavaScript prototype object

下面在 Person.prototype 对象中定义了一个名为greet()的新方法：

```js
Person.prototype.greet = function() {
    return "Hi, I'm " + this.name + "!";
}
```

在这种情况下，JavaScript引擎将greet()方法添加到Person.prototype对象中：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-method.svg)

以下创建了 Person 的一个新实例：

```js
let p1 = new Person('John');
```

在内部，JavaScript 引擎创建一个名为 p1 的新对象，并通过原型链接将 p1 对象链接到 Person.prototype 对象：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-Person-object.svg)

p1、Person.prototype 和 Object.protoype 之间的链接称为原型链。

以下代码调用 p1 对象上的greet()方法：

```js
let greeting = p1.greet();
console.log(greeting);
```

因为 p1 没有greet()方法，所以JavaScript遵循原型链接并在Person.prototype对象上找到它。

由于JavaScript可以在Person.prototype对象上找到greet()方法，因此它执行greet()方法并返回结果：

下面调用 p1 对象的 toString() 方法：

```js
let s = p1.toString();
console.log(s);
```

在这种情况下，JavaScript 引擎会沿着原型链在 Person.prototype 中查找 toString() 方法。

由于 Person.prototype 没有 toString() 方法，因此 JavaScript 引擎会向上查找原型链并在 Object.prototype 对象中搜索 toString() 方法。

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-calling-a-method.svg)

如果调用 Person.prototype 和 Object.prototype 对象上不存在的方法，JavaScript 引擎将遵循原型链，如果找不到该方法，则会抛出错误。例如：

```js
p1.fly();
```

由于fly()方法不存在于原型链中的任何对象上，因此JavaScript引擎会发出以下错误：

```js
TypeError: p1.fly is not a function
```

下面创建了 name 属性为“Jane”的 Person 的另一个实例：

```js
let p2 = new Person('Jane');
```

![JS prototype-two person objects](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-two-person-objects.svg)

p2 对象具有与 p1 对象相同的属性和方法。

总之，当你在原型对象上定义一个方法时，这个方法被所有实例共享。

## Defining methods in an individual object

下面定义了 p2 对象上的 draw() 方法。

```js
p2.draw = function () {
    return "I can draw.";
};
```

JavaScript 引擎将 draw() 方法添加到 p2 对象，而不是 Person.prototype 对象：

![JS prototype - object with method](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-object-with-method.svg)

这意味着只可以在 p2 对象上调用 draw() 方法：

```js
p2.draw();
```

但是你不能在 p1 对象上调用 draw() 方法：

```js
p1.draw()
TypeError: p1.draw is not a function
```

当您在对象中定义方法时，该方法仅对该对象可用。默认情况下它不能与其他对象共享。

## Getting prototype linkage

`__proto__` 发音为 dunder proto。 `__proto__` 是 Object.prototype 对象的访问器属性。它公开了访问它的对象的内部原型链接（[[Prototype]]）。

`__proto__ `已在 ES6 中标准化，以确保与 Web 浏览器的兼容性。但是，将来可能会弃用它，转而使用 Object.getPrototypeOf()。因此，永远不应该在生产代码中使用 `__proto__`。

`p1.__proto__ `公开引用 Person.prototype 对象的 [[Prototype]]。

同样，`p2.__proto__` 也引用与 `p1.__proto__` 相同的对象：

```js
console.log(p1.__proto__ === Person.prototype); // true
console.log(p1.__proto__ === p2.__proto__); // true
```

如前所述，应该使用 Object.getPrototypeOf() 方法而不是 `__proto__`。 Object.getPrototypeOf() 方法返回指定对象的原型。

```js
console.log(p1.__proto__ === Object.getPrototypeOf(p1)); // true
```

获取原型链接的另一种流行方法是当 Object.getPrototypeOf() 方法无法通过构造函数属性使用时，如下所示：

```js
p1.constructor.prototype
```

p1.constructor 返回 Person，因此 p1.constructor.prototype 返回原型对象。

## Shadowing

观察以下方法调用：

```js
console.log(p1.greet());
```

p1 对象没有定义greet() 方法，因此JavaScript 会沿着原型链查找它。在这种情况下，它可以在 Person.prototype 对象中找到该方法。

让我们向对象 p1 添加一个与 Person.prototype 对象中的方法同名的新方法：

```js
p1.greet = function() {
    console.log('Hello');
}
```

并调用greet()方法：

```js
console.log(p1.greet());
```

因为p1对象有greet()方法，JavaScript只是立即执行它，而无需在原型链中查找它。

这是 shadowing 的一个例子。 p1 对象的greet() 方法隐藏了p1 对象引用的原型对象的greet() 方法。