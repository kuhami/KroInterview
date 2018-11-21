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

```js

```
```js

```
```js

```
