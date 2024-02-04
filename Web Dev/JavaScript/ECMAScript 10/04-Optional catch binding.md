# Optional catch Binding

## Introduction to the optional `catch` binding

try...catch 语句用于处理可能发生的任何错误。通常，将可能导致错误的代码放在 try 块中，将处理错误的代码放在 catch 块中，如下所示：

```js
try {
    // code that may cause an error
} catch (error) {
    // code that handles the error
} 
```

在 catch 块中，可以访问包含错误详细信息的 Error 对象。

在实践中，可能需要使用 try...catch 语句来检查 Web 浏览器中是否实现了某个功能。如果不是，希望回退到具有更广泛支持的不太理想的功能，例如：

```js
try {
    // check if a feature is implemented
} catch (error) {
    // fall back to a less desirable feature
}
```

在这种情况下，error 对象被声明但从未使用。

ES2019 引入了可选的 catch 绑定，允许省略 catch 绑定及其周围的 ()，如下所示：

```js
try {

} catch {

}
```