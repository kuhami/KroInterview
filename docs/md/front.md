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
<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg"><front style="color:red">经典面试题：</front>`typeof` 对于数组、对象，都会显示 `object`，显然用`typeof` 来区分它们是不行的，那么怎么区分呢？
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
3.instanceof instanceof检测的是原型
      [] instanceof Array; //true
      {} instanceof Object;//true 
4.`Object.prototype.toString.call()`调用`toString( )`方法试着将该变量转化为代表其类型的`string`
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

<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg">知识点：
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
闭包是 `js` 中的一大特色，也是一大难点。简单来说，所谓闭包就是说，一个函数能够访问其函数外部作用域中的变量。

闭包的三大特点为：
1. 函数嵌套函数
2. 内部函数可以访问外部函数的变量
3. 参数和变量不会被回收

举例来说：
```js
function test(){
     var a=1;
     return function(){
       alert(a);
     }
   }
   var foo = test();
   foo(); //弹出a的值
```
这个例子中，变量 `a` 在 `test` 方法外部是无法访问的，但 `test` 方法里面，嵌套了一个匿名函数，通过`return`返回，`test`作用域中的变量`a`，
可以在匿名函数中访问。并且当`test`方法执行后，变量`a`所占内存并不会释放，以达到嵌套的函数还可以访问的目的。

<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg">闭包的作用在于，可以通过闭包，设计私有变量及方法。

举个私有变量的例子：
```js
var aaa = (function(){
        var a = 1;
        function bbb(){
                a++;
                alert(a);
        }
        function ccc(){
                a++;
                alert(a);
        }
        return {
                b:bbb, //json结构
                c:ccc
        }
    })();
    alert(aaa.a) //undefined 
    aaa.b();     //2
    aaa.c();     //3
```

<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg">总结：
1. 闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量。闭包的缺点就是常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。

2. 不必纠结到底怎样才算闭包，其实你写的每一个函数都算作闭包，即使是全局函数，你访问函数外部的全局变量时，就是闭包
的体现。

<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg"><front style="color:red">经典面试题：</front>循环中使用闭包解决 `var` 定义函数的问题
```js
for ( var i=1; i<=5; i++) {
	setTimeout( function timer() {
		console.log( i );
	}, i*1000 );
}
```
首先因为`setTimeout`是个异步函数，所有会先把循环全部执行完毕，这时候`i`就是`6` 了，所以会输出一堆 `6`。

解决办法两种，第一种使用闭包
```js
for (var i = 1; i <= 5; i++) {
  (function(j) {
    setTimeout(function timer() {
      console.log(j);
    }, j * 1000);
  })(i);
}
```
第二种就是使用 `setTimeout` 的第三个参数
```js
for ( let i=1; i<=5; i++) {
	setTimeout( function timer() {
		console.log( i );
	}, i*1000 );
}
```
因为对于 `let` 来说，他会创建一个块级作用域，相当于
```js
{ // 形成块级作用域
  let i = 0
  {
    let ii = i
    setTimeout( function timer() {
        console.log( i );
    }, i*1000 );
  }
  i++
  {
    let ii = i
  }
  i++
  {
    let ii = i
  }
  ...
}
```

## new

>众所周知：没有对象怎么办？那就new一个！现在我们就来剖析一下原生JS中new关键字内部的工作原理。

要创建 Person 的新实例，必须使用 new 操作符。以这种方式调用构造函数实际上会经历以下 4
个步骤：
1. 新生成了一个对象
2. 新对象隐式原型链接到函数原型
3. 调用函数绑定this
4. 返回新对象

核心代码：
````js
function _new(fun) {
  return function() {
    let obj = {
      __proto__: fun.prototype
    }
    fun.apply(obj, arguments)
    return obj
  }
}
````
测试用例：
```js
function person(name, age) {
  this.name = name
  this.age = age
}
let obj = _new(person)('LL', 100)
console.log(obj) //{name: 'LL', age: 100}
```
## 深浅拷贝
```js
let a = {
    age : 1
}
let b = a
a.age = 2
console.log(b.age) // 2
```
从上述例子中我们可以发现，如果给一个变量赋值一个对象，那么两者的值会是同一个引用，其中一方改变，另一方也会相应改变。

