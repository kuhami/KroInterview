<img style="width:220px" src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/md/npm.png">

>  `nodejs` 社区乃至 Web 前端工程化领域发展到今天，作为 node 自带的包管理工具的 npm 已经成为每个前端开发者必备的工具。

本文介绍一些常用的`npm`命令和一些小技巧。

## 开卷必读
*如果之前未使用过 `npm`，可以学习[npm 使用介绍](https://www.npmjs.cn/)入门*

1. **一定要先测试命令的效果后**，再用于工作环境中，以防造成不能弥补的后果！**到时候别拿着砍刀来找我**
2. 如果喜欢这个项目，欢迎Star、提交Pr、[反馈问题](https://github.com/kuhami/KroInterview/issues)😊

## npm init

我们都知道 package.json 文件是用来定义一个 package 的描述文件, 也知道`npm init`命令用来初始化一个简单的 package.json 文件，执行该命令后终端会依次询问 name, version, description 等字段。

### npm 执行默认行为

 而如果想要偷懒步免去一直按 enter，在命令后追加 --yes 参数即可，其作用与一路下一步相同。
 
```sh
npm init --yes
```

**[⬆ 返回顶部](#开卷必读)**


