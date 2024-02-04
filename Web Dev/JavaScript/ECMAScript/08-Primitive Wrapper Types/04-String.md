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

## Searching

### match()

match() 方法允许将字符串与指定的正则表达式进行匹配并获取结果数组。

如果没有找到任何匹配项， 方法将返回 null。否则，它返回一个包含整个匹配和任何括号捕获匹配结果的数组。

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

### search()

```js
search(regexp: string | RegExp): number
// regexp: The regular expression pattern and applicable flags.
// Finds the first substring match in a regular expression search.
```

如果只需要查找字符串是否与正则表达式匹配，则可以使用 search() 方法。

search() 方法接受正则表达式并返回找到第一个匹配项的字符串位置。如果未找到匹配项，则返回 -1。

```js
let str = "This is a test of search()";
let pos = str.search(/is/);
console.log(pos); // 2
```

### indexOf()

要在字符串中查找子字符串，可以使用 indexOf() 方法：

```js
string.indexOf(searchString: string, position?: number);
// searchString: The substring to search for in the string
// position: The index at which to begin searching the String object. If omitted, search starts at the beginning of the string.
// Returns the position of the first occurrence of a substring.
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

### lastIndexOf()

要查找字符串中子字符串最后一次出现的位置，可以使用 lastIndexOf() 方法。

```js
string.lastIndexOf(searchString: string, position?: number)
```

与 indexOf() 方法不同，lastindexOf() 方法从 position 参数从后向前搜索。

```js
let str = "This is a string";
console.log(str.lastIndexOf('is')); // 5
```

如果在字符串中找不到子字符串，lastIndexOf() 方法也会返回 -1。

```js
console.log(str.lastIndexOf('are')); // -1
```

### includes()

include() 方法判断一个字符串是否包含另一个字符串：

```js
string.includes(searchString [,position])
```

如果在字符串中找到 searchString，则 includes() 方法返回 true；否则为 false。

可选的 position 参数指定字符串中开始搜索 searchString 的位置。该位置默认为 0。

includes() 匹配字符串时区分大小写。

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

### startsWith()

如果字符串在指定 position 以 searchString 开头，startsWith() 返回 true，否则返回 false。

`startsWith` 的语法：

```js
startsWith(searchString: string, position?: number): boolean
```

- searchString 是要在此字符串开头搜索的字符。
- position 是一个可选参数，用于确定搜索 searchString 的起始位置。默认为 0。

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

### endsWith()

如果字符串以指定字符串的字符结尾，endsWith() 返回 true，否则返回 false。

endsWith() 方法的语法：

```js
endsWith(searchString: string, endPosition?: number): boolean
```

- searchString 是要在字符串末尾搜索的字符。
- endPosition 是一个可选参数，用于确定要搜索的字符串的长度。它默认为字符串的长度。

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

## Trimming

### trim()

### trimStart()

### trimEnd()

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

## Padding

### padStart() & padEnd()

#### String.prototype.padStart()

The `padStart()` method pads a string with another string to a certain length from the start of the string and returns a resulting string that reaches a certain length. The following illustrates the `padStart()` method:

```js
padStart(maxLength: number, fillString?: string): string
// The length of the resulting string once the current string has been padded. If this parameter is smaller than the current string's length, the current string will be returned as it is.
// fillString: The string to pad the current string with. If this string is too long, it will be truncated and the left-most part will be applied. The default value for this parameter is " " (U+0020).
// Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length. The padding is applied from the start (left) of the current string.
```

想要一个包含 8 个字符的数字字符串。对于长度小于 8 的字符串，将用零 (0) 填充。

```js
let str = '1234'.padStart(8,'0');
console.log(str); // "00001234"
```

The following example pads a string by spaces because we don’t pass the pad string.

```js
let str = 'abc'.padStart(5);
console.log(str); // "  abc"
```

```js
let str = '1234'.padStart(8, 'AAB')
console.log(str) // AABA1234
```

#### String.prototype.padEnd()

```js
padEnd(maxLength: number, fillString?: string): string
// Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length. The padding is applied from the end (right) of the current string.
```

```js
let str = 'abc'.padEnd(5);
console.log(str); // "abc  "
```

```js
str = 'abc'.padEnd(5,'*');
console.log(str); // "abc**"
```

```js
str = 'abc'.padEnd(5,'def');
console.log(str); // "abcde"
```

## Extracting

### split()

The `String.prototype.split()` divides a string into an array of substrings:

```js
split(separator: string | RegExp, limit?: number): string[]
// separator: A string that identifies character or characters to use in separating the string. If omitted, a single-element array containing the entire string is returned.
// limit: A value used to limit the number of elements returned in the array.
// Split a string into substrings using the specified separator and return them as an array.
```

```js
let str = 'JavaScript String split()';
let substrings = str.split(' ');
console.log(substrings); // ["JavaScript", "String", "split()"]
```

```js
let str = 'JavaScript String split()';
let substrings = str.split(' ',2);
console.log(substrings); // ["JavaScript", "String"]
```

### substring()

```js
substring(start: number, end?: number): string
// start: The zero-based index number indicating the beginning of the substring.
// end: Zero-based index number indicating the end of the substring. The substring includes the characters up to, but not including, the character indicated by end. If end is omitted, the characters from start through the end of the original string are returned.
// Returns the substring at the specified location within a String object.
```

If `startIndex` equals `endIndex`, the `substring()` method returns an empty string.

If `startIndex` is greater than the `endIndex`, the `substring()` swaps their roles: the startIndex becomes the endIndex and vice versa.

If either `startIndex` or `endIndex` is less than zero or greater than the `string.length`, the `substring()` considers it as zero (0) or `string.length` respectively.

If any parameter is `NaN`, the `substring()` treats it as if it were zero (0).

```js
let str = 'JavaScript Substring';
let substring = str.substring(0,10);
console.log(substring); // JavaScript
```

```js
let str = 'JavaScript Substring';
let substring = str.substring(11);
console.log(substring); // Substring
```

```js
let email = 'john.doe@gmail.com';
let domain = email.substring(email.indexOf('@') + 1);
console.log(domain); // gmail.com
```

### slice()

The `String.prototype.slice()` method extracts a portion of a string and returns it as a substring.

```js
slice(start?: number, end?: number): string
// start: The index to the beginning of the specified portion of stringObj.
// end: The index to the end of the specified portion of stringObj. The substring includes the characters up to, but not including, the character indicated by end. If this value is not specified, the substring continues to the end of stringObj.
// Returns a section of a string.
```

```js
const str = 'Hello';
const substr = str.slice(3);
console.log({ substr }); // { substr: 'lo' }
```

`start` 是负数：

```js
const str = 'Hello';
const substr = str.slice(-3);
console.log({ substr }); // { substr: 'llo' }
```

If the `start` is omitted, `undefined`, or cannot be converted to a number, the `slice()` method starts extraction from the beginning of the string:

```js
const str = 'Hello';
const substr = str.slice();
console.log({ substr }); // { substr: 'Hello' }
```

If the `start` is greater than or equal to the length of the string, the `slice()` method returns an empty string.

```js
const str = 'Hello';
const substr = str.slice(5);
console.log({ substr }); // { substr: '' }
```

`end` 参数：

```js
const str = 'Hello';
const substr = str.slice(0, 2);
console.log({ substr }); // { substr: 'He' }
```

```js
const str = 'Hello';
const substr = str.slice(0, -2);
console.log({ substr }); // { substr: 'Hel' }
```

```js
const str = 'Hello';
const substr = str.slice(2, 6);
console.log({ substr }); // { substr: 'llo' }
```

## Concatenating

### concat()

The `String.prototype.concat()` method accepts a list of strings and returns a new string that contains the combined strings:

```js
concat(...strings: string[]): string
// strings: The strings to append to the end of the string.
// Returns a string that contains the concatenation of two or more strings.
```

If the arguments are not strings, the `concat()` converts them to strings before carrying the concatenation.

> It’s recommended that you use the `+` or `+=` operator for string concatenation to get better performance.

```js
let greeting = 'Hi';
let message = greeting.concat(' ', 'John');
console.log(message); // Hi John
```

```js
let colors = ['Blue',' ','Green',' ','Teal'];
let result = ''.concat(...colors);
console.log(result); // Blue Green Teal
```

```js
let str = ''.concat(1,2,3);
console.log(str); // 123
```

## Replacing

### replace()

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

### replaceAll()

To replace all the occurrences of a substring with a new one, you can call the `replace()` method repeatedly or use a regular expression with a global flag (`g`).

ES2021 introduced the String `replaceAll()` method that returns a new string with all matches of a pattern replaced by a replacement:

```js
String.prototype.replaceAll(pattern, replacement)
```

The `pattern` can be a string or a regular expression. When the `pattern` is a regular expression, it needs to include the global flag (`g`); otherwise, the `replaceAll()` will throw an exception.

The assumption is that you made a mistake and should have used the `replace()` method to replace the first occurrence that matches the pattern only.

The `replacement` argument can be a string or a callback function that will be invoked for each match.

When the `replacement` is a callback function, it has the following form:

```js
replacement(match, offset, str)
```

- `match` is the matched substring.
- `offset` is offset of the matched substring within the original string. For example, if the original string is `'Hello'` and the matched substring is `'ll'`, then the `offset` will be 2.
- `str` is the original string.

Like the `replace()` method, the `replaceAll()` method doesn’t change the original string. It returns the completely new string with the pattern replaced by the replacement.

The following example uses the String `replaceAll()` method to replace the string `JS` with the string `JavaScript` in the string ‘`JS will, JS will, JS will rock you'`:

