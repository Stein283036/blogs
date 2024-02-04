# JavaScript Set Type in ES6

## Introduction to the JavaScript `Set` object

ES6 提供了一种新类型 Set，它存储任意类型的唯一值的集合。

```js
let setObject = new Set();
```

Set 构造函数还接受一个可选的可迭代对象。如果将可迭代对象传递给 Set 构造函数，则可迭代对象的所有元素都将添加到新集合中：

```js
let setObject = new Set(iterableObject);
```

## Useful `Set` methods

- `add(value)` – appends a new element with a specified value to the set. It returns the `Set` object, therefore, you can chain this method with another `Set` method.
- `clear()` – removes all elements from the `Set` object.
- `delete(value)` – deletes an element specified by the value.
- `entries()`– returns a new `Iterator` that contains an array of `[value, value]` .
- `forEach(callback [, thisArg])` – invokes a callback on each element of the `Set` with the `this` value sets to `thisArg` in each call.
- `has(value)` – returns `true` if an element with a given value is in the set, or `false` if it is not.
- `keys()` – is the same as `values()` function.
- `[@@iterator]` – returns a new `Iterator` object that contains values of all elements stored in the insertion order.

## JavaScript `Set` examples

### Create a new Set from an Array

```js
let chars = new Set(['a', 'a', 'b', 'c', 'c']);
```

Set 中的所有元素都必须是唯一的，因此 chars 仅包含 3 个不同的元素 a、b 和 c。

```js
console.log(chars); // Set { 'a', 'b', 'c' }
```

chars 是 Set 类型的实例，因此以下语句返回 true。

```js
let result = chars instanceof Set;
console.log(result);
```

### Get the size of a Set

要获取 Set 所包含的元素数量，可以使用 Set 对象的 size 属性：

```js
let size = chars.size;
console.log(size);//  3
```

### Add elements to a Set

```js
chars.add('d');
console.log(chars); // Set { 'a', 'b', 'c', 'd' }
```

由于 add() 方法是可链接的（返回 Set 对象），因此可以使用链语句添加多个元素到集合中：

```js
chars.add('e')
     .add('f');
```

### Check if a value is in the Set

要检查集合中是否具有特定元素，使用 has() 方法。如果集合包含该元素，has() 方法返回 true，否则返回 false。

```js
let exist = chars.has('a');
console.log(exist);// true
exist = chars.has('z');
console.log(exist); // false
```

### Remove elements from a set

```js
chars.delete('f');
console.log(chars); // Set {"a", "b", "c", "d", "e"}
```

delete() 方法返回 true 表示该元素已成功删除。要删除集合中的所有元素，可以使用 clear() 方法：

```js
chars.clear();
console.log(chars); // Set{}
```

### Looping the elements of a JavaScript Set

Set 对象维护其元素的插入顺序，因此迭代元素时，元素的顺序与插入的顺序相同。

```js
let roles = new Set();
roles.add('admin')
    .add('editor')
    .add('subscriber');
```

使用 for...of 循环迭代：

```js
for (let role of roles) {
    console.log(role);
}
```

Set 还像 Map 一样提供了keys()、values() 和entrys() 方法。但是，Set 中的 key 和 value 是相同的。

```js
for (let [key, value] of roles.entries()) {
    console.log(key === value);
}
```

### Invoke a callback function on each element of a set

如果要对集合中的每个元素调用回调函数，可以使用 forEach() 方法。

```js
roles.forEach(role => console.log(role.toUpperCase()));
```

## WeakSets

WeakSet 与 Set 类似，只是它只包含对象。由于 WeakSet 中的对象可能会被自动垃圾回收，因此 WeakSet 没有 size 属性。与 WeakMap 一样，无法迭代 WeakSet 的元素，因此 WeakSet 在实践中很少使用。事实上，仅使用 WeakSet 来检查指定值是否在集合中。

```js
let computer = {type: 'laptop'};
let server = {type: 'server'};
let equipment = new WeakSet([computer, server]);

if (equipment.has(server)) {
    console.log('We have a server');
}
```
