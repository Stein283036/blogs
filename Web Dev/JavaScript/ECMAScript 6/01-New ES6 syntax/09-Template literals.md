# JavaScript Template Literals In Depth

在 ES6 之前，使用单引号 (') 或双引号 (") 来包裹字符串字面量。并且字符串的功能非常有限。

为了能够解决更复杂的问题，ES6 模板字面量提供了允许更安全、更干净地使用字符串的语法。

在 ES6 中，通过将文本用反引号 (`) 括起来来创建模板字面量：

```js
let simple = `This is a template literal`;
```

模板字面量有以下功能：

- 多行字符串：可以跨越多行的字符串。
- 字符串插值（string interpolation）：能够用字符串的一部分替换变量或表达式的值。
- HTML 转义：转换字符串以便安全地包含在 HTML 中的能力。

## The basic syntax of JavaScript template literals

```js
let str = `Template literal in ES6`;

console.log(str);// Template literal in ES6
console.log(str.length); // 23
console.log(typeof str);// string
```

使用反引号，可以在模板字面量中自由使用单引号或双引号而无需转义。

```js
let anotherStr = `Here's a template literal`;
```

## Multiline strings

在 ES6 之前，使用以下技术通过在字符串中手动包含换行符 (\n) 来创建多行字符串：

```js
let msg = 'Multiline \n\
string';

console.log(msg);
//Multiline
//string
```

注意，换行符 (\n) 后面的 \ 表示字符串的继续，而不是新行。

然而，这种技术在 JavaScript 引擎中并不一致。因此，创建依赖于数组和字符串连接（string concatenation）的多行字符串是很常见的：

```js
let msg = ['This text',
         'can',
         'span multiple lines'].join('\n');
```

模板字面量定义多行字符串：

```js
let p =
`This text
can
span multiple lines`;
```

空格是字符串的一部分。因此，需要确保文本以正确的缩进对齐。

```js
let post = {
    title: 'JavaScript Template Literals',
    excerpt: 'Introduction to JavaScript template literals in ES6',
    body: 'Content of the post will be here...',
    tags: ['es6', 'template literals', 'javascript']
};
```

以下代码返回 post 对象的 HTML 代码。

```js
let {title, excerpt, body, tags} = post;

let postHtml = `<article>
<header>
    <h1>${title}</h1>
</header>
<section>
    <div>${excerpt}</div>
    <div>${body}</div>
</section>
<footer>
    <ul>
      ${tags.map(tag => `<li>${tag}</li>`).join('\n      ')}
    </ul>
</footer>
</article>`;
```

以下是变量 postHtml 的输出。注意这里使用空格来正确缩进 `<li>` 标签。

```js
<article>
<header>
    <h1>JavaScript Template Literals</h1>
</header>
<section>
    <div>Introduction to JavaScript template literals in ES6</div>
    <div>Content of the post will be here...</div>
</section>
<footer>
    <ul>
      <li>es6</li>
      <li>template literals</li>
      <li>javascript</li>
    </ul>
</footer>
```

## Variable and expression substitutions

模板字面量和常规字符串之间的最大区别是替换。

替换允许在字符串中嵌入变量和表达式。 JavaScript 引擎将自动用它们的值替换这些变量和表达式。此功能称为字符串插值（string interpolation）。

```js
let firstName = 'John',
    lastName = 'Doe';

let greeting = `Hi ${firstName}, ${lastName}`;
console.log(greeting); // Hi John, Doe
```

The substitution `${firstName}` and `${lastName}` access the variables  `firstName` and `lastName` to insert their values into the `greeting `string.

替换表达式：

```js
let price = 8.99,
    tax = 0.1;

let netPrice = `Net Price:$${(price * (1 + tax)).toFixed(2)}`;

console.log(netPrice); // netPrice:$9.89
```