```js
let str = 'JS will, JS will, JS will rock you.'
let newStr = str.replaceAll('JS', 'JavaScript')
console.log(newStr) // JavaScript will, JavaScript will, JavaScript will rock you.
```

The following example uses the String `replaceAll()` method to search for a substring by a regular expression. It replaces each match with a specific replacement determined by a callback function:

```js
let str = 'JS will, Js will, js will rock you.'
let pattern = /js/gi
function replacement(match, offset, str) {
  if (match === 'JS') {
    return 'JavaScript'
  } else if (match === 'Js') {
    return 'Javascript'
  } else if (match === 'js') {
    return 'javascript'
  }
}
let newStr = str.replaceAll(pattern, replacement)
console.log(newStr) // JavaScript will, Javascript will, javascript will rock you. 
```

## Changing cases

### toUpperCase()

### toLowerCase()

要更改字符串的大小写，可以使用 toLowerCase() 和 toUpperCase() 方法。

```js
let greeting = 'Hello';
console.log(greeting.toLowerCase()); // 'hello'
console.log(greeting.toUpperCase()); // 'HELLO';
```

在某些语言中，将字符串转换为小写和大写的规则非常具体。

因此，使用 toLocaleLowerCase() 和 toLocaleUpperCase() 方法更安全，尤其是不知道代码将处理哪种语言时。

## Comparing

### localeCompare()

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
