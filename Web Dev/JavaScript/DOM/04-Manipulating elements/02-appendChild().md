# JavaScript appendChild

## Introduction to the JavaScript `appendChild()` method

The `appendChild()` is a method of the `Node` interface. The `appendChild()` method allows you to add a node to the end of the list of child nodes of a specified parent node.

```js
parentNode.appendChild(childNode);
```

In this method, the `childNode` is the node to append to the given parent node. The `appendChild()` returns the appended child.

If the `childNode` is a reference to an existing node in the document, the `appendChild()` method moves the `childNode` from its current position to the new position.

## JavaScript `appendChild()` examples

### Simple `appendChild()` example

```html
<ul id="menu">
</ul>
```

The following example uses the `appendChild()` method to add three list items to the `<ul>` element:

```js
function createMenuItem(name) {
    let li = document.createElement('li');
    li.textContent = name;
    return li;
}
// get the ul#menu
const menu = document.querySelector('#menu');
// add menu item
menu.appendChild(createMenuItem('Home'));
menu.appendChild(createMenuItem('Services'));
menu.appendChild(createMenuItem('About Us'));
```

### Moving a node within the document example

```html
<ul id="first-list">
    <li>Everest</li>
    <li>Fuji</li>
    <li>Kilimanjaro</li>
</ul>

<ul id="second-list">
    <li>Karakoram Range</li>
    <li>Denali</li>
    <li>Mont Blanc</li>
</ul>
```

The following example uses the `appendChild()` to move the first child element from the first list to the second list:

```js
// get the first list
const firstList = document.querySelector('#first-list');
// take the first child element
const everest = firstList.firstElementChild;
// get the second list
const secondList = document.querySelector('#second-list');
// append the everest to the second list
secondList.appendChild(everest)
```