# JavaScript Private Fields

## Introduction to the JavaScript private fields

ES2022 允许为类定义私有字段。要定义私有字段，请在字段名称前添加 # 符号。

例如，以下定义了具有私有字段 radius 的 Circle 类：

```js
class Circle {
  #radius;
  constructor(value) {
    this.#radius = value;
  }
  get area() {
    return Math.PI * Math.pow(this.#radius, 2);
  }
}
```

下面创建了 Circle 类的一个新实例并计算其面积：

```js
let circle = new Circle(10);
console.log(circle.area); // 314.1592653589793
```

由于 #radius 是私有字段，因此只能在 Circle 类中访问它。换句话说，#radius 字段在 Circle 类之外是不可见的。

## Using getter and setter to access private fields

下面通过添加 radius 的 getter 和 setter 来重新定义 Circle 类，以提供对 #radius 私有字段的访问：

```js
class Circle {
  #radius = 0;
  constructor(radius) {
    this.radius = radius; // calling setter
  }
  get area() {
    return Math.PI * Math.pow(this.#radius, 2);
  }
  set radius(value) {
    if (typeof value === 'number' && value > 0) {
      this.#radius = value;
    } else {
      throw 'The radius must be a positive number';
    }
  }
  get radius() {
    return this.#radius;
  }
}
```

## Private fields and subclasses

私有字段只能在定义它们的类内部访问。此外，它们不能从子类访问。例如，以下定义了继承 Circle 类的 Cylinder 类：

```js
class Cylinder extends Circle {
  #height;
  constructor(radius, height) {
    super(radius);
    this.#height = height;

    // cannot access the #radius of the Circle class here
  }
}
```

如果尝试访问 Cylinder 类中的#radius 私有字段，将收到 SyntaxError。

## The `in` operator: check private fields exist

要检查对象在类中是否有私有字段，可以使用 in 运算符：

```js
fieldName in objectName
```

例如，以下代码将 hasRadius() 静态方法添加到 Circle 类，该方法使用 in 运算符检查 circle 对象是否具有 #radius 私有字段：

```js
class Circle {
  #radius = 0;
  constructor(radius) {
    this.radius = radius;
  }
  get area() {
    return Math.PI * Math.pow(this.radius, 2);
  }
  set radius(value) {
    if (typeof value === 'number' && value > 0) {
      this.#radius = value;
    } else {
      throw 'The radius must be a positive number';
    }
  }
  get radius() {
    return this.#radius;
  }
  static hasRadius(circle) {
    return #radius in circle;
  }
}

let circle = new Circle(10);

console.log(Circle.hasRadius(circle)); // true
```

## Static private fields

以下示例显示如何使用静态私有字段：

```js
class Circle {
  #radius = 0;
  static #count = 0;
  constructor(radius) {
    this.radius = radius; // calling setter
    Circle.#count++;
  }
  get area() {
    return Math.PI * Math.pow(this.radius, 2);
  }
  set radius(value) {
    if (typeof value === 'number' && value > 0) {
      this.#radius = value;
    } else {
      throw 'The radius must be a positive number';
    }
  }
  get radius() {
    return this.#radius;
  }
  static hasRadius(circle) {
    return #radius in circle;
  }
  static getCount() {
    return Circle.#count;
  }
}

let circles = [new Circle(10), new Circle(20), new Circle(30)];

console.log(Circle.getCount()); // 3
```