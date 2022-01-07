# 个人 尚硅谷React全家桶学习笔记 （九）

## 12.对state的理解

> 1.有状态的为复杂组件，无状态的为简单组件
>
>  2.state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)
>
>  3.组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

## 13.初始化state

			class Demo extends React.Component{
				constructor(props){
					super(props)
					this.state={isHot:true}
				}
				render(){
					const{isHot}=this.state
					return <h1>今天天气很{isHot ? '炎热':'凉爽'}</h1>
				}
			}
		
		ReactDOM.render(<Demo/>,document.getElementById('test'))

## 14.React中的事件绑定

	class Demo extends React.Component{
			constructor(props){
				super(props)
				this.state={isHot:true}
			}
			render(){
				const{isHot}=this.state
				return <h1 onClick={demo}>今天天气很{isHot ? '炎热':'凉爽'}</h1>
			}
		}
	function demo(){
		console.log('点击')
	}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意

> React中的事件为驼峰命名  原生onclick应写为onClick
>
> 不应该用 引号写函数 而是用{}
>
> 直接写函数名 无需加()调用 react会帮你调用





## 15.类中方法中的this

			class Demo extends React.Component{
				constructor(props){
					super(props)
					this.state={isHot:true}
				}
				render(){
					const{isHot}=this.state
					return <h1 onClick={this.demo}>今天天气很{isHot ? '炎热':'凉爽'}</h1>
				}
				demo(){
					console.log(this)
				}
			}
		
		ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意

由于demo是作为onClick的回调，所以不是实例调用，是直接调用。

类中的方法默认开启了局部的严格模式，所以

demo中的this为undefined





## 16.解决类中的this指向问题

	class Demo extends React.Component{
			constructor(props){
				super(props)
				this.state={isHot:true}
				this.demo=this.demo.bind(this)
			}
			render(){
				const{isHot}=this.state
				return <h1 onClick={this.demo}>今天天气很{isHot ? '炎热':'凉爽'}</h1>
			}
			demo(){
				console.log(this)
			}
		}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

**this.demo1=this.demo2.bind(this)**

> 这行代码意思为在实例中创建一个新函数 demo1  它的内容为原型中的demo2函数
>
> 这样就能解决this的指向问题 因为是用实例调用的函数





## 17.setState的使用

		class Demo extends React.Component{
			constructor(props){
				super(props)
				this.state={isHot:true}
				this.demo=this.demo.bind(this)
			}
			render(){
				const{isHot}=this.state
				return <h1 onClick={this.demo}>今天天气很{isHot ? '炎热':'凉爽'}</h1>
			}
			demo(){
				const isHot=this.state.isHot
				this.setState({isHot:!isHot})
			}
		}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意

> state必须通过setState进行更新，并且更新是合并不是替换。





## 18.state的简写方式

		class Demo extends React.Component{
			state={isHot:true}
			render(){
				const{isHot}=this.state
				return <h1 onClick={this.demo}>今天天气很{isHot ? '炎热':'凉爽'}</h1>
			}
			demo=()=>{
				const isHot=this.state.isHot
				this.setState({isHot:!isHot})
			}
		}
	
	ReactDOM.render(<Demo/>,document.getElementById('test'))

#### 注意

> state直接使用赋值语句也能初始化
>
> 自定义函数需要同时使用赋值语句和箭头函数 赋值语句用于类函数  箭头函数用于解决this的指向问题





## 19.总结state

> 1.state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)
>
> 2.组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)
>
> 3.组件中render方法中的this为组件实例对象
>
> 4.组件自定义的方法中this为undefined，如何解决？
>
> ​	1)强制绑定this: 通过函数对象的bind()
>
> ​	2)箭头函数
>
> 5.状态数据，不能直接修改或更新