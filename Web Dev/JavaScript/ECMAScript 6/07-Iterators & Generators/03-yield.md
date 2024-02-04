# JavaScript yield

## Introduction to the JavaScript `yield` keyword

yield 关键字暂停和恢复生成器函数 (function*)。

yield 关键字的语法：

```js
[variable_name] = yield [expression];
```

expression 指定通过迭代协议从生成器函数返回的值。如果省略表达式，yield 返回 undefined。

variable_name 存储传递给迭代器对象的 next() 方法的可选值。

## JavaScript `yield` examples

### Returning a value

```js
function* foo() { 
    yield 1;
    yield 2;
    yield 3;
}

let f = foo();

console.log(f.next()); // { value: 1, done: false }
```

### Returning `undefined`

```js
function* bar() {
    yield;
}

let b = bar();
console.log(b.next()); // { value: undefined, done: false }
```

### Passing a value to the `next()` method

在以下示例中，yield 关键字是一个表达式，用于计算传递给 next() 方法的参数：

```js
function* generate() {
    let result = yield;
    console.log(`result is ${result}`);
}

let g = generate();
console.log(g.next()); 

console.log(g.next(1000));
```

第一次调用 g.next() 返回以下对象：

```js
{ value: undefined, done: false }
```

第二次调用 g.next() 执行以下任务：

- Evaluate `yield` to 1000.
- Assign `result` the value of `yield`, which is `1000`.
- Output the message and return the object

输出：

```js
result is 1000
{ value: undefined, done: true }
```

### Using `yield` in an array

以下示例使用 yield 关键字作为数组的元素：

```js
function* baz() {
    let arr = [yield, yield];
    console.log(arr);
}

var z = baz();

console.log(z.next());  
console.log(z.next(1)); 
console.log(z.next(2));
```

第一次调用 z.next() 将 arr 数组的第一个元素设置为 1 并返回以下对象：

```js
{ value: undefined, done: false }
```

第二次调用 z.next() 将 arr 数组的第二个元素设置为 2 并返回以下对象：

```js
{ value: undefined, done: false }
```

第三次调用 z.next() 显示 arr 数组的内容并返回以下对象：

```js
[ 1, 2 ]
{ value: undefined, done: true }
```

### Using `yield` to return an array

以下生成器函数使用 yield 关键字返回一个数组：

```js
function* yieldArray() {
    yield 1;
    yield [ 20, 30, 40 ];
}

let y = yieldArray();

console.log(y.next()); 
console.log(y.next()); 
console.log(y.next());
```

第一次调用 y.next() 返回以下对象：

```js
{ value: 1, done: false }
```

第二次调用 y.next() 返回以下对象：

```js
{ value: [ 20, 30, 40 ], done: false }
```

在本例中，yield 将数组 [20, 30, 40] 设置为返回对象的 value 属性的值。

第三次调用 y.next() 返回以下对象：

```js
{ value: undefined, done: true }
```

### Using the `yield` to return individual elements of an array

```js
function* yieldArrayElements() {
    yield 1;
    yield* [ 20, 30, 40 ];
}

let a = yieldArrayElements();

console.log(a.next()); // { value: 1, done: false }
console.log(a.next()); // { value: 20, done: false }
console.log(a.next()); // { value: 30, done: false }
console.log(a.next()); // { value: 40, done: false }
console.log(a.next()); // { value: undefined, done: true }
```

在此示例中，yield* 是新语法。 yield* 表达式用于委托给另一个可迭代对象或生成器。

因此，以下表达式返回数组 [20, 30, 40] 的各个元素：

```js
yield* [20, 30, 40];
```
