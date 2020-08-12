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

```
在组件挂载完成后调用，且全局只调用一次，在该生命周期函数内：
1.可以在这里使用refs，获取真实dom元素
2.该钩子内也可以发起异步请求，并在异步请求中可以进行setState
```

二、运行中状态：

`componentWillReceiveProps`: 组件将要接收到属性的时候调用

`shouldComponentUpdate`: 组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止render调用，后面的函数不会被继续执行了）

`componentWillUpdate`: 组件即将更新不能修改属性和状态
 
`render`: 组件重新描绘

`componentDidUpdate`: 组件已经更新

三、销毁阶段：

`componentWillUnmount`: 组件即将销毁

## react性能优化是哪个周期函数？
`shouldComponentUpdate` 这个方法用来判断是否需要调用render方法重新描绘dom。因为dom的描绘非常消耗性能，如果我们能在shouldComponentUpdate方法中能够写出更优化的dom diff算法，可以极大的提高性能。

## React 中 refs 的作用是什么？
> Refs 是一个 获取 DOM节点或 React元素实例的工具。在 React 中 Refs 提供了一种方式，允许用户访问DOM 节点或者在render方法中创建的React元素。

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

## React 中有三种构建组件的方式？

1. 函数式定义的 `无状态组件`
2. es5原生方式 `React.createClass` 定义的组件
3. es6形式的 `extends React.Component` 定义的组件

## 调用 setState 之后发生了什么？

1. 在代码中调用setState函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。
2. 经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个UI界面。
3. 在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。
4. 在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。

## 为什么建议传递给 setState 的参数是一个 callback 而不是一个对象?
> 因为 this.props 和 this.state 的更新可能是异步的，不能依赖它们的值去计算下一个 state。

