# 个人 尚硅谷React全家桶学习笔记(十三)

## 37.引出生命周期

```
class Life extends React.Component{
		state={
			opacity:1
		}
		death=()=>{
			//卸载组件
			ReactDOM.unmountComponentAtNode(document.getElementById('test'))
		}
		//组件挂载完毕后调用 并且只调用一次
		componentDidMount(){
			this.timer=setInterval(() => {
				//获取原状态
				let{opacity}=this.state
				//减小0.1
				opacity-=0.1
				if(opacity<=0) opacity=1
				//设置新的透明度
				this.setState({opacity})
			},200);
		}
		//组件将要卸载时调用一次
		componentWillUnmount(){
				//清除定时器
				clearInterval(this.timer)
		}
		

	render(){
	
		return(

		<div>
			<h2 style={{opacity:this.state.opacity}}>React学不会怎么办？</h2>
			<button onClick={this.death}>不活了</button>
		</div>

		)
	}
}
ReactDOM.render(<Life/>,document.getElementById('test'))
```

**在合适的时机 调用函数**

**例如  componentDidMount() 是在函数挂载完毕后调用且只调用一次的函数**

**componentWillUnmount() 是在组件卸载前调用且只调用一次的函数**



**1.组件从创建到死亡会经历一些特定的阶段。**

**2.React组件中包含一系列勾子函数(生命周期回调函数)，会在特定时刻调用。**

**3.我们在定义组件时，会在特定的生命周期回调函数中做特定的工作。**





## 38.生命周期（旧）_组件挂载流程

	class Count extends React.Component{
		//构造器
		constructor(props){
			console.log('Count-constructor');
			super(props)
		}
		//组件将要挂载的钩子
		componentWillMount(){
			console.log('Count-componentWillMount');
		}
		//组件挂载完毕的钩子
		componentDidMount(){
			console.log('Count-componentDidMount');
		}
		
		render(){
			console.log('Count-render');
			return(
			<div>
				<h2>挂载流程</h2>
			</div>
			)
		}
	}
	ReactDOM.render(<Count/>,document.getElementById('test'))



**控制台会依次分别输出**

**Count-constructor**  

**Count-componentWillMount**  

**Count-render** 

**Count-componentDidMount**

**这也是组件挂载时的流程**





## 39.生命周期（旧）_setstate流程

	class Count extends React.Component{
		//构造器
		constructor(props){
			console.log('Count-constructor');
			super(props)
			//初始化状态
			this.state={count:0}
		}
		add=()=>{
			//获取原状态
			const {count}=this.state
			//更新状态
			this.setState({count:count+1})
		}
		death=()=>{
			ReactDOM.unmountComponentAtNode(document.getElementById('test'))
		}
		
		//组件将要挂载的钩子
		componentWillMount(){
			console.log('Count-componentWillMount');
		}
		//组件挂载完毕的钩子
		componentDidMount(){
			console.log('Count-componentDidMount');
		}
		//组件将要卸载的钩子
		componentWillUnmount(){
			console.log('Count-componentWillUnmount');
		}
		//控制组件更新的阀门
		shouldComponentUpdate(){
			console.log('Count-shouldComponentUpdate')
			return true
		}
		//组件将要更新的钩子
		componentWillUpdate(){
			console.log('Count-componentWillUpdate');
		}
		//组件更新完毕的钩子
		componentDidUpdate(){
			console.log('Count-componentDidUpdate')
		}
		render(){
			console.log('Count-render');
			const {count}=this.state
			return(
			<div>
				<h2>当前求和为：{count}</h2>
				<button onClick={this.add}>点我+1</button>
				<button onClick={this.death}>卸载</button>
			</div>
			)
		}
	}
	ReactDOM.render(<Count/>,document.getElementById('test'))

**每次点按钮+1时 控制台都会依次输出**

**Count-shouldComponentUpdate  （控制组件更新的阀门）**

**Count-componentWillUpdate	（组件将要更新的钩子）**

