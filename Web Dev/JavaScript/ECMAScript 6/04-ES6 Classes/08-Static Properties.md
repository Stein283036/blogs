# JavaScript Static Properties

## Introduction to the JavaScript static properties

与静态方法一样，静态属性由类的所有实例共享。要定义静态属性，使用 static 关键字，后跟属性名称，如下所示：

```js
class Item {
  static count = 0;
}
```

要访问静态属性，使用类名后跟 . 运算符和静态属性名称。

```js
console.log(Item.count); // 0
```

要在类构造函数或实例方法中访问静态属性，使用以下语法：

```js
className.staticPropertyName;
```

以下示例在类构造函数中增加 count 静态属性：

```js
class Item {
  constructor(name, quantity) {
    this.name = name;
    this.quantity = quantity;
    Item.count++;
  }
  static count = 0;
  static getCount() {
    return Item.count;
  }
}

let pen = new Item("Pen", 5);
let notebook = new Item("notebook", 10);

console.log(Item.getCount()); // 2
```

此示例创建 Item 类的两个实例，这两个实例调用类构造函数。由于类构造函数每次调用时都会将 静态 count 属性加一，因此 count 的值为 2。
