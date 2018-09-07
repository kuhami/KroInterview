# JS

> `JavaScript` 是因特网上最流行的脚本语言，它存在于全世界所有 Web 浏览器中，能够增强用户与 Web 站点和 Web 应用程序之间的交互。

## 内置数据类型


JS 中分为七种内置数据类型，七种内置类型又分为两大类型：基本数据类型和引用数据类型（Object）。

基本类型有六种： `null`，`undefined`，`boolean`，`number`，`string`，`symbol`（ES6引入了一种新的原始数据类型[Symbol](http://es6.ruanyifeng.com/#docs/symbol)）。

其中 `JS` 的数字类型是浮点类型的，没有整型。并且浮点类型基于 IEEE 754标准实现，在使用中会遇到某些 [bug](#bug除不尽啊)。`NaN` 也属于 `number` 类型，并且 `NaN` 不等于自身。

对于基本类型来说，如果使用字面量的方式，那么这个变量只是个字面量，只有在必要的时候才会转换为对应的类型。

```js
let a = 111 // 这只是字面量，不是 number 类型
a.toString() // 使用时候才会转换为对象类型
```
对象（Object）是引用数据类型，在使用过程中会遇到浅拷贝和深拷贝的问题。
```js
let a = { name: 'FE' }
let b = a
b.name = 'EF'
console.log(a.name) // EF
```

## Typeof

`typeof` 操作符返回一个字符串，表示未经计算的操作数的类型。

下表总结了 `typeof` 可能的返回值，有关类型和原始值的更多信息，可查看[JavaScript](#内置数据类型)内置数据类型。

| 类型         | 结果                                       |
| ---------- | ---------------------------------------- |
| Undefined  | "undefined"                              |
| Null      | "object"（见下文）                               |
| Boolean  | "boolean"                                       |
| Number   |   "number"                                 |
| String     |            "string"                            |
| Symbol （ECMAScript 6 新增）         |     "symbol"                    |
|宿主对象（由JS环境提供）| Implementation-dependent|
|函数对象| "function"|
|任何其他对象	| "object"|

`typeof` 对于基本类型，除了 `null` 都可以显示正确的类型
``` js
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof b // b 没有声明，但是还会显示 undefined
typeof console.log // 'function'
typeof NaN // 'number'，NaN是"Not-A-Number"的缩写
```
`typeof` 对于数组、对象，都会显示 `object`，显然用`typeof` 来区分它们是不行的，那么怎么区分呢？
``` js
var a = [],b={}
typeof a // 'object'
typeof b // 'object' //显然用`typeof` 来区分它们是不行的
1.`Array.isArray()`
    Array.isArray(a) // true
    Array.isArray(b) // false
2.如果你只是用 typeof 来检查该变量，不论是 `array` 还是 `object`，都将返回 `objec`。
  此问题的一个可行的答案是是检查该变量是不是`object`，
  并且检查该变量是否有数字长度（当为空`array`时长度也可能为0,object的长度为 `undefined`）。
      typeof a === 'object' && !isNaN(a.length)//true
      typeof b === 'object' && !isNaN(b.length)//false
3.`Object.prototype.toString.call()`调用`toString( )`方法试着将该变量转化为代表其类型的`string`
      Object.prototype.toString.call(a)  === '[object Array]'//true
      Object.prototype.toString.call(b)  === '[object Array]'//false
```
对于 `null` 来说，虽然它是基本类型，但是会显示 `object`，这是一个存在很久了的 `Bug`；

````js
typeof null === 'object'; // 从一开始出现JavaScript就是这样的
````
PS：为什么会出现这种情况呢？在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是 0。由于 `null` 代表的是空指针（大多数平台下值为 0x00），因此，`null`的类型标签也成为了 0，`typeof null`就错误的返回了"object"。

## 遍历

说到遍历，首先想到的是数组的遍历，方法不要太多，比如 `for`， `forEach`，`map`，`filter`，`every`，`some`等；`But` 你知道它们的作用吗？

下面来看下用法，首先 定义一个数组：

```js
 var arr = ['1', 'two', 2, true, '二'];
```

知识点：
1. `for`循环，需要知道数组的长度，才能遍历;
2. `forEach`循环，循环数组中每一个元素并采取操作， 没有返回值， 可以不用知道数组长度；

```js
 arr.forEach(function (i, index) { 
     console.log(i, index);
  });
  //返回值： 1,0; two,2; 2,2; true,3; 二,4;
```
 3 . `map`函数，遍历数组每个元素，并回调操作，需要返回值，返回值组成新的数组，原数组不变；

```js
 var newMaparr = arr.map(function (i, index) { 
     return i +',hi';
  });
console.log(arr,newarr);
  //返回值： ['1', 'two', 2, true, '二'],['1,hi', 'two,hi', '2,hi', 'true,hi', '二,hi'];
```
4 . `filter`函数， 过滤通过条件的元素组成一个新数组， 原数组不变；
```js
 var newFilterarr = arr.filter(function (i, index) { 
     return typeof i == "number";
  });
console.log(arr,newFilterarr);
  //返回值： ['1', 'two', 2, true, '二'],[2];
```
5 . `some`函数，遍历数组中是否有符合条件的元素，返回Boolean值

```js
 var newSomearr = arr.some(function (i, index) { 
     return typeof i == "number";
  });
console.log(arr,newSomearr);
  //返回值： ['1', 'two', 2, true, '二'],true;
```
6 . `every`函数， 遍历数组中是否每个元素都符合条件， 返回Boolean值

```js
 var newEveryarr = arr.every(function (i, index) { 
     return typeof i == "number";
  });
console.log(arr,newEveryarr);
  //返回值： ['1', 'two', 2, true, '二'],false;
```

当然， 除了遍历数组之外，还有遍历对象，常用方法 `for ··· in`

```js
 var obj = {a:'test', b:2, c:true}
 for(var i in obj){
    console.log(i,obj[i]);
 }
//返回值： 0,test; 1,2; 2,true;
```
`for ··· in` 不仅可以用来 遍历对象，还可以用来遍历数组， 不过 `i` 对应与数组的`key`值

```js
 var arr = ['1', 'two', 2, true, '二'];
 for(var i in arr){
    console.log(i,arr[i]);
 }
//返回值： 0,1; 1,two; 2,2; 3,true; 4,二;
```

## 闭包

### 变量的作用域