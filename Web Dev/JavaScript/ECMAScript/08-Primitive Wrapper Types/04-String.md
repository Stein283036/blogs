JavaScript String Type

## Introduction to JavaScript String type

String 类型是字符串原始类型的对象包装，可以使用 String 构造函数创建。

```js
let str = new String('JavaScript String Type');
```

String 类型有一个名为 length 的属性，用于说明字符串中的字符数。

```js
console.log(str.length); // 22
```

要获取原始字符串值，使用 String 对象的以下方法之一：valueOf()、toString() 和 toLocaleString()。

```js
console.log(str.valueOf());
console.log(str.toString());
console.log(str.toLocaleString());
```

要访问字符串中的单个字符，可以使用带有数字索引的方括号表示法 []。

```js
console.log(str[0]); // J
```

ES5 中引入了方括号表示法。在 ES5 之前，使用 charAt() 方法。

```js
console.log(str.charAt(0)); // J
```

当对原始字符串变量或字符串字面量调用方法时，它会转换为 String 类型的实例。

```js
'literal string'.toUpperCase();
```

## String manipulation

### Concatenating strings

要连接两个或多个字符串，使用 concat() 方法。

```js
let firstName = 'John';
let fullName = firstName.concat(' ','Doe');
console.log(fullName); // "John Doe"
console.log(firstName); // "John"
```

concat() 方法连接两个或多个字符串并返回结果字符串。注意，concat() 方法不会修改原始字符串。

除了 concat() 方法之外，还可以使用加法运算符 (+) 来连接字符串。在实践中，加法运算符比 concat() 方法更常用。

### Extracting substrings

要从字符串中提取子字符串，使用 substr() 方法。

```js
substr(startIndex,[length]); // 该方法已被弃用
```

substr() 方法接受两个参数。

第一个参数 startIndex 是提取字符的位置，而第二个参数 length 指定要提取的字符数。

```js
let str = "JavaScript String";

console.log(str.substr(0, 10)); // "JavaScript"
console.log(str.substr(11,6)); // "String"
```

如果省略长度参数，substr() 方法将提取字符到字符串末尾。

有时，希望使用起始索引和结束索引从字符串中提取子字符串。在这种情况下，使用 substring() 方法。

```js
substring(startIndex,endIndex) // 不包括 endIndex
```

```js
let str = "JavaScript String";
console.log(str.substring(4, 10)); // "Script"
```

### Locating substrings

要在字符串中查找子字符串，可以使用 indexOf() 方法：

```js
string.indexOf(searchString: string, position?: number);
```

indexOf() 方法接受两个参数：要定位的子字符串和方法开始在字符串中向前搜索的 position。

indexOf() 返回子字符串在字符串中第一次出现的索引。如果未找到子字符串，indexOf() 方法将返回 -1。

```js
let str = "This is a string";
console.log(str.indexOf("is")); // 2
```

以下示例使用 position 参数：

```js
console.log(str.indexOf('is', 3)); // 5
```

要查找字符串中子字符串最后一次出现的位置，可以使用 lastIndexOf() 方法。

```js
string.lastIndexOf(searchString: string, position?: number)
```

与 indexOf() 方法不同，lastindexOf() 方法从 position 参数从后向前搜索。

```js
console.log(str.lastIndexOf('is')); // 5
```

如果在字符串中找不到子字符串，lastIndexOf() 方法也会返回 -1。

```js
console.log(str.lastIndexOf('are')); // -1
```

### Removing whitespace characters

要删除字符串的所有前导和尾随空白字符，使用trim() 方法。

```js
let rawString = ' Hi  ';
let strippedString = rawString.trim();
console.log(strippedString); // "Hi"
```

> 请注意，trim() 方法会创建原始字符串的副本，并删除空格字符，它不会更改原始字符串。

ES6 引入了两种从字符串中删除空格字符的新方法：

- trimStart() 返回一个字符串，其中删除了字符串开头的空格。
- trimEnd() 返回一个字符串，其中删除了字符串末尾的空格。

### Changing cases

要更改字符串的大小写，可以使用 toLowerCase() 和 toUpperCase() 方法。

```js
let greeting = 'Hello';
console.log(greeting.toLowerCase()); // 'hello'
console.log(greeting.toUpperCase()); // 'HELLO';
```

在某些语言中，将字符串转换为小写和大写的规则非常具体。

因此，使用 toLocaleLowerCase() 和 toLocaleUpperCase() 方法更安全，尤其是不知道代码将处理哪种语言时。

### Comparing strings

要比较两个字符串，可以使用 localeCompare() 方法。

```js
localeCompare(that: string, locales?: string | string[], options?: Intl.CollatorOptions): number
Determines whether two strings are equivalent in the current or specified locale.
```

localeCompare() 返回三个值之一：-1、0 和 1。

- 如果按字母顺序第一个字符串位于第二个字符串之前，则该方法返回 -1。
- 如果第一个字符串按字母顺序位于第二个字符串之后，则该方法返回 1。
- 如果两个字符串相等，该方法返回 0。

```js
console.log('A'.localeCompare('B')); // -1
console.log('B'.localeCompare('B')); // 0
console.log('C'.localeCompare('B')); // 1
```

### Matching patterns

match() 方法允许将字符串与指定的正则表达式进行匹配并获取结果数组。

如果没有找到任何匹配项，match() 方法将返回 null。否则，它返回一个包含整个匹配和任何括号捕获匹配结果的数组。

如果未设置全局标志 (g)，则数组的元素零包含整个匹配项。

```js
let expression = '1 + 2 = 3';
let matches = expression.match(/\d+/);
console.log(matches[0]); // "1"
```

如果设置了全局标志 (g)，则结果数组的元素包含所有匹配项，如下所示：

```js
let expression = '1 + 2 = 3';
let matches = expression.match(/\d+/g);

for (const match of matches) {
  console.log(match);
}
1
2
3
```

在此示例中，matches 数组包含表达式字符串中的所有匹配项，包括 1、2 和 3。

如果只需要查找字符串是否与正则表达式匹配，则可以使用 search() 方法。

与 match() 方法类似，search() 方法接受正则表达式并返回找到第一个匹配项的字符串位置。如果未找到匹配项，则返回 -1。

```js
search(regexp: string | RegExp): number
Finds the first substring match in a regular expression search.
```

```js
let str = "This is a test of search()";
let pos = str.search(/is/);
console.log(pos); // 2
```

### Replacing substrings

要替换字符串中的子字符串，使用replace() 方法。

```js
replace(searchValue: string | RegExp, replaceValue: string): string
Replaces text in a string, using a regular expression or search string.
```

以下示例说明了如何使用正则表达式将 the 替换为 a：

```js
let str = "the baby kicks the ball";

// replace "the" with "a"
let newStr = str.replace(/the/g, "a");

console.log(newStr); // "a baby kicks a ball"
console.log(str); // "the baby kicks the ball"
```

以下示例演示如何通过使用第一个参数作为 string 来将 kicks 替换为 holds。

```js
newStr = str.replace('kicks', 'holds');
console.log(newStr); // "the baby holds the ball"
```