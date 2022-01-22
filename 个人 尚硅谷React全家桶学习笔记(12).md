# 个人 尚硅谷React全家桶学习笔记(十二)

## 32.react中的事件处理

**1.通过onXxx属性指定事件 注意大小写（onClick）** 

​	**a.React使用的是自定义事件，而不是原生DOM事件（为了更好的兼容性)**

​	**b.React中的时间是通过事件委托方式处理的（委托给组件最外层的元素  因为高效）**

**2.通过event.target得到发生时间的DOM元素对象（不要过度使用ref  发生事件的元素是要操作的元素就可以省略ref）**





## 33.非受控组件

```
class Login extends React.Component{
		handleSubmit=(event)=>{
			event.preventDefault()
			const {username,password}=this
			alert('你输入的用户名是：${username.value},你输入的密码是：${password.value}')
		}
		render(){
			return(
			<form onSubmit={this.handleSubmit}>
			用户名:<input ref={c=>this.username=c} type="text" name="username"/>
			密码:<input ref={c=>this.password=c} type="password" name="password"/>
			<button>登录</button>
			</form>
			)
		}
	}
	ReactDOM.render(<Login/>,document.getElementById('test'))
```

**现用现取**

## 34.受控组件

```
class Login extends React.Component{
		

​	state={
​		username:'',
​		password:''
​	}
​	saveUsername=(event)=>{
​		this.setState({username:event.target.value})
​	}
​	savePassword=(event)=>{
​		this.setState({password:event.target.value})
​	}
​	handleSubmit=(event)=>{
​		event.preventDefault()
​		const{username,password}=this.state
​		alert('你输入的用户名是：${username},你输入的密码是：${password}')
​	}
​	render(){
​		return(

		<form onSubmit={this.handleSubmit}>
		用户名:<input onChange={this.saveUsername} type="text" name="username"/>
		 密码：<input onChange={this.savePassword} type="password" name="password"/>
		<button>登录</button>
		</form>

​		)
​	}
}
ReactDOM.render(<Login/>,document.getElementById('test'))
```

**页面中所有输入类的DOM随着你的输入把东西放在state中，要用时在取出来 就是受控组件**

**相比非受控 还是建议使用受控 因为相比非受控 受控省略了ref**





## 35.高阶函数_函数柯里化

**高阶函数：如果一个函数符合以下2个规范中的任何一个，那么该函数就是高阶函数。**

​			1.若A函数，接受的参数是一个函数，那么A就可以称之为高阶函数。

​			2.若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。

**函数的柯里化：通过函数调用继续返回函数的方式，实现多次接受参数最后统一处理的函数编码形式**

```
普通函数:
	function sum(a,b,c){
	return a+b+c
	}

柯里化: 
function sum(a){
		return(b)=>{
			return(c)=>{
				return a+b+c
			}
		}
	}
```





## 36.不用柯里化的写法

**老师较真 省略...**