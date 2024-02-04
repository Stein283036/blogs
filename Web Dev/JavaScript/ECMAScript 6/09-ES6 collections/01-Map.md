# JavaScript Map Object

## Introduction to JavaScript Map object

在 ES6 之前，经常使用 oject 来模拟 map，将键映射到任意类型的值。但是使用 object 作为 map 有一些副作用：

1. An object always has a default key like the prototype.
2. A key of an object must be a **string or a symbol**, you cannot use an object as a key.
3. An object does not have a property that represents the size of the map.

ES6 提供了一种名为 Map 的新集合类型来解决这些缺陷。

根据定义，Map 对象保存键值对。键在 Map 集合中是唯一的。换句话说，Map 对象中的键仅出现一次。

Map 的键和值可以是任何类型的值。

When iterating a `Map` object, each iteration returns a 2-member array of `[key, value]`. The iteration order follows the insertion order which corresponds to the order in which each key-value pair was first inserted into the Map by the `set()` method.

创建 Map 的语法：

```js
let map = new Map([iterable]);
```

Map() 接受一个可选的可迭代对象，其元素是键值对。

## Useful JavaScript Map methods

- `clear()` – removes all elements from the map object.
-  `delete(key)` – removes an element specified by the key. It returns if the element is in the map, or false if it does not.
-  `entries()` – returns a new Iterator object that contains an array of `[key, value]` for each element in the map object. The order of objects in the map is the same as the insertion order.
-  `forEach(callback[, thisArg])` – invokes a callback for each key-value pair in the map in the insertion order. The optional thisArg parameter sets the `this` value for each callback.
-  get(key) – returns the value associated with the key. If the key does not exist, it returns undefined.
-  has(key) – returns true if a value associated with the key exists or false otherwise.
-  `keys()` – returns a new Iterator that contains the keys for elements in insertion order.
-  `set(key, value)` – sets the value for the key in the map object. It returns the map object itself therefore you can chain this method with other methods.
-  `values()` returns a new iterator object that contains values for each element in insertion order.

## JavaScript Map examples

### Create a new Map object

有一个 user 对象列表：

```js
let john = {name: 'John Doe'},
    lily = {name: 'Lily Bush'},
    peter = {name: 'Peter Drucker'};
```

假设需要创建 user 和 role 的映射：

```js
let userRoles = new Map();
```

userRoles 是 Map 对象的实例，其类型是对象：

```js
console.log(typeof(userRoles)); // object
console.log(userRoles instanceof Map); // true
```

### Add elements to a Map

To assign a role to a user, use the `set()` method:

```js
userRoles.set(john, 'admin');
```

The `set()` method maps user `john` with the `admin` role. set() 方法返回 Map 对象，因此可以链式调用：

```js
userRoles.set(lily, 'editor')
          .set(peter, 'subscriber');
```

### Initialize a map with an iterable object

```js
let userRoles = new Map([
    [john, 'admin'],
    [lily, 'editor'],
    [peter, 'subscriber']
]);
```

### Get an element from a map by key

```js
userRoles.get(john); // admin
```

如果传递的键不存在，则 get() 方法将返回 undefined。

```js
let foo = {name: 'John Doe'};
userRoles.get(foo); //undefined
```

### Check the existence of an element by key

要检查 map 中是否存在某个 key，使用 has() 方法。

```js
userRoles.has(foo); // false
userRoles.has(lily); // true
```

### Get the number of elements in the map

The `size` property returns the number of entries (key-value pair) of the Map object.

```js
console.log(userRoles.size); // 3
```

### Iterate over map keys

To get the keys of a `Map` object, you use the `keys()` method. The `keys()` returns a new iterator object that contains the keys of elements in the map.

```js
let john = { name: 'John Doe' },
  lily = { name: 'Lily Bush' },
  peter = { name: 'Peter Drucker' };

let userRoles = new Map([
  [john, 'admin'],
  [lily, 'editor'],
  [peter, 'subscriber'],
]);

for (const user of userRoles.keys()) {
  console.log(user.name);
}
```

### Iterate over map values

使用 values() 方法来获取包含 map 中所有元素的值的迭代器对象：

```js
let john = { name: 'John Doe' },
  lily = { name: 'Lily Bush' },
  peter = { name: 'Peter Drucker' };

let userRoles = new Map([
  [john, 'admin'],
  [lily, 'editor'],
  [peter, 'subscriber'],
]);

for (let role of userRoles.values()) {
  console.log(role);
}
```

### Iterate over map elements

entries() 方法返回一个迭代器对象，其中包含 Map 对象中每个元素的 [key,value] 数组：

```js
let john = { name: 'John Doe' },
  lily = { name: 'Lily Bush' },
  peter = { name: 'Peter Drucker' };

let userRoles = new Map([
  [john, 'admin'],
  [lily, 'editor'],
  [peter, 'subscriber'],
]);

for (const [user, role] of userRoles.entries()) {
  console.log(`${user.name}: ${role}`);
}
```

除了 for...of 循环之外，还可以使用 map 对象的 forEach() 方法：

```js
let john = { name: 'John Doe' },
  lily = { name: 'Lily Bush' },
  peter = { name: 'Peter Drucker' };

let userRoles = new Map([
  [john, 'admin'],
  [lily, 'editor'],
  [peter, 'subscriber'],
]);
// forEach() 接收的第一个回调函数的参数是 value key
userRoles.forEach((role, user) => console.log(`${user.name}: ${role}`));
```

### Convert map keys or values to an array

```js
const users = [...userRoles.keys()];
console.log(users);
```

```js
const roles = [...userRoles.values()];
console.log(roles);
```

### Delete an element by key

要删除 map 中的 entry，使用 delete() 方法。

```js
userRoles.delete(john);
```

### Delete all elements in the map

```js
userRoles.clear();
console.log(userRoles.size); // 0
```

## WeakMap

WeakMap 与 Map 类似，只是 WeakMap 的 key 必须是对象。这意味着当对某个 key（对象）的引用超出作用域时，相应的 value 会自动从内存中释放。

A `WeakMap` only has subset methods of a `Map` object:

-  `get(key)`
-  `set(key, value)`
-  `has(key)`
-  `delete(key)`

Map 和 WeekMap 之间的主要区别：

- Elements of a WeakMap cannot be iterated.
- Cannot clear all elements at once.
- Cannot check the size of a WeakMap.