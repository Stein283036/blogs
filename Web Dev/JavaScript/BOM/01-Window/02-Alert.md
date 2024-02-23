# JavaScript alert

## Introduction to JavaScript `alert()` method

The browser can invoke a system dialog to display information to the user.

系统对话框与浏览器中显示的网页无关。它也不包含任何 HTML。它的外观完全取决于当前的操作系统和浏览器，而不是CSS。

To invoke an alert system dialog, you invoke the `alert()` method of the `window` object.

```js
window.alert(message);
```

或者：

```js
alert(message);
```

```js
alert('Welcome to JavaScriptTutorial.net!');
```

When the `alert()` method is invoked, a system dialog shows the specified message to the user followed by a single **OK** button.

使用警报对话框来通知用户一些他们无法控制的事情，例如错误。用户可以做出的唯一选择是在阅读消息后关闭对话框。

注意，警报对话框是同步的且是模态的（modal）。这意味着代码执行在对话框显示时停止，并在对话框关闭后恢复。例如，以下代码在三秒后显示警报对话框：

```js
setTimeout(() => {
    alert('3 seconds has been passed!')
}, 3000);
```