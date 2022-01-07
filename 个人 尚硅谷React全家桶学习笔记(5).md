# 个人 尚硅谷React全家桶学习笔记 （五）

## 5.JSX语法规则

#### JSX

> 1. 全称:  JavaScript XML
>
> 2. react定义的一种类似于XML的JS扩展语法: JS + XML本质是	React.createElement(component,props,...children)方法的语法糖
>
> 3. 作用:用于简化创建虚拟DOM
>
>    1)写法: 
>
> ```
> var ele=<h1>Hello JSX!</h1>
> ```
>
> ​	2)注意1::它不是字符串，也不是HTML/XML	标签
>
> ​	3)注意2:它最终产生的就是一个JS对象
>
> 
>
> 4. 标签名任意:HTML标签或其它标签
>
> 5. 标签属性任意:HTML标签属性和其它

#### 基本语法规则:

1.定义虚拟DOM时，无需写引号。

2.标签中混入JS表达式时 要用{}。

```
const myID='Atguigu'
const myData='Hello,React'
const VDOM=(
<h2 id={myId}>
<span>{MyData}</span> 
</h2>
)
```

3.样式的类名指定不要用class，而是用className。

4.内联样式，要用 style={{key:value}}的形式写。

5.只有一个根标签

6.标签必须闭合 

7.标签首字母 

​	1）.若小写字母开头，则将该标签转为html中同	名元素，若无该标签对应的同名元素，则报错。

​	2)   .若大写字母开头，react就去渲染对应的组    	件，若组件未定义，则报错。