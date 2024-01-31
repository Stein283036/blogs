# Introduction

## 概述

JavaScript是一种高级、解释性的编程语言，主要用于在网页上添加交互性和动态内容。它是一种多范式的语言，支持面向对象编程、命令式编程和函数式编程等不同编程范式。

## ECMAScript版本

1. **ECMAScript 1 (ES1)**: 1997年发布，是JavaScript的最初版本。

2. **ECMAScript 2 (ES2)**: 1998年发布，进行了一些修订和改进。

3. **ECMAScript 3 (ES3)**: 1999年发布，是一个重要的版本，定义了大部分现代JavaScript的基本特性。ES3在Web开发中广泛使用，直到近年来仍有很多项目在使用。

4. **ECMAScript 4 (ES4)**: 这个版本计划进行较大的变革，但最终被取消。由于各方面的分歧，ECMAScript 4的草案被废弃，导致后来的发展采取了不同的路径。

5. **ECMAScript 5 (ES5)**: 2009年发布，对ES3进行了修订和改进，引入了一些新的功能。ES5的特性在当时成为主流，支持广泛。

6. **ECMAScript 6 (ES6) / ECMAScript 2015 (ES2015)**: 2015年发布，引入了许多新的特性，如let和const关键字、箭头函数、类、模块等。ES6标志着JavaScript语言的重大升级，为开发者提供了更丰富的语法和功能。

7. **ECMAScript 2016 (ES2016) 和以后的版本**: 自ES6以后，ECMAScript开始以年份来进行版本标识，每年发布一个小版本，其中可能包含一些新功能。例如，ES2016、ES2017等版本都引入了一些小的改进和新特性。

8. **ECMAScript 2021 (ES2021)**: 最新的主要版本，引入了一些新的功能，包括逻辑赋值运算符、String.prototype.replaceAll()等。

需要注意的是，虽然ECMAScript规范定义了JavaScript的核心特性，但实际上，浏览器和其他JavaScript运行环境可能会支持不同版本的ECMAScript，并且可能会提供额外的特性和API。在实际开发中，开发者需要根据目标环境选择合适的ECMAScript版本。

## 组成

1. **核心(ECMAScript)**: ECMAScript是JavaScript的标准规范，规定了语言的基本结构、数据类型、运算符、语法等。所有的JavaScript引擎都必须实现ECMAScript标准。目前，最新版本的ECMAScript是ECMAScript 2021。
2. **文档对象模型(DOM)**: DOM是一种处理文档结构的接口，它允许JavaScript通过对文档的访问和操作来改变页面的内容、结构和样式。DOM 将文档表示为一个树结构，每个节点都是文档中的一个元素。
3. **浏览器对象模型(BOM)**: BOM提供了与浏览器交互的对象，例如window、navigator、location等。BOM并不属于JavaScript语言的核心规范，但它是JavaScript在浏览器环境中实现交互的重要组成部分。

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

总体而言，JavaScript在浏览器和Node.js中都是一种多用途的编程语言，使得开发者能够在前端和后端均使用同一种语言来构建整个Web应用。这也被称为全栈开发（Full Stack Development）。

## 引擎

当加载网页时，即下载 HTML 和 CSS 后，Web 浏览器中的 JavaScript 引擎会执行 JavaScript 代码。

JavaScript 引擎是 Web 浏览器的一个组件，负责解释和执行 JavaScript 代码。它包括一个用于分析代码的解析器、一个用于将其转换为机器代码的编译器以及一个用于运行编译后的代码的解释器。

最初，JavaScript 引擎是作为解释器实现的。然而，现代 JavaScript 引擎通常被实现为即时编译器，将 JavaScript 代码编译为字节码以提高性能。

## 引入JS——script标签

不建议将 JavaScript 代码直接放置在 <script> 元素中，并且应仅用于概念验证或测试目的。

可以从远程服务器加载 JavaScript 文件。这使您能够从不同的域（例如内容分发网络 (CDN)）提供 JavaScript，以提高页面加载速度。

当页面上有多个 JavaScript 文件时，JavaScript 引擎会按照文件出现的顺序解释这些文件。

对于包含许多外部 JavaScript 文件的页面，在渲染阶段可能会显示空白页面。为了防止这种情况，您可以在 </body> 标记之前添加 JavaScript 文件。

- 通过 `script` 标签引入外部 JS 文件
- 通过内嵌 `script` 标签直接加入 JS 代码

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



