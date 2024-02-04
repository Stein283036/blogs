# JavaScript globalThis

## Introduction to the JavaScript globalThis object

ES2020 引入了 globalThis 对象，它提供了跨环境访问全局对象的标准方法。

从历史上看，JavaScript 有一个全局对象，在不同的环境中具有不同的名称。

在网络浏览器中，全局对象是 window 或 frames。

但是，Web Workers API 没有 window 对象，因为它没有浏览上下文（browsing context）。因此，Web Workers API 使用 self 作为全局对象。

另一方面，Node.js 使用 global 关键字来引用全局对象。

| Environment  | Global |
| :----------- | :----- |
| Web Browsers | this   |
| Web Workers  | self   |
| Node.js      | global |

如果编写跨环境工作并需要访问全局对象的 JavaScript 代码，则必须使用不同的语法，例如 window、frames、self 或 global。

为了标准化这一点，ES2020 引入了跨环境可用的 globalThis。

例如，以下代码检查当前环境是否支持 Fetch API：

```js
const canFetch = typeof globalThis.fetch === 'function';
console.log(canFetch);
```

该代码检查 fetch() 函数是否是全局对象的属性。在网络浏览器中，globalThis 是window 对象。因此，如果在现代 Web 浏览器上运行此代码，则 canFetch 将为 true。

以下代码在 Web 浏览器上返回 true：

```js
globalThis === window // true
```





