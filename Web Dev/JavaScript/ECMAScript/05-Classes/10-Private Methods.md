# JavaScript Private Methods

## Introduction to JavaScript private methods

默认情况下，类的成员是 public 范围。 ES2020 引入了私有成员，包括私有字段和方法。

要将公共方法设为私有，请在其名称前加上 #。 JavaScript 允许为实例方法、静态方法和 getter/setter 定义私有方法。

下面显示了定义私有实例方法的语法：

```js
class MyClass {
  #privateMethod() {
    //...
  }
}
```

在此语法中，#privateMethod 是私有实例方法。只能在MyClass内部调用。换句话说，不能从类外部或MyClass的子类中调用它。

要在 MyClass 中调用 #privateMethod，请使用 this 关键字，如下所示：

```js
this.#privateMethod();
```

下面说明了定义私有静态方法的语法：

```js
class MyClass {
  static #privateStaticMethod() {
    //...
  }
}
```

要在 MyClass 内调用 #privateStaticMethod()，使用类名而不是 this 关键字：

```js
MyClass.#privateStaticMethod();
```

下面显示了私有 getter/setter 的语法：

```js
class MyClass {
  #field;
  get #field() {
      return #field;
  }
  set #field(value){
      #field = value;
  }
}
```

在此示例中，#field 是私有 getter 和 setter，提供对私有字段 #field 的访问。

在实践中，可以使用私有方法来最大限度地减少对象公开的方法数量。

根据经验，应该首先默认将所有类方法设为私有。然后，每当对象需要使用该方法与其他对象交互时，就将方法设为公共。

## JavaScript private method examples

### Private instance method example

下面说明如何使用私有实例方法定义 Person 类：

```js
class Person {
  #firstName;
  #lastName;
  constructor(firstName, lastName) {
    this.#firstName = firstName;
    this.#lastName = lastName;
  }
  getFullName(format = true) {
    return format ? this.#firstLast() : this.#lastFirst();
  }

  #firstLast() {
    return `${this.#firstName} ${this.#lastName}`;
  }
  #lastFirst() {
    return `${this.#lastName}, ${this.#firstName}`;
  }
}

let person = new Person('John', 'Doe');
console.log(person.getFullName()); // John Doe
```

### Private static method example

以下代码将 #validate() 私有静态方法添加到 Person 类：

```js
class Person {
  #firstName;
  #lastName;
  constructor(firstName, lastName) {
    this.#firstName = Person.#validate(firstName);
    this.#lastName = Person.#validate(lastName);
  }
  getFullName(format = true) {
    return format ? this.#firstLast() : this.#lastFirst();
  }
  static #validate(name) {
    if (typeof name === 'string') {
      let str = name.trim();
      if (str.length >= 3) {
        return str;
      }
    }
    throw 'The name must be a string with at least 3 characters';
  }

  #firstLast() {
    return `${this.#firstName} ${this.#lastName}`;
  }
  #lastFirst() {
    return `${this.#lastName}, ${this.#firstName}`;
  }
}

let person = new Person('John', 'Doe');
console.log(person.getFullName());
```
