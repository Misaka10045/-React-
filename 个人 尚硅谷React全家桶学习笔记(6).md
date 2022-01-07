# 个人 尚硅谷React全家桶学习笔记 （六）

## 6.jsx小练习

	const data=['Angular','React','Vue']
		
		const VDOM=(
			<div>
				<h1>前端js框架列表</h1>
				<ul>{
					data.map((item,index)=>{
						return<li key={index}>{item}</li>
					})
				}</ul>
			</div>
		)
		
		ReactDOM.render(VDOM,document.getElementById('test'))

#### 一定注意区分:【js语句(代码)】与【js表达式】

​	**1.表达式:一个表达式会产生一个值，可以放在任何一个需要值的地方**

​			下面这些都是表达式:

​				1)   a

​				2)   a+b

​				3)   demo(1)

​				4)   arr.map()

​				5)   function test() {}

**2.语句(代码):**

​			下面这些都是语句(代码):

​				1)   if(){}

​				2)   for(){}

​				3)   switch(){case:xxxx}





## 7.组件与模块

#### 模块

 1)理解: 向外提供特定功能的js程序，一般就是一个js文件

 2)为什么要拆成模块: 随着业务逻辑增加，代码越来越繁多复杂。

 3)作用: 复用js，简化js的编写，提高js运行效率

#### 组件

 1)理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image 等)

 2)为什么：一个界面的功能更复杂

 3)作用：复用编码，简化项目编码，提高运行效率

#### 模块化

当应用的js都以模块来编写的，这个应用就是一个模块化的应用

#### 组件化

当应用是以多组件的方式实现，这个应用就是一个组件化的应用

