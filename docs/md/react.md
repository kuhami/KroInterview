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