通常在开发中我们不希望出现这样的问题，我们可以使用浅拷贝来解决这个问题。
### 浅拷贝
`Object.assign`方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用.
```js
let a = {
    age: 1
}
let b = Object.assign({}, a)
a.age = 2
console.log(b.age) // 1
```
通常`浅拷贝`就能解决大部分问题了，但是当我们遇到如下情况就需要使用到深拷贝了
```js
let a = {
    age: 1,
    jobs: {
        first: 'FE'
    }
}
let b = Object.assign({}, a)
a.jobs.first = 'native'
console.log(b.jobs.first) // native
```
`浅拷贝` 只解决了第一层的问题，如果接下去的值中还有对象的话，那么就又回到刚开始的话题了，两者享有相同的引用。要解决这个问题，我们需要引入深拷贝。

### 深拷贝

* 递归实现

````js
function deepCopy(oldObj, newObj) {
    var newObj = newObj || {}
    for (var i in oldObj) {
        if (oldObj[i] instanceof Object) {
            if (oldObj[i].constructor === Array) {
                newObj[i] = []
            } else {
                newObj[i] = {}
            }
            deepCopy(oldObj[i], newObj[i])
        } else {
            newObj[i] = oldObj[i]
        }
    }
    return newObj
}

var obj1 = {
    country: 'China',
    city: ['Beijing,Shanghai,Nanjing'],
    age: 16,
    friends: {
        name: 'dot',
        sex: 'female',
        age: null
    }
}

var obj2 = {
    name: 'dolby',
    fav: 'food'
}

var obj3 = null

console.log(deepCopy(obj1, obj2))
//{ name: 'dolby',
//   fav: 'food',
//   country: 'China',
//   city: [ 'Beijing,Shanghai,Nanjing' ],
//   age: 16,
//   friends: { name: 'dot', sex: 'female', age: null } }

console.log(deepCopy(obj1, obj3))
//{ country: 'China',
//   city: [ 'Beijing,Shanghai,Nanjing' ],
//   age: 16,
//   friends: { name: 'dot', sex: 'female', age: null } }
````
* `JSON`对象的`parse()`和`stringify()`方法

`JSON`对象是`ES5`中引入的新的类型（支持的浏览器为IE8+），`JSON`对象`parse`方法可以将JSON字符串反序列化成JS对象，`stringify`方法可以将JS对象序列化成JSON字符串，借助这两个方法，也可以实现对象的深复制。
```js
var source = {
    name:"source",
    child:{
        name:"child"
    }
}
var target = JSON.parse(JSON.stringify(source));
//改变target的name属性
target.name = "target";
console.log(source.name);   //source
console.log(target.name);   //target
//改变target的child
target.child.name = "target child";
console.log(source.child.name);  //child
console.log(target.child.name);  //target child
```
从代码的输出可以看出，复制后的target与source是完全隔离的，二者不会相互影响。

这个方法使用较为简单，可以满足基本的深复制需求，而且能够处理JSON格式能表示的所有数据类型，但是对于正则表达式类型、函数类型等无法进行深复制(而且会直接丢失相应的值)，同时如果对象中存在循环引用的情况也无法正确处理

* `jQuery`库中的`extend`复制方法

在 jQuery 中可通过添加一个参数来实现递归extend。调用$.extend(true, {}, ...)就可以实现深复制。jQuery 无法正确深复制 JSON 对象以外的对象.
```js
var x = {
    a: 1,
    b: { f: { g: 1 } },
    c: [ 1, 2, 3 ]
};

var y = $.extend({}, x),          //浅复制
    z = $.extend(true, {}, x);    //深复制

y.b.f === x.b.f       // true
z.b.f === x.b.f       // false
```
## 截取Url获取参数
<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/lamp.jpg"><front style="color:red">经典面试题：</front> 如何获取浏览器`URL`中查询字符串中的参数

| 方法         | 描述                                       |
| ---------- | ---------------------------------------- |
| exec()  | 用正则表达式模式在字符串中查找，并返回该查找结果的第一个值（数组），如果匹配失败，返回null。  |
| decodeURIComponent()      | 函数可对 encodeURIComponent() 函数编码的 URI 进行解码。             |


````js
/* 截取Url
 * @param name	要截取的参数名
 * 例如：http://localhost:3000/index.html?name=张三&&age=24&&sex=male
 * 用法：getParam("name") // 张三
 *      getParam("age")  // 24
 */
