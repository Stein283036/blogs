# JavaScript Events

## Introduction to JavaScript events

An event is an action that occurs in the web browser, which the web browser feedbacks to you so that you can respond to it.

For example, when you click a button on a webpage, you may want to respond to this `click` event by displaying a dialog box.

Each event may have an event handler which is a block of code that will execute when the event occurs.

An event handler is also known as an event listener. It listens to the event and executes when the event occurs.

Suppose you have a button with the id `btn`:

```html
<button id="btn">Click Me!</button>
```

To define the code that will be executed when the button is clicked, you need to register an event handler using the `addEventListener()` method:

```js
let btn = document.querySelector('#btn');
function display() {
    alert('It was clicked!');
}
btn.addEventListener('click',display);
```

A shorter way to register an event handler is to place all code in an anonymous function, like this:

```js
let btn = document.querySelector('#btn');
btn.addEventListener('click',function() {
    alert('It was clicked!');
});
```

## Event flow

Assuming that you have the following HTML document:

```html
<!DOCTYPE html>
<html>
<head>
    <title>JS Event Demo</title>
</head>
<body>
    <div id="container">
        <button id='btn'>Click Me!</button>
    </div>
</body>
```

When you click the button, you’re clicking not only the button but also the button’s container, the `div`, and the whole webpage.

Event flow explains the order in which events are received on the page from the element where the event occurs and propagated through the DOM tree.

There are two main event models: event bubbling and event capturing.

### Event bubbling

In the event bubbling model, an event starts at the most specific element and then flows upward toward the least specific element (the `document` or even `window`).

When you click the button, the `click` event occurs in the following order:

1. button
2. div with the id container
3. body
4. html
5. document

The `click` event first occurs on the button which is the element that was clicked. Then the `click` event goes up the DOM tree, firing on each node along its way until it reaches the `document` object.

![JavaScript event bubbling](D:\2024年\blogs\Web Dev\JavaScript\DOM\07-Working with Events\assets\JavaScript-event-bubbling.png)



Note that modern web browsers bubble the event up to the `window` object.

当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡，事件冒泡是默认存在的。

### Event capturing

addEventListener 第三个参数传入 true 代表是捕获阶段触发（很少使用）若传入 false 代表冒泡阶段触发，默认就是 false 若是用 L0 事件监听，则只有冒泡阶段，没有捕获阶段。

In the event capturing model, an event starts at the least specific element and flows downward toward the most specific element.

When you click the button, the `click` event occurs in the following order:

1. document
2. html
3. body
4. div with the id container
5. button

![JavaScript event capturing](D:\2024年\blogs\Web Dev\JavaScript\DOM\07-Working with Events\assets\JavaScript-event-capturing.png)

### DOM Level 2 Event flow

DOM level 2 events specify that event flow has three phases:

- First, event capturing occurs, which provides the opportunity to intercept the event.
- Then, the actual target receives the event.
- Finally, event bubbling occurs, which allows a final response to the event.

![JavaScript DOM Level 2 Event](D:\2024年\blogs\Web Dev\JavaScript\DOM\07-Working with Events\assets\JavaScript-DOM-Level-2-Event.png)

## Event object

When the event occurs, the web browser passes an `Event` object to the event handler:

```js
let btn = document.querySelector('#btn');

btn.addEventListener('click', function(event) {
    console.log(event.type); // 'click'
});
```

Note that the `event` object is only accessible inside the event handler. Once all the event handlers have been executed, the event object is automatically destroyed.

### preventDefault()

To prevent the default behavior of an event, you use the `preventDefault()` method.

For example, when you click a link, the browser navigates you to the URL specified in the `href` attribute:

```html
<a href="https://www.javascripttutorial.net/">JS Tutorial</a>
```

However, you can prevent this behavior by using the `preventDefault()` method of the `event` object:

```js
let link = document.querySelector('a');

link.addEventListener('click',function(event) {
    console.log('clicked');
    event.preventDefault();
});
```

Note that the `preventDefault()` method does not stop the event from bubbling up the DOM. An event can be canceled when its `cancelable` property is `true`.

### stopPropagation()

The `stopPropagation()` method immediately stops the flow of an event through the DOM tree. However, it does not stop the browser’s default behavior.

```js
let btn = document.querySelector('#btn');

btn.addEventListener('click', function(event) {
    console.log('The button was clicked!');
    event.stopPropagation();
});

document.body.addEventListener('click',function(event) {
    console.log('The body was clicked!');
});
```

Without the `stopPropagation()` method, you would see two messages on the Console window.

However, the `click` event never reaches the `body` because the `stopPropagation()` was called on the `click` event handler of the button.

此方法可以阻断事件流动传播，不光在冒泡阶段有效，捕获阶段也有效。