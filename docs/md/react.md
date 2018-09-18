# React

> `React` 用于构建用户界面的 JavaScript 库。

<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg">注意：

`React`是一个JavaScript库，因此它需要你熟悉JavaScript。如果你感觉还不够了解，我们建议看看MDN上有关JavaScript的内容，以便你学得更轻松。

在例子中我们也使用了一些`ES6`语法。由于这些语法还比较新，我们也是尽量谨慎的尝试使用他们。但是我们还是建议你去熟悉一下这些内容：`箭头函数`， `类`， `模板字符串`， `let`， 和 `const` 声明等等。

### 生命周期
这个问题要考察的是组件的生命周期

一、初始化阶段：

`getDefaultProps`: 获取实例的默认属性

`getInitialState`: 获取每个实例的初始化状态

`componentWillMount`：组件即将被装载、渲染到页面上

`render`: 组件在这里生成虚拟的DOM节点

`componentDidMount`: 组件真正在被装载之后

二、运行中状态：

`componentWillReceiveProps`: 组件将要接收到属性的时候调用

`shouldComponentUpdate`: 组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止render调用，后面的函数不会被继续执行了）

`componentWillUpdate`: 组件即将更新不能修改属性和状态
 
`render`: 组件重新描绘

`componentDidUpdate`: 组件已经更新

三、销毁阶段：

`componentWillUnmount`: 组件即将销毁

## React中Keys的作用？
> `Keys` 是React在操作列表中元素被修改,添加,或者删除的辅助标识.如果我们不加的话，react会在控制台抛出一段警告,那么这个key具体有什么作用。

Keys可以在DOM中的某些元素被增加或删除的时候帮助React识别哪些元素发生了变化。因此你应当给数组中的每一个元素赋予一个确定的标识。

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

但是，需要指出的一点是，我们在保证数组每项的唯一的标识时，还需要保证其值的稳定性，不能经常改变.

>key 的值要保持稳定且唯一，不能使用`random`来生成key的值。

## react性能优化是哪个周期函数？
`shouldComponentUpdate` 这个方法用来判断是否需要调用render方法重新描绘dom。因为dom的描绘非常消耗性能，如果我们能在shouldComponentUpdate方法中能够写出更优化的dom diff算法，可以极大的提高性能。

## 为什么虚拟dom会提高性能？
虚拟dom相当于在js和真实dom中间加了一个缓存，利用dom diff算法避免了没有必要的dom操作，从而提高性能。

具体实现步骤如下：
1. 用 Java 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中
2. 当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异
3. 把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新了。



