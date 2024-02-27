# Introduction

## 概述

JavaScript是一种高级、解释性的编程语言，主要用于在网页上添加交互性和动态内容。它是一种多范式的语言，支持面向对象编程、命令式编程和函数式编程等不同编程范式。

## 组成

1. **核心(ECMAScript)**: ECMAScript是JavaScript的标准规范，规定了语言的基本结构、数据类型、运算符、语法等。所有的JavaScript引擎都必须实现ECMAScript标准。
2. **文档对象模型(DOM)**: DOM是一种处理文档结构的接口，它允许JavaScript通过对文档的访问和操作来改变页面的内容、结构和样式。DOM 将文档表示为一个树结构，每个节点都是文档中的一个元素。
3. **浏览器对象模型(BOM)**: BOM提供了与浏览器交互的对象，例如window、navigator、location、history等。BOM并不属于JavaScript语言的核心规范，但它是JavaScript在浏览器环境中实现交互的重要组成部分。

## 应用

### 浏览器

- **网页交互**: JavaScript可以通过DOM实现对网页内容的动态操作，包括修改、添加、删除元素，以及处理用户输入。
- **异步通信**: 使用JavaScript可以通过XMLHttpRequest或Fetch API进行异步通信，例如向服务器发送请求并在后台获取数据，实现无需刷新页面的内容更新。
- **动画效果**: JavaScript可以通过操作DOM和CSS来创建动画效果，使页面更加生动和吸引人。
- **表单验证**: 可以使用JavaScript对用户输入进行验证，提高表单的交互性和用户友好性。
- **构建单页应用(SPA)**: JavaScript框架（如React、Angular、Vue等）可以用于构建单页应用，提供更流畅的用户体验，减少页面刷新的需求。

### 服务端

1. **服务器端开发**: Node.js是一种基于事件驱动、非阻塞I/O的JavaScript运行时环境，用于服务器端开发。开发者可以使用JavaScript编写服务器端的应用程序，例如Web服务器、API服务器等。
2. **构建工具和脚本**: Node.js广泛用于构建工具和脚本，例如使用npm（Node.js包管理器）管理项目依赖、执行自动化构建任务、进行单元测试等。
3. **后端框架**: 有许多基于Node.js的后端框架，如Express.js，用于简化和加速服务器端应用的开发过程。
4. **实时应用程序**: Node.js的事件驱动模型和非阻塞I/O使其非常适合处理实时应用程序，如聊天应用、在线游戏等。
5. **数据库访问**: 使用Node.js可以方便地访问数据库，执行查询并将数据返回给客户端。

## Engine

当加载网页时，即下载 HTML 和 CSS 后，Web 浏览器中的 JavaScript 引擎会执行 JavaScript 代码。

JavaScript 引擎是 Web 浏览器的一个组件，负责解释和执行 JavaScript 代码。它包括一个用于分析代码的解析器、一个用于将其转换为机器代码的编译器以及一个用于运行编译后的代码的解释器。

最初，JavaScript 引擎是作为解释器实现的。然而，现代 JavaScript 引擎通常被实现为即时编译器，将 JavaScript 代码编译为字节码以提高性能。

## 引入JS——script标签

不建议将 JavaScript 代码直接放置在 <script> 元素中，并且应仅用于概念验证或测试目的。

当页面上有多个 JavaScript 文件时，JavaScript 引擎会按照文件出现的顺序解释这些文件。

### async 和 defer 属性

要修改浏览器加载和执行 JavaScript 文件的方式，可以使用 <script> 元素的两个属性之一：async 和 defer。这些属性仅对外部脚本文件生效。

当一个脚本标签包含 `async` 属性时，脚本将会异步加载，而不会阻塞页面的解析和渲染。异步加载的脚本一旦下载完成，会立即执行，不管其他资源是否已经加载完成。如果有多个脚本同时设置了 `async` 属性，它们的执行顺序将取决于加载完成的顺序。

当一个脚本标签包含 `defer` 属性时，脚本也会异步加载，但是它会在文档解析完成之后、`DOMContentLoaded` 事件触发之前执行。多个带有 `defer` 属性的脚本按照它们在文档中出现的顺序执行。

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript defer demonstration</title>
    <script defer src="defer-script.js"></script>
</head>
<body>
</body>
</html>
```

这两者通常用于优化页面加载性能，使得脚本加载不阻塞页面渲染，同时控制脚本的执行时机。如果你希望脚本在页面解析过程中不阻塞，但又需要按照顺序执行，可以使用 `defer`。如果顺序不是关键，而你想要脚本在加载完成后尽快执行，可以使用 `async`。



