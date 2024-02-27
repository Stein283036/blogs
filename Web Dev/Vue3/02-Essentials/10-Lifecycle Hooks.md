# Lifecycle Hooks

每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听（data observation），编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。

## 注册周期钩子

举例来说，`mounted` 钩子可以用来在组件完成初始渲染并创建 DOM 节点后运行代码：

还有其他一些钩子，会在实例生命周期的不同阶段被调用，最常用的是 `mounted`、`updated` 和 `unmounted`。

所有生命周期钩子函数的 `this` 上下文都会自动指向当前调用它的组件实例。

## 生命周期图示

<img src="D:\2024年\blogs\Web Dev\Vue3\02-Essentials\assets\lifecycle.DLmSwRQE.png" alt="Component lifecycle diagram" style="zoom: 33%;" />