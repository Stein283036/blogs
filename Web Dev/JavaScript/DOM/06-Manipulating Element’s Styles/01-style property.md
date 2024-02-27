# JavaScript Style

## Setting inline styles

要设置元素的内联样式，可以使用该元素的 style 属性：

```js
element.style
```

The `style` property returns the read-only `CSSStyleDeclaration` object that contains a list of CSS properties. For example, to set the color of an element to `red`, you use the following code:

```js
element.style.color = 'red';
```

If the CSS property contains hyphens (`-`) for example `-webkit-text-stroke` you can use the array-like notation (`[]`) to access the property:

```js
element.style.['-webkit-text-stock'] = 'unset';
```

To completely override the existing inline style, you set the `cssText` property of the `style` object.

```js
element.style.cssText = 'color:red;background-color:yellow';
```

Or you can use the `setAttribute()` method:

```js
element.setAttribute('style','color:red;background-color:yellow');
```

Once setting the inline style, you can modify one or more CSS properties:

```js
element.style.color = 'blue';
```

If you do not want to completely overwrite the existing CSS properties, you can concatenate the new CSS property to the `cssText` as follows:

```js
element.style.cssText += 'color:red;background-color:yellow';
```