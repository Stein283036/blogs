# Document Object Model in JavaScript

## What is Document Object Model (DOM)

文档对象模型 (DOM) 是用于操作 HTML 文档的应用程序编程接口 (API)。

DOM 将 HTML 文档表示为节点树。 DOM 提供的功能允许有效地添加、删除和修改文档的某些部分。

DOM 是跨平台且与语言无关的操作 HTML 和 XML 文档的方法。

## A document as a hierarchy of nodes

DOM 将 HTML 文档表示为节点层次结构。

```js
<html>
    <head>
        <title>JavaScript DOM</title>
    </head>
    <body>
        <p>Hello DOM!</p>
    </body>
</html>
```

![JavaScript DOM](D:\2024年\blogs\Web Dev\JavaScript\DOM\01-Getting started\assets\JavaScript-DOM.png)

In this DOM tree, the document is the root node. The root node has one child node which is the `<html>` element. The `<html>` element is called the *document element*.

Each document can have only one `document` element. In an HTML document, the `document` element is the `<html>` element. Each markup can be represented by a node in the tree.

### Node Types

Each node in the DOM tree is identified by a node type. JavaScript uses integer numbers to determine the node types. The following table illustrates the node type constants:

| Constant                           | Value | Description                                                  |
| :--------------------------------- | :---- | :----------------------------------------------------------- |
| `Node.ELEMENT_NODE`                | `1`   | An `Element` node like `<p>` or `<div>`.                     |
| `Node.TEXT_NODE`                   | `3`   | The actual `Text` inside an `Element` or `Attr`.             |
| `Node.CDATA_SECTION_NODE`          | `4`   | A `CDATASection`, such as `<!CDATA[[ … ]]>`.                 |
| `Node.PROCESSING_INSTRUCTION_NODE` | `7`   | A `ProcessingInstruction` of an XML document, such as `<?xml-stylesheet … ?>`. |
| `Node.COMMENT_NODE`                | `8`   | A `Comment` node, such as `<!-- … -->`.                      |
| `Node.DOCUMENT_NODE`               | `9`   | A `Document` node.                                           |
| `Node.DOCUMENT_TYPE_NODE`          | `10`  | A `DocumentType` node, such as `<!DOCTYPE html>`.            |
| `Node.DOCUMENT_FRAGMENT_NODE`      | `11`  | A `DocumentFragment` node.                                   |

To get the type of node, you use the `nodeType` property:

```js
node.nodeType
```

可以将 nodeType 属性与上述常量进行比较来确定节点类型。

```js
if (node.nodeType == Node.ELEMENT_NODE) {
    // node is the element node
}
```

### The `nodeName` and `nodeValue` properties

A node has two important properties: `nodeName` and `nodeValue` that provide specific information about the node.

The values of these properties depend on the node type. For example, if the node type is the element node, the `nodeName` is always the same as the element’s tag name and `nodeValue` is always `null`.

For this reason, it’s better to test node type before using these properties:

```js
if (node.nodeType == Node.ELEMENT_NODE) {
    let name = node.nodeName; // tag name like <p>
}
```

### Node and Element

Sometimes it’s easy to confuse between the `Node` and the `Element`.

A node is a generic name of any object in the DOM tree. It can be any built-in DOM element such as the document. Or it can be any HTML tag specified in the HTML document like `<div>` or `<p>`. 

An element is a node with a specific node type `Node.ELEMENT_NODE`, which is equal to 1.

In other words, the node is the generic type of element. The element is a specific type of the node with the node type `Node.ELEMENT_NODE`.

The following picture illustrates the relationship between the `Node` and `Element` types:

![Document Object Model in JavaScript](D:\2024年\blogs\Web Dev\JavaScript\DOM\01-Getting started\assets\Document-Object-Model-in-JavaScript-17083225580327.png)

Note that the `getElementById()` and `querySelector()` returns an object with the `Element` type while `getElementsByTagName()` or `querySelectorAll()` returns `NodeList` which is a collection of nodes. 

### Node Relationships

Any node has relationships to other nodes in the DOM tree.

For example, `<body>` is a child node of the `<html>` node, and `<html>` is the parent of the `<body>` node.

The `<body>` node is the sibling of the `<head>` node because they share the same immediate parent, which is the `<html>` element.







