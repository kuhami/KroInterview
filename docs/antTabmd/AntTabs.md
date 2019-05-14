# Ant Tabs（pro 2.0）

本文介绍`Ant Tabs`一些 新增的功能和原理及思路介绍及更新日志。

![](https://raw.githubusercontent.com/kuhami/react-ant/master/public/ant.jpeg)
## 实现多页签的原理及思路

 `Ant Tabs` 基于 `Ant Design Pro 2.0` 基础上修改的多标签Tabs，修改此多标签也是工作上的需求，原来后台项目也是基于 `Antd Design` 来开发的，在 github上demo也不是很多，基本上也不符合自己的需求，于是就本着`自己动手,丰衣足食`的思想，自己在`Antd Design`的基础上修改了部分文件。
   
  但是，中间也走了很多弯路，踩了很多坑，修改了多个版本最终才成了现在的需求，不过我觉得还可以，仅供大家参考。
       
### 引入 ant Tabs
主要修改文件 `react-ant/src/layouts/BasicLayout.js` 中引入`Tabs` 组件

代码解析
```js
constructor(props) {
    super(props);
    const {routes} = props.route,routeKey = '/home/home'; // routeKey 为设置首页设置 试试 '/dashboard/analysis' 或其他key值
    const tabLists = this.updateTree(routes);
    let tabList=[];
    tabLists.map((v) => {
      if(v.key === routeKey){
        if(tabList.length === 0){
          v.closable = false
          tabList.push(v);
        }
      }
    });
    this.state = ({
        tabList:tabList,
        tabListKey:[routeKey],
        activeKey:routeKey,
        routeKey
    })

    this.getPageTitle = memoizeOne(this.getPageTitle);
    this.matchParamsPath = memoizeOne(this.matchParamsPath, isEqual);
  }
```
- tabList: 用来存储打开的多标签
- tabListKe:用来判断 tabList 是否重复保持tabList标签唯一性
- activeKey:当前激活 tab 面板的 key
- routeKey: 为设置首页设置 试试 '/dashboard/analysis' 或其他key值

```js
updateTree = data => {
    const treeData = data;
    const treeList = [];
    // 递归获取树列表
    const getTreeList = data => {
      data.forEach(node => {
        if(!node.level){
          treeList.push({ tab: node.name, key: node.path,locale:node.locale,closable:true,content:node.component });
        }
        if (node.routes && node.routes.length > 0) { //!node.hideChildrenInMenu &&
          getTreeList(node.routes);
        }
      });
    };
    getTreeList(treeData);
    return treeList;
  };
```
- updateTree函数：为递归 `routes` 多维数据变成一维数据
```js
 <SiderMenu
            logo={logo}
            theme={navTheme}
            onCollapse={this.handleMenuCollapse}
            menuData={menuData}
            isMobile={isMobile}
            {...this.props}
            onHandlePage ={this.onHandlePage}
          />
```

- onHandlePage: 点击左侧及页面内触发的函数
```js
 {hidenAntTabs ?
              (<Authorized authority={routerConfig} noMatch={<Exception403 />}>
              {children}
                </Authorized>) :
              (this.state.tabList && this.state.tabList.length ? (
              <Tabs
                // className={styles.tabs}
                activeKey={activeKey}
                onChange={this.onChange}
                tabBarExtraContent={operations}
                tabBarStyle={{background:'#fff'}}
                tabPosition="top"
                tabBarGutter={-1}
                hideAdd
                type="editable-card"
                onEdit={this.onEdit}
              >
                {this.state.tabList.map(item => (
                  <TabPane tab={item.tab} key={item.key} closable={item.closable}>
                    <Authorized authority={routerConfig} noMatch={<Exception403 />}>
                      {/*{item.content}*/}
                      <Route key={item.key} path={item.path} component={item.content} exact={item.exact} />
                    </Authorized>
                  </TabPane>
                ))}
              </Tabs>
            ) : null)}
```
- hidenAntTabs：添加这个字段为在抽屉屑中控制是否显示多标签



## 相关链接
- [Ant Tabs 源码地址](https://github.com/kuhami/react-ant)
- [Ant Tabs 文档地址](https://kuhami.github.io/KroInterview/antTabs.html#/AntTabs)
- [Ant Tabs 更新日志](https://kuhami.github.io/KroInterview/antTabs.html#/AntTabs)

## 更新日志
### 2019-05-14
- 更新组件：antd 组件由`^3.11.6`更新至`^3.16.1`,可以享用更丰富的组件和样式

### 2019-05-09
- 增加页面：丰富了首页常用菜单，使打开页面更加快捷

### 2019-04-29
- 修复功能：解决了 `个人中心`和`个人设置`页面展示不全的问题
- 增加功能：拾色器组件

### 2019-04-23
- 增加功能：增加了左侧点击出发的函数，及ç`onHandlePage ={this.onHandlePage}`
- 增加文档：主要解释了`Ant Tabs`的原理及功能

### 2019-04-18
- 增加功能：AntTableFinder-多功能Table 深度封装 ant Table 表格

### 2019-04-10
- 增加功能：Tabs-支持多标签功能
- 增加功能：支持-关闭当前标签页、关闭其他标签页、关闭全部标签页
- 增加功能：拖拽组件
- 增加功能：富文本编译器
- 增加功能：支持-是否 隐藏 `Ant-Tabs` 功能

## 反馈

如果你觉得有用，对你有些帮助，欢迎给个[Star](https://github.com/kuhami/react-ant)😊，如果你还为明白及文中有错误，请提交[Issues](https://github.com/kuhami/react-ant/issues)😊