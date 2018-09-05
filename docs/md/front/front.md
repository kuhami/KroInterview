# JS

> JavaScript 是因特网上最流行的脚本语言，它存在于全世界所有 Web 浏览器中，能够增强用户与 Web 站点和 Web 应用程序之间的交互。

## 内置数据类型


JS 中分为七种内置数据类型，七种内置类型又分为两大类型：基本数据类型和引用数据类型（Object）。

基本类型有六种： `null`，`undefined`，`boolean`，`number`，`string`，`symbol`（ES6引入了一种新的原始数据类型[Symbol](http://es6.ruanyifeng.com/#docs/symbol)）。

其中 JS 的数字类型是浮点类型的，没有整型。并且浮点类型基于 IEEE 754标准实现，在使用中会遇到某些 [bug](#bug除不尽啊)。NaN 也属于 number 类型，并且 NaN 不等于自身。

对于基本类型来说，如果使用字面量的方式，那么这个变量只是个字面量，只有在必要的时候才会转换为对应的类型。

```js
let a = 111 // 这只是字面量，不是 number 类型
a.toString() // 使用时候才会转换为对象类型
```
对象（Object）是引用类型，在使用过程中会遇到浅拷贝和深拷贝的问题。
```js
let a = { name: 'FE' }
let b = a
b.name = 'EF'
console.log(a.name) // EF
```

## Typeof

typeof 对于基本类型，除了 null 都可以显示正确的类型
