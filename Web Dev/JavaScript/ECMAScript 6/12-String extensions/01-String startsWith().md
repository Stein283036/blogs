# JavaScript String startsWith()

### Introduction to the JavaScript startsWith() method

如果字符串在指定 position 以 searchString 开头，startsWith() 返回 true，否则返回 false。

`startsWith` 的语法：

```js
startsWith(searchString: string, position?: number): boolean
```

### Arguments

- searchString 是要在此字符串开头搜索的字符。
- position 是一个可选参数，用于确定搜索 searchString 的起始位置。默认为 0。

## JavaScript String startsWith() examples

```js
const title = 'Jack and Jill Went Up the Hill';
```

使用 startsWith() 方法来检查 title 是否以字符串“Jack”开头：

```js
console.log(title.startsWith('Jack')); // true
```

startsWith() 方法匹配字符区分大小写，因此以下语句返回 false：

```js
title.startsWith('jack'); // false
```

此示例使用带有第二个参数的startsWith()方法，该方法确定开始搜索的起始位置：

```js
console.log(title.startsWith('Jill', 9)); // true
```