function getParam(name) {
	var search = document.location.search;
	var pattern = new RegExp("[?&]" + name + "\=([^&]+)", "g");
	var matcher = pattern.exec(search);
	var items = null;
	if (null != matcher) {
		try {
			items = decodeURIComponent(decodeURIComponent(matcher[1]));
		} catch(e) {
			try {
				items = decodeURIComponent(matcher[1]);
			} catch(e) {
				items = matcher[1];
			}
		}
	}
	return items;
};
````
## 存储
> `cookie`、`localStorage`和`sessionStorage`的区别

| 特性         | cookie     | sessionStorage |                  localStorage                |
| ---------- | --------- | -------------------- | ----------- |
|数据生命期 | 一般由服务器生成，可以设置过期时间，默认关闭浏览器失效|页面会话期间可用| 除非数据被清除，否则一直存在.|
|存放数据大小 | 4K左右（因为每次http请求都会携带cookie）|一般5M或更大| 一般5M或更大|
|与服务端通信|每次都会携带在 header 中，对于请求性能影响|不参与|不参与|

从上表可以看到，`cookie` 已经不建议用于存储。如果没有大量数据存储需求的话，可以使用 `localStorage` 和 `sessionStorage` 。对于不怎么改变的数据尽量使用 `localStorage` 存储，否则可以用 `sessionStorage` 存储。

无论是`cookie`还是HTML5的本地存储，都是相对不安全的，很容易受到各种各样的攻击，特别是HTML5的存储空间大，给了攻击者更大的发挥平台，所以都不能用来存储敏感信息。登录信息等重要信息还是存放到服务器里比较好

对于 `cookie`，我们还需要注意安全性。

| 属性         | 作用     |
| ---------- | --------- |
|value | 如果用于保存用户登录态，应该将该值加密，不能使用明文的用户标识|
|http-only | 不能通过 JS 访问 Cookie，减少 XSS 攻击|
|secure | 只能在协议为 HTTPS 的请求中携带|
|same-site | 规定浏览器不能在跨域请求中携带 Cookie，减少 CSRF 攻击|

## 跨域

跨域是指一个域下的文档或脚本试图去请求另一个域下的资源，这里跨域是广义的。

广义的跨域：
```js
1.) 资源跳转： A链接、重定向、表单提交
2.) 资源嵌入： <link>、<script>、<img>、<frame>等dom标签，还有样式中background:url()、@font-face()等文件外链
3.) 脚本请求： js发起的ajax请求、dom和js对象的跨域操作等
```
其实我们通常所说的跨域是狭义的，是由浏览器同源策略限制的一类请求场景。

### 什么是同源策略？

说到跨域就不得不提“同源策略”。
 
`同源策略`是浏览器针对恶意的代码所进行的措施，为了防止世界被破坏，为了保护世界的和平，Web浏览器，采取了同源策略，只允许脚本读取和所属文档来源相同的窗口和文档的属性。
那么，怎么判断文档来源是否相同呢？很简单，看三个部分： `协议`、`主机`、`端口号`。只要其中一个部分不同，则不同源。

### 常见跨域场景

| URL         | 说明     | 是否允许通信| 
| ---------- | --------- |---------| 
|http://www.domain.com/a.js <br/> http://www.domain.com/b.js <br/> http://www.domain.com/lab/c.js | 同一域名，不同文件或路径|允许|
|http://www.domain.com:8000/a.js <br/> http://www.domain.com/b.js | 同一域名，不同端口|不允许|
|http://www.domain.com/a.js <br/> https://www.domain.com/b.js  | 同一域名，不同协议|不允许|
|http://www.domain.com/a.js <br/> http://192.168.4.12/b.js | 域名和域名对应相同ip|不允许|
|http://www.domain.com/a.js <br/> http://x.domain.com/b.js <br/> http://domain.com/c.js | 主域相同，子域不同|不允许|
|http://www.domain1.com/a.js <br/> http://www.domain2.com/b.js | 不同域名 |不允许|

### 如何跨域

1. JSONP

`JSONP`由两部分组成： 回调函数和数据。
原理：通过动态`<script>`元素来使用，可以通过`src`属性指定一个跨域`URL`。
````js
<script>
    var script = document.createElement('script');
    script.type = 'text/javascript';

    // 传参并指定回调执行函数为onBack
    script.src = 'http://www.domain2.com:8080/login?user=admin&callback=onBack';
    document.head.appendChild(script);

    // 回调执行函数
    function onBack(res) {
        alert(JSON.stringify(res));
    }
 </script>
