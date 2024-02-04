# JavaScript String endsWith

## Introduction to the JavaScript String endsWith() method

如果字符串以指定字符串的字符结尾，endsWith() 返回 true，否则返回 false。

endsWith() 方法的语法：

```js
endsWith(searchString: string, endPosition?: number): boolean
```

### Arguments

- searchString 是要在字符串末尾搜索的字符。
- endPosition 是一个可选参数，用于确定要搜索的字符串的长度。它默认为字符串的长度。

## JavaScript String endsWith() method examples

```js
const title = 'Jack and Jill Went Up the Hill';
```

使用 endsWith() 方法来检查 title 是否以字符串“Hill”结尾：

```js
console.log(title.endsWith('Hill')); // true
```

使用带有第二个参数的 endsWith() 方法，该方法确定要搜索的字符串的长度：

```js
console.log(title.endsWith('Up', 21)); // true
```