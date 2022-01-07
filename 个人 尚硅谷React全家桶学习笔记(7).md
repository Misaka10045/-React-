# 个人 尚硅谷React全家桶学习笔记 （七）

## 8.开发者工具的安装

省略.....



## 9.函数式组件

		function Demo(){
			return <h2>我是用函数式定义的组件(适用于【简单组件】的定义)</h2>
		}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意点

1.函数名首字母必须大写  （Demo）

2.函数必须有返回值

3.渲染时必须写组件标签 并且闭合



#### React的操作

1.React解析组件标签，找到了Demo组件。

2.发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为虚拟DOM，随后呈现在页面中。
