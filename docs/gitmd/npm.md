<img src="https://raw.githubusercontent.com/kuhami/KroInterview/master/docs/img/md/npm.jpeg">

>  `nodejs` 社区乃至 Web 前端工程化领域发展到今天，作为 node 自带的包管理工具的 npm 已经成为每个前端开发者必备的工具。

本文介绍一些常用的`npm`命令和一些小技巧。

## 开卷必读
*如果之前未使用过 `Git`，可以学习[Git小白教程](http://rogerdudler.github.io/git-guide/index.zh.html)入门*

1. **一定要先测试命令的效果后**，再用于工作环境中，以防造成不能弥补的后果！**到时候别拿着砍刀来找我**
2. 所有的命令都在`git version 2.7.4 (Apple Git-66)`下测试通过
3. 统一概念：
	- 工作区：改动（增删文件和内容）
	- 暂存区：输入命令：`git add 改动的文件名`，此次改动就放到了‘暂存区’
	- 本地仓库(简称：本地)：输入命令：`git commit 此次修改的描述`，此次改动就放到了’本地仓库’，每个commit，我叫它为一个‘版本’。
	- 远程仓库(简称：远程)：输入命令：`git push 远程仓库`，此次改动就放到了‘远程仓库’（GitHub等)
	- commit-id：输出命令：`git log`，最上面那行`commit xxxxxx`，后面的字符串就是commit-id
4. 如果喜欢这个项目，欢迎Star、提交Pr、[反馈问题](https://github.com/kuhami/KroInterview/issues)😊

## 展示帮助信息
```sh
git help -g
```

**[⬆ 返回顶部](#开卷必读)**


