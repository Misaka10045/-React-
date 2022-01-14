# 个人 尚硅谷React全家桶学习笔记(十一)

## 27.字符串形式的ref

**作用类似ID**

	class Demo extends React.Component{
		showData=()=>{
			const{input1}=this.refs
			alert(input1.value)
		}
		render(){
			return(
			<div>
			<input ref='input1' type='text' placeholder='点击按钮'/>
			<button onClick={this.showData}>点我提示</button>
			</div>
			)
		}
	}
	
	ReactDOM.render(<Demo/>,document.getElementById('test1'))

**注意**  给标签添加时为ref  使用时为refs





## 28.回调形式的ref

**注意** 字符串形式的ref可能后续版本会废弃掉，因为有缺陷 效率低。

	class Demo extends React.Component{
		showData=()=>{
			const{input1}=this
			alert(input1.value)
		}
		render(){
			return(
			<div>
			<input ref={c => this.input1=c} type='text' placeholder='点击按钮'/>
			<button onClick={this.showData}>点我提示</button>
			</div>
			)
		}
	}
	ReactDOM.render(<Demo/>,document.getElementById('test1'))

ref中的箭头函数 react会自动帮你调用

同时是箭头函数 所以里面的this为实例对象。





## 29.回调ref中调用次数的问题

如果ref回调函数是以内联函数的方式定义的，在更新组件过程中它会执行两次，第一次传入参数null，第二次才传入参数DOM元素。

解决方法如下 使定义成class的绑定函数方法

	class Demo extends React.Component{
		showData=()=>{
			const{input1}=this
			alert(input1.value)
		}
		saveInput=(c)=>{
			this.input1=c;
			
		}
		render(){
			return(
			<div>
			<input ref={this.saveInput} type='text' placeholder='点击按钮'/>
			<button onClick={this.showData}>点我提示</button>
			</div>
			)
		}
	}
	
	ReactDOM.render(<Demo/>,document.getElementById('test1'))

**注意** 两者没有作用上的差别 都能使用。





## 30.createRef的使用

	class Demo extends React.Component{
		myRef=React.createRef()
		showData=()=>{
			alert(this.myRef.current.value)
		}
		render(){
			return(
			<div>
			<input ref={this.myRef} type='text' placeholder='点击按钮'/>
			<button onClick={this.showData}>点我提示</button>
			</div>
			)
		}
	}
	
	ReactDOM.render(<Demo/>,document.getElementById('test1'))

React.createRef调用后可以返回一个容器，该容器可以存储被ref标识的节点，

但一个容器只能装一个

**注意** this.myRef.current.value 中的current不能少





## 31.总结ref

1.组件内的标签可以定义ref属性来标识自己

2.尽量不用字符串形式的ref

3.createRef最为复杂但也是官方最推荐的