````
服务端返回如下（返回时即执行全局函数）：
```js
onBack({"status": true, "user": "admin"})
```
2 .除此之外，还可以利用`jQuery`来实现。
```js
$.ajax({
    url: 'http://www.domain2.com:8080/login',
    type: 'get',
    dataType: 'jsonp',  // 请求方式为jsonp
    jsonpCallback: "onBack",    // 自定义回调函数名
    data: {}
});
```
优点:
1. 兼容性强。
2. 简单易用，能之间访问响应文本，支持浏览器与服务器之间双向通信。

不足：
1. 只能用GET方法，不能使用POST方法
2. 无法判断请求是否失败，没有错误处理。

## JS继承
> JS作为面向对象的弱类型语言，继承也是其非常强大的特性之一。那么如何在JS中实现继承呢？让我们拭目以待。

<h3>JS继承的实现方式</h3>

既然要实现继承，那么首先我们得有一个父类，代码如下：
````js
// 定义一个动物类
function Animal (name) {
  // 属性
  this.name = name || 'Animal';
  // 实例方法
  this.sleep = function(){
    console.log(this.name + '正在睡觉！');
  }
}
// 原型方法
Animal.prototype.eat = function(food) {
  console.log(this.name + '正在吃：' + food);
};
````
### 原型链继承
核心： 将父类的实例作为子类的原型
```js
function Cat(){ 
}
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';

//　Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.eat('fish'));
console.log(cat.sleep());
console.log(cat instanceof Animal); //true 
console.log(cat instanceof Cat); //true
```

优点：
1. 非常纯粹的继承关系，实例是子类的实例，也是父类的实例
2. 父类新增原型方法/原型属性，子类都能访问到
3. 简单，易于实现

缺点：
1. 要想为子类新增属性和方法，必须要在new Animal()这样的语句之后执行，不能放到构造器中
2. 无法实现多继承
3. 创建子类实例时，无法向父类构造函数传参

### 构造继承

核心：使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）

```js
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // false
console.log(cat instanceof Cat); // true
```

优点：
1. 解决了1中，子类实例共享父类引用属性的问题
2. 创建子类实例时，可以向父类传递参数
3. 可以实现多继承（call多个父类对象）

缺点：
1. 实例并不是父类的实例，只是子类的实例
2. 只能继承父类的实例属性和方法，不能继承原型属性/方法
3. 无法实现函数复用，每个子类都有父类实例函数的副本，影响性能

### 实例继承

核心：为父类实例添加新特性，作为子类实例返回

```js
function Cat(name){
  var instance = new Animal();
  instance.name = name || 'Tom';
  return instance;
}

// Test Code
var cat = new Cat();
console.log(cat.name);
console.log(cat.sleep());
console.log(cat instanceof Animal); // true
console.log(cat instanceof Cat); // false
```

优点：
1. 不限制调用方式，不管是new 子类()还是子类(),返回的对象具有相同的效果

缺点：
1. 实例是父类的实例，不是子类的实例
1. 不支持多继承

## ES6
### ES6常用特性
> `let`, `const`, `class`, `extends`, `super`, `arrow` `functions`, `template string`, `destructuring`, `default`, `rest arguments` 这些是ES6最常用的几个语法，基本上学会它们，就可以满足我们日常的使用！下面就用用最通俗易懂的语言和例子来讲解它们。
    
### Set 和 Map 数据结构
与 Array 增、删、改、查对比

````js
let map = new Map(); 
let set = new Set(); 
let array = []; 
// 增 
 map.set('t', 1); 
 set.add( { t : 1 } ); 
 array.push( { t:1 } );
 console.info( map, set, array ); 
 // Map { 't' => 1 } Set { { t: 1 } } [ { t: 1 } ] 
 
// 查 
let map_exist = map.has( 't' ); 
let set_exist = set.has( {t:1} ); 
let array_exist = array.find(item => item.t) 
console.info(map_exist, set_exist, array_exist); 
//true false { t: 1 } 

// 改
map.set('t', 2); 
set.forEach(item => item.t ? item.t = 2:'');
array.forEach(item => item.t ? item.t = 2:''); 
console.info(map, set, array); 
// Map { 't' => 2 } Set { { t: 2 } } [ { t: 2 } ] 
// 删 
map.delete('t'); 
set.forEach(item => item.t ? set.delete(item):''); 
let index = array.findIndex(item => item.t); array.splice(index,1); 
console.info(map, set, array); 
// Map {} Set {} []
````

### Class 的继承

>Class 可以通过extends关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

```js
class Point {
}

class ColorPoint extends Point {
}
```