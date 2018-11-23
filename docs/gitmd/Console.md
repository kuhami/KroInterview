## Console 命令

>相比使用 `console.log` 去输出值，我们有更多的方式去调试 `JavaScript`。你以为我要聊调试器么？不不不你想错了。

告诉写 JavaScript 的人应该使用浏览器的调试器去调试代码，这看来很不错，并且肯定有其适用的时间和场合。但是大多数时候你仅仅只想查看一段特定的代码是否执行或者一个变量的值是什么，而不是迷失在 RxJS 代码库或者一个 Promise 库的深处。

然而，尽管 console.log 有其适用的场合，大多数人仍然没有意识到 console 本身除了基础 log 还有许多选择。合理使用这些方法能让调试更简单、更快速，并且更加直观。

## console.log()

很多人不知道经典的  `console.log` 其实有着丰富的函数特性。尽管大多数人只使用 `console.log(object)` 这种语法，但你仍然能写 `console.log(object, otherObject, string)` 并且它会将所有东西都整齐的打印出来。有时候确实很方便。
不止那些，这儿还有另一种格式：`console.log(msg, values)`。这个执行方式和 C 或者 PHP 的 `sprintf` 很相似。

```js
console.log('I like %s but I do not like %s.', 'Skittles', 'pus');
```