# JavaScript Recursive Function

## Introduction to the JavaScript recursive functions

递归函数是一个不断调用自身直到不再调用自身的函数。这种技术称为递归。

假设有一个名为 recurse() 的函数。如果 recurse() 在函数体内调用自身，则它是一个递归函数，如下所示：

```js
function recurse() {
    // ...
    recurse();
    // ...
}
```

递归函数总是有一个停止调用自身的条件。否则，它将无限期地调用自己。

```js
function recurse() {
    if(condition) {
        // stop calling itself
        //...
    } else {
        recurse();
    }
}
```

通常，使用递归函数将大问题分解为较小的问题。通常，会在二叉树和图形等数据结构以及二分搜索和快速排序等算法中找到递归函数。

## JavaScript recursive function examples

### A simple JavaScript recursive function example

假设需要开发一个从指定数字倒数到 1 的函数。例如，从 3 倒数到 1：

```js
function countDown(fromNumber) {
    console.log(fromNumber);

    let nextNumber = fromNumber - 1;

    if (nextNumber > 0) {
        countDown(nextNumber);
    }
}
countDown(3);
```

### Calculate the sum of n natural numbers example

假设需要使用递归技术计算从 1 到 n 的自然数之和。为此，需要递归地定义 sum()，如下所示：

```js
function sum(n) {
  if (n <= 1) {
    return n;
  }
  return n + sum(n - 1);
}
```
