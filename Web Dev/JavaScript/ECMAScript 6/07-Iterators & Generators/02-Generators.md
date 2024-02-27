# JavaScript Generators

在 JavaScript 中，常规函数是基于运行到完成（run-to-completion）模型执行的。它不能中途暂停然后从暂停的地方继续。

```js
function foo() {
    console.log('I');
    console.log('cannot');
    console.log('pause');
}
```

foo() 函数从上到下执行。退出 foo() 的唯一方法是返回或抛出错误。如果再次调用 foo() 函数，它将从上到下开始执行。

ES6 引入了一种与常规函数不同的新函数：函数生成器或生成器（function generator or generator）。

generator 可以中途暂停，然后从暂停处继续。

```js
function* generate() {
    console.log('invoked 1st time');
    yield 1;
    console.log('invoked 2nd time');
    yield 2;
}
```

generate() 函数细节：

- 首先，会在 function 关键字后面看到星号 (*)。`*` 表示 generate() 是一个生成器，而不是一个普通函数。
- 其次，yield 语句返回一个值并暂停函数的执行。

以下代码调用 generate() 生成器：

```js
let gen = generate();
```

调用 generate() 生成器：

- 首先，在控制台中看不到任何内容。
- 其次，从 generate() 中得到返回值 Object [Generator] {}。

因此，生成器在调用时返回一个 Generator 对象，而不执行其主体。

Generator 对象有一个 next() 方法返回另一个具有两个属性的对象：done 和 value。换句话说，Generator 对象是可迭代的 （iterable）。

下面调用 Generator 对象的 next() 方法：

```js
let result = gen.next();
console.log(result);
invoked 1st time
{ value: 1, done: false }
```

正如所看到的，Generator 对象执行方法体，在第 1 行输出消息“invoked 1st time”，并在第 2 行返回值 1。

yield 语句返回 1 并在第 2 行暂停生成器。

类似地，以下代码第二次调用 Generator 的 next() 方法：

```js
result = gen.next();
console.log(result);
invoked 2nd time
{ value: 2, done: false }
```

这次，生成器从第 3 行恢复执行，输出消息“invoked 2nd time”并返回（或产生）2。

下面第三次调用生成器对象的 next() 方法：

```js
result = gen.next();
console.log(result); // { value: undefined, done: true }
```

由于生成器是可迭代的，因此可以使用 for...of 循环：

```js
for (const g of gen) {
    console.log(g);
}
invoked 1st time
1
invoked 2nd time
2
```

## More JavaScript generator examples

以下示例说明了如何使用生成器生成永无止境的序列：

```js
function* forever() {
    let index = 0;
    while (true) {
        yield index++;
    }
}

let f = forever();
console.log(f.next()); // { value: 0, done: false }
console.log(f.next()); // { value: 1, done: false }
console.log(f.next()); // { value: 2, done: false }
```

## Using generators to implement iterators

当实现迭代器时，必须手动定义 next() 方法。在 next() 方法中，还必须手动保存当前元素的状态。

由于生成器是可迭代的，因此它们可以帮助简化实现迭代器的代码。

```js
class Sequence {
    constructor( start = 0, end = Infinity, interval = 1 ) {
        this.start = start;
        this.end = end;
        this.interval = interval;
    }
    * [Symbol.iterator]() {
        for( let index = this.start; index <= this.end; index += this.interval ) {
            yield index;
        }
    }
}
```

通过使用生成器，Symbol.iterator 方法要简单得多。

以下脚本使用序列迭代器生成从 1 到 10 的奇数序列：

```js
let oddNumbers = new Sequence(1, 10, 2);

for (const num of oddNumbers) {
    console.log(num);
}
```

## Using a generator to implement the Bag data structure

Bag 是一种能够收集元素并迭代元素的数据结构。它不支持删除项目。

以下脚本实现了 Bag 数据结构：

```js
class Bag {
    constructor() {
        this.elements = [];
    }
    isEmpty() {
        return this.elements.length === 0;
    }
    add(element) {
        this.elements.push(element);
        return this;
    }
    * [Symbol.iterator]() {
        for (let element of this.elements) {
            yield element;
        }
    }
}

let bag = new Bag();

bag.add(1).add(2).add(3);

for (let e of bag) {
    console.log(e);
}
```