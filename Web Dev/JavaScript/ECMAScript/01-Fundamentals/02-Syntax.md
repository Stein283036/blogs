# Syntax

## Whitespace

空白是指在其他字符之间提供空间的字符。 JavaScript 有以下空格：

- Carriage return
- Space
- New Line
- tab

JavaScript 引擎会忽略空格。但是，您可以使用空格来格式化代码，以使其易于阅读和维护。

JavaScript 打包器（Webpack）会删除 JavaScript 文件中的所有空格，并将它们放入单个文件中进行部署。通过这样做，JavaScript 捆绑器使 JavaScript 代码更轻、更快地加载到 Web 浏览器中。

## Statements

语句是一段声明变量或指示 JavaScript 引擎执行任务的代码。一个简单的语句以分号 (;) 结束。尽管分号 (;) 是可选的；您应该始终使用它来终止语句。

### Blocks

块是零个或多个简单语句的序列。块由一对大括号 {} 分隔。

## Identifiers

标识符是您为变量、参数、函数、类等选择的名称。

标识符名称以字母（a-z 或 A-Z）、下划线（_）或美元符号（$）开头，后跟一系列字符，包括（a-z、A-Z）、数字（0-9）、下划线(_) 和美元符号 ($)。

请注意，该字母不限于 ASCII 字符集，并且可能包括扩展 ASCII 或 Unicode，但不建议这样做。

## Comments

注释是用来解释程序元素的额外信息，JS引擎会忽视所有的注释。

- 单行注释 `//`
- 多行注释 `/* */`

## Expressions

表达式是计算结果的一段代码。

## Keywords & Reserved words

JavaScript 定义了具有特定用途的保留关键字列表。因此，由于语言规则，您不能使用保留关键字作为标识符或属性名称。

