<img style="width:220px;background:#2B3A42" src="https://webpack.docschina.org/e0b5805d423a4ec9473ee315250968b2.svg">

>  本质上，`webpack` 是一个现代 `JavaScript` 应用程序的静态模块打包工具。当 webpack 处理应用程序时，它会在内部构建一个 依赖图(dependency graph)，此依赖图会映射项目所需的每个模块，并生成一个或多个 bundle。

## webpack demos 欢迎学习使用
> `Webpack` - 从新手到大师 - 让一切变得简单

## 前言：Webpack是什么
 
 Webpack是一个像Grunt和Gulp一样的前端构建系统
 
 它类似Browserify，可被用作模块打包并且能够做的更多
 
 ```
 $ browserify main.js > bundle.js
 # be equivalent to
 $ webpack main.js bundle.js
 ```
 它的配置文件是Webpack.config.js
 ```js
 // webpack.config.js
 module.exports = {
   entry: './main.js',
   output: {
     filename: 'bundle.js'
   }
 };
 ```
 在有Webpack.config.js之后，你能不输入任何参数调用Webpack
 ```
 $ webpack
 ```
 需要传递参数调用
 ```npm
 $ npm run build
 ```
 你应该知道一些命令行选项
 ```
 webpack --------- 进行一次开发模式编译　　　　
 webpack -p  ----- 进行一次生产模式编译
 webpack --watch  -------- 持续增量式监控编译
 webpack -d ------- 生成source maps
 webpack --colors   ------- 显示静态资源的颜色
 webpack --display-error-details  ------- 显示更多报错信息
 ```
 为了应用运行的准备，你能像下面那样写在你的package.json文件的scripts里
 ```
 // package.json
 {
   // ...
   "scripts": {
     "dev": "webpack-dev-server --devtool eval --progress --colors",
     "deploy": "NODE_ENV=production webpack -p"
   },
   // ...
 }
 ```
## 怎样使用
 
 首先 全局安装 `Webpack` 和 `webpack-dev-server`
 
 ``` npm
 $ npm i -g webpack webpack-dev-server
 ```
 然后 `clone` 项目`webpack-demos`
 
 ```npm
 $ git clone https://github.com/kuhami/webpack-demos.git
 ```
 安装依赖项
 ```npm
 $ cd webpack-demos
 $ npm install
 ```
 现在可以运行 `webpack-demos` 下的文件了
 ```
 $ cd demo01
 $ npm run dev
 ```
 用你的浏览器打开http://127.0.0.1:8080
 
## 结语

这里真的没有过多的总结。在你可能只想得到比 `console.log(pet)` 的信息更多一点，并且不太需要调试器的时候，上面这些工具都可能帮到你。

也许最有用的是 `console.table`，但是其他方法也都有其适用的场景。在我们想要调试一些东西时，我热衷于使用 `console.assert`，但那也只在某种特殊情况下。







