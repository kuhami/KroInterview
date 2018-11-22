## 开卷必读

>人家都说，前端需要每年定期出来面面试，衡量一下自己当前的技术水平以及价值，不管你想不想换工作，此前端面试集锦，都可测试测试你的前端水平，看看自己水平咋样。

`Interview` 直接介绍一些常用的面试一些小技巧和一些经典面试题。

[快速开始](Interview.md)了解详情。

## 实现一个函数，判断输入是不是回文字符串

```js
function run(input) {
  if (typeof input !== 'string') return false;
  return input.split('').reverse().join('') === input;
}
```
## 垂直水平居中问题

两种以上方式实现已知或者未知宽度的垂直水平居中？

```js

// 1
.wraper {
  position: relative;
  .box {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100px;
    height: 100px;
    margin: -50px 0 0 -50px;
  }
}

// 2
.wraper {
  position: relative;
  .box {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

// 3
.wraper {
  .box {
    display: flex;
    justify-content:center;
    align-items: center;
    height: 100px;
  }
}

// 4
.wraper {
  display: table;
  .box {
    display: table-cell;
    vertical-align: middle;
  }
}
```
>面试官问你flex布局，垂直水平居中必须知道宽度吗？答：是，哈哈，你上当了。。。（其实答案是不需要知道高度的）

## 实现Storage
实现Storage，使得该对象为单例，并对localStorage进行封装设置值setItem(key,value)和getItem(key)

```js
var instance = null;
class Storage {
  static getInstance() {
    if (!instance) {
      instance = new Storage();
    }
    return instance;
  }
  setItem = (key, value) => localStorage.setItem(key, value),
  getItem = key => localStorage.getItem(key)
}

```
## 你的技术栈主要是react，那你说说你用react有什么坑点？
1、JSX做表达式判断时候，需要强转为boolean类型，如：

```js
render() {
  const b = 0;
  return <div>
    {
      !!b && <div>这是一段文本</div>
    }
  </div>
}
```
如果不使用 !!b 进行强转数据类型，会在页面里面输出 0。

2、尽量不要在 `componentWillReviceProps` 里使用 `setState`，如果一定要使用，那么需要判断结束条件，不然会出现无限重渲染，导致页面崩溃。

3、给组件添加ref时候，尽量不要使用匿名函数，因为当组件更新的时候，匿名函数会被当做新的prop处理，让ref属性接受到新函数的时候，react内部会先清空ref，也就是会以null为回调参数先执行一次ref这个props，然后在以该组件的实例执行一次ref，所以用匿名函数做ref的时候，有的时候去ref赋值后的属性会取到null。[详情](https://reactjs.org/docs/refs-and-the-dom.html#caveats)

```js

```