**Count-render**	

**Count-componentDidUpdate	（组件更新完毕的钩子）**



**点击按钮卸载时 控制台将会输出**

**Count-componentWillUnmount  （组件将要卸载的钩子）**



**shouldComponentUpdate为控制组件更新的阀门**

**如果返回值为flase 那么将会阻止组件更新**

**如果为true则更新**

**如果不写的话 react会自动返回true** 





## 40.生命周期（旧）_forceUpdate流程

**不更改任何状态 并且跳过阀门强制更新**

	class Count extends React.Component{
		//构造器
		constructor(props){
			console.log('Count-constructor');
			super(props)
			//初始化状态
			this.state={count:0}
		}
		add=()=>{
			//获取原状态
			const {count}=this.state
			//更新状态
			this.setState({count:count+1})
		}
		death=()=>{
			ReactDOM.unmountComponentAtNode(document.getElementById('test'))
		}
		force=()=>{
			this.forceUpdate()
		}
		
		//组件将要挂载的钩子
		componentWillMount(){
			console.log('Count-componentWillMount');
		}
		//组件挂载完毕的钩子
		componentDidMount(){
			console.log('Count-componentDidMount');
		}
		//组件将要卸载的钩子
		componentWillUnmount(){
			console.log('Count-componentWillUnmount');
		}
		//控制组件更新的阀门
		shouldComponentUpdate(){
			console.log('Count-shouldComponentUpdate')
			return true
		}
		//组件将要更新的钩子
		componentWillUpdate(){
			console.log('Count-componentWillUpdate');
		}
		//组件更新完毕的钩子
		componentDidUpdate(){
			console.log('Count-componentDidUpdate')
		}
		render(){
			console.log('Count-render');
			const {count}=this.state
			return(
			<div>
				<h2>当前求和为：{count}</h2>
				<button onClick={this.add}>点我+1</button>
				<button onClick={this.death}>卸载</button>
				<button onClick={this.force}>强制更新</button>
			</div>
			)
		}
	}
	ReactDOM.render(<Count/>,document.getElementById('test'))

**点击强制更新按钮时 控制台将会只输出**

**Count-componentWillUpdate**

**Count-render**

**Count-componentDidUpdate**

**跳过了shouldComponentUpdate**





## 41.生命周期（旧）_父组件render流程

	class A extends React.Component{
		//初始化状态
		state={carName:'奔驰'}
		changeCar=()=>{
			this.setState({carName:'奥拓'})
		}
		
		render(){
			return(
			<div>
				<div>A组件</div>
				<button onClick={this.changeCar}>换车</button>
				<B carName={this.state.carName}/>
			</div>
			)
		}
	}
	
	class B extends React.Component{
		//组件将要接收新的props的钩子
		componentWillReceiveProps(){
			console.log('B-componentWillReceiveProps')
		}
		render(){
			return(
				<div>B组件,接收到的车是:{this.props.carName}</div>
			)
		}
	}
	
	ReactDOM.render(<A/>,document.getElementById('test'))

**这段代码中 A是B的父组件**

**而componentWillReceiveProps则是组件将要接收 新 的props的钩子**

**也就是说 第一次接收props时并不会触发componentWillReceiveProps**

**而是在之后接收新的props时才会触发**

**所以控制台只有在点击 换车 按钮时才会输出**

**B-componentWillReceiveProps**





## 42.总结生命周期（旧）总结

​	**1.初始化阶段： 由ReactDOM.render()触发---初次渲染**

1. constructor()

2. componentWillMount()

3. render()

4. componentDidMount()    **常用：一般在这做一些初始化的事。**

​	**2.更新阶段：由组件内部this.setSate()或父组件重新render触发**

1. shouldComponentUpdate()

2. componentWillUpdate()

3. render()   **必要**

4. componentDidUpdate()

​	**3.卸载组件： 由ReactDOM.unmountComponentAtNode()触发**

1. componentWillUnmount()  **常用：一般做一些收尾的事**