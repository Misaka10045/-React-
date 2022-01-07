# 个人 尚硅谷React全家桶学习笔记 （三）

## 3.虚拟DOM的两种创建方式

#### **使用js创建虚拟DOM** 

*无需引入babel.min.js*

*脚本类型为*   `type="text/javascript"` 

**创建虚拟DOM**

*const VDOM=React.createElement(标签名，标签属性，标签内容)*

`const VDOM=React.createElement('h1',{id:"title"},'Hello,React')`

#### 标签内嵌套标签

**JSX写法**

`const VDOM=(<h1 id="title"><span>Hello,React</span></h1>）`

**JS写法**

`const VDOM=React.createElement('h1',{id:'title'},React.createElement('span',{},'Hello,React'))` 