# 个人 尚硅谷React全家桶学习笔记 （二）

## 2.React案例

#### 引入文件

**react.js  React的核心库**

**react-dom.js  提供操作DOM的react扩展库**

**babel.min.js 解析JSX语法 代码转为JS代码的库**

>  *核心库必须在扩展库之前引入*
>
> *自己写的脚本类型为*   `type="text/babel"` 

#### 创建虚拟DOM

*const DOM名=内容* 

`const VDOM=<h1 id="title">Hello,React</h1>`   *<!--内容无需写引号-->*

#### 渲染虚拟DOM到页面

`ReactDOM.render(DOM名,使用原生JS选择器 选择容器)`   <!--*React唯一直接操作DOM的地方*-->