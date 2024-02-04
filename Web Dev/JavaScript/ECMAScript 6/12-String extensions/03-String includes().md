# JavaScript String includes() Method

## Introduction to JavaScript String `includes()` method

include() 方法判断一个字符串是否包含另一个字符串：

```js
string.includes(searchString [,position])
```

如果在字符串中找到 searchString，则 includes() 方法返回 true；否则为 false。

可选的 position 参数指定字符串中开始搜索 searchString 的位置。该位置默认为 0。

includes() 匹配字符串时区分大小写。

## JavaScript String `includes()` examples

```js
let email = 'admin@example.com';
console.log(email.includes('@')); // true
```

```js
let str = 'JavaScript String';
console.log(str.includes('Script')); // true
```

```js
let str = 'JavaScript String';
console.log(str.includes('Script', 5)); // true
```