## react diff 原理 ?(常考，大厂必考）
> [react diff 原理](https://zhuanlan.zhihu.com/p/20346379)
## 为什么虚拟dom会提高性能？
虚拟dom相当于在js和真实dom中间加了一个缓存，利用dom diff算法避免了没有必要的dom操作，从而提高性能。

具体实现步骤如下：
1. 用 Java 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中
2. 当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异
3. 把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新了。

## 除了在构造函数中绑定 This，还有其它方式吗?

1. 使用属性初始值设定项(property initializers)来正确绑定回调
2. create-react-app 也是默认支持的
3. 在回调中你可以使用箭头函数，但问题是每次组件渲染时都会创建一个新的回调

## 调用 Super(Props) 的目的是什么?
> 在 super() 被调用之前，子类是不能使用 this 的，在 ES2015 中，子类必须在 constructor 中调用 super()。传递 props 给 super() 的原因则是便于(在子类中)能在 constructor 访问 this.props。

## 简述 flux 思想?

> Flux 的最大特点，就是数据的"单向流动"。

1. 用户访问 View
2. View 发出用户的 Action
3. Dispatcher 收到 Action，要求 Store 进行相应的更新
4. Store 更新后，发出一个"change"事件
5. View 收到"change"事件后，更新页面

## createElement和cloneElement有什么区别？

> createElement 函数是 JSX 编译之后使用的创建 React Element 的函数，而 cloneElement 则是用于复制某个元素并传入新的 Props。

## 如何告诉 React 它应该编译生产环境版本？

通常情况下我们会使用 Webpack 的 DefinePlugin 方法来将 NODE_ENV 变量值设置为 production。编译版本中 React 会忽略 propType 验证以及其他的告警信息，同时还会降低代码库的大小，React 使用了 Uglify 插件来移除生产环境下不必要的注释等信息。

## 展示组件(Presentational component)和容器组件(Container component)之间有何不同?
`展示组件`
1. 关注页面的展示效果（外观）
2. 内部可以包含展示组件和容器组件，通常会包含一些自己的DOM结构和样式
3. 通常允许通过this.props.children方式来包含其他组件。
4. 对应用程序的其他部分没有依赖关系，例如Flux操作或store。
5. 不用关心数据是怎么加载和变动的。
6. 只能通过props的方式接收数据和进行回调(callback)操作。
7. 很少拥有自己的状态，即使有也是用于展示UI状态的。
8. 通常会写成函数式组件除非该组件需要自己的状态，生命周期或者做一些性能优化。

`容器组件`
1. 关注应用的是如何工作的
2. 内部可以包含容器组件和展示组件
3. 提供数据和行为给其他的展示组件或容器组件
4. 往往是有状态的，因为它们倾向于作为数据源
5. 通常使用高阶组件生成，例如React Redux的connect。

## (组件的)状态(state)和属性(props)之间有何不同？

`State` 是一种数据结构，用于组件挂载时所需数据的默认值。State 可能会随着时间的推移而发生突变，但多数时候是作为用户事件行为的结果。

`Props`(properties 的简写)则是组件的配置。props 由父组件传递给子组件，并且就子组件而言，props 是不可变的(immutable)。组件不能改变自身的 props，但是可以把其子组件的 props 放在一起(统一管理)。Props 也不仅仅是数据–回调函数也可以通过 props 传递。

## 何为受控组件(controlled component)？

在 HTML 中，表单元素（`如<input>、 <textarea> 和 <select>`）通常自己维护 state，并根据用户输入进行更新。而在 React 中，可变状态（mutable state）通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新。

我们可以把两者结合起来，使 React 的 state 成为“唯一数据源”。渲染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”。

## React react组件的划分业务组件技术组件？
1. 根据组件的职责通常把组件分为UI组件和容器组件。
2. UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
3. 两者通过 React-Redux 提供 connect ⽅法联系起来

## redux中间件

## 了解 redux 么，说一下 redux 吧

## redux有什么缺点?
1. 一个组件所需要的数据，必须甶父组件传过来，而不能像flux中直接从store取。

2. 当一个组件相关数据更新吋，即使父组件不需要用到这个组件，
父组件还是会重新render,
可能会 有效率影响，或者需要写复杂的shouldComponentUpdate进行判断。

## Immutable
关于`Immutable`的定义，官方文档是这样说的：
> Immutable data encourages pure functions (data-in, data-out) and lends itself to much simpler application development and enabling techniques from functional programming such as lazy evaluation.
  
  简而言之，`Immutable`数据就是一旦创建，就不能更改的数据。每当对`Immutable`对象进行修改的时候，就会返回一个新的`Immutable`对象，以此来保证数据的不可变。对于`Immutable`的好处及介绍，大家可以参考Immutable 详解及 React 中实践，这篇文章介绍的很清楚。
  
  因为`Immutable`的官方文档有点晦涩难懂，本文只是用来整理`Immutable`常用的API的使用，便于使用与查询，想了解更详细的内容，[请戳这里~](https://facebook.github.io/immutable-js/docs/#/)

### Immutable 的几种数据类型
1. `List`: 有序索引集，类似JavaScript中的Array。
2. `Map`: 无序索引集，类似JavaScript中的Object。

用的最多就是`List`和`Map`，所以在这里主要介绍这两种数据类型的API。

### API的使用

<h5 style="font-size: 18px;">1.fromJS()</h5>

作用：将一个`js`数据转换为`Immutable`类型的数据。

用法：`fromJS(value, converter)`

简介：value是要转变的数据，converter是要做的操作。第二个参数可不填，默认情况会将数组准换为List类型，将对象转换为Map类型，其余不做操作。

代码实现：

```js
  const obj = Immutable.fromJS({a:'123',b:'234'},function (key, value, path) {
      console.log(key, value, path)
      return isIndexed(value) ? value.toList() : value.toOrderedMap())
  })
```
<h5 style="font-size: 18px;">2.toJS()</h5>

作用：将一个`Immutable`数据转换为`JS`类型的数据。

用法：`value.toJS()`

<h5 style="font-size: 18px;">3.is()</h5>

作用：对两个对象进行比较。

用法：`is(map1,map2)`

简介：和js中对象的比较不同，在js中比较两个对象比较的是地址，但是在Immutable中比较的是这个对象`hashCode`和`valueOf`，只要两个对象的hashCode相等，值就是相同的，避免了深度遍历，提高了性能。

代码实现：
```js
import { Map, is } from 'immutable'
const map1 = Map({ a: 1, b: 1, c: 1 })
const map2 = Map({ a: 1, b: 1, c: 1 })
map1 === map2   //false
Object.is(map1, map2) // false
is(map1, map2) // true
```
<h5 style="font-size: 18px;">4.List 和 Map</h5>

作用：用来创建一个新的`List`/`Map`对象
>`List() 和 Map()`

用法:
```js
//List

List(): List<any>
List<T>(): List<T>

//Map

Map(): Map<any>
Map<T>(): Map<T>
```

> `List.of() 和 Map.of()`

作用：创建一个新的包含`value`的`List/Map`对象

用法：

```js
List.of<T>(...values: Array<T>): List<T>

Map.of<T>(...values: Object<T>): Map<T>
```
<h5 style="font-size: 18px;">判断</h5>

> `List.isList() 和 Map.isMap()`

作用：判断一个数据结构是不是`List/Map`类型

用法：

```js
List.isList(maybeList: any): boolean

Map.isMap(maybeMap: any): boolean
```
<h5 style="font-size: 18px;">长度</h5>

>`size`

作用：获取`List/Map`的长度

<h5 style="font-size: 18px;">数据读取</h5>

> `get() 、 getIn()`

作用：获取数据结构中的数据

>`has() 、 hasIn()`

作用:判断是否存在某一个`key`

用法：

```js
Immutable.fromJS([1,2,3,{a:4,b:5}]).has('0'); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).has('0'); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).hasIn([3,'b']) //true
```

>`includes()`

作用：判断是否存在某一个`value`

用法：

```js
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(2); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes('2'); //false 不包含字符2
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(5); //false 
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes({a:4,b:5}) //false
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(Immutable.fromJS({a:4,b:5})) //true
```

<h5 style="font-size: 18px;">数据修改</h5>

注：这里对于数据的修改，是对原数据进行操作后的值赋值给一个新的数据，并不会对原数据进行修改，因为Immutable是不可变的数据类型。

>`设置set（）`

作用：设置第一层`key`、`index`的值

用法：

```js
set(index: number, value: T): List<T>
set(key: K, value: V): this
```
>`setIn()`

作用：设置深层结构中某属性的值

用法：

```js
setIn(keyPath: Iterable<any>, value: any): this
```
用法与set()一样，只是第一个参数是一个数组，代表要设置的属性所在的位置

>`删除 delete`

用来删除深层数据，用法参考setIn

>`更新 update()`

```js
update(index: number, updater: (value: T) => T): this //List
update(key: K, updater: (value: V) => V): this  //Map
```

代码示例：

```js
////List
const list = List([ 'a', 'b', 'c' ])
const result = list.update(2, val => val.toUpperCase())

///Map
const aMap = Map({ key: 'value' })
const newMap = aMap.update('key', value => value + value)
```

>`updateIn()`

用法参考setIn

>`清除 clear()`

作用：清楚所有数据

用法：clear():this

代码事例：

```js
Map({ key: 'value' }).clear()  //Map
List([ 1, 2, 3, 4 ]).clear()   // List
```
<h5 style="font-size: 18px;">merge</h5>

作用：浅合并，新数据与旧数据对比，旧数据中不存在的属性直接添加，就数据中已存在的属性用新数据中的覆盖

<h5 style="font-size: 18px;">序列算法</h5>

>`concat()`

作用：对象的拼接，用法与js数组中的`concat()`相同，返回一个新的对象。

用法：`const List = list1.concat(list2)`

>`map()`

作用：遍历整个对象，对`Map/List`元素进行操作，返回一个新的对象。

用法：

```js
Map({a:1,b:2}).map(val=>10*val)
//Map{a:10,b:20}
```

>`Map特有的mapKey()`

作用：遍历整个对象，对Map元素的key进行操作，返回一个新的对象。

用法：

```js
Map({a:1,b:2}).map((key,val)=>{
  return [key+'l',val*10]
})
//Map{al:10,bl:20}
```

>`过滤 filter`

作用：返回一个新的对象，包括所有满足过滤条件的元素

用法：

```js
Map({a:1,b:2}).filter((key,val)=>{
  return val == 2
})
//Map{b:2}
```

还有一个filterNot()方法，与此方法正好相反。





