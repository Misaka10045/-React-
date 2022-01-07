# 个人 尚硅谷React全家桶学习笔记（八）

## 10.类相关知识复习

> 1.类中的构造器不是必须写的，要对实例进行一些初始化的操作，如添加指定属性时才写。
>
> 2.如果A类继承了B类，且A类中卸了构造器，那么A类构造器中的super是必须要调用的。
>
> 3.类中所定义的方法，都是放在了类的原型对象上，供实例去使用。





## 11.类式组件

	class Demo extends React.Component{
			render(){
				return <h2>我是用类式定义的组件(适用于【复杂组件】的定义)</h2>
			}
		}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意点

必须继承React中的 Component



#### React的操作

1.React解析组件标签，找到了Demo组件。

2.发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法，将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。