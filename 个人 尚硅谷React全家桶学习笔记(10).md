# 个人 尚硅谷React全家桶学习笔记 （十）

## 20.props的基本使用

		class Person extends React.Component{
			render(){
				const{name,age,sex}=this.props
			 return (
				<ul>
					<li>姓名:{name}</li>
					<li>性别:{sex}</li>
					<li>年龄:{age}</li>
				</ul>
			)
		 }
		}
	ReactDOM.render(<Person name="Jerry" age="19" sex="男"/>,document.getElementById('test'))

在渲染时写在标签内的 key value组合会存在实例的props中
可以通过this调用





## 21.批量传递props

	class Person extends React.Component{
			render(){
				const{name,age,sex}=this.props
			 return (
				<ul>
					<li>姓名:{name}</li>
					<li>性别:{sex}</li>
					<li>年龄:{age}</li>
				</ul>
			)
		 }
		}
		
		const p ={name:'老刘',age:18,sex:'女'}
	ReactDOM.render(<Person {...p}/>,document.getElementById('test'))

使用{...p}来批量传递props



#### 重点复习展开运算符

	let arr1=[1,3,5,7,9]
	let arr2=[2,4,6,8,10]
	console.log(...arr1);

控制台会分开输出

1 3 5 7 9

	let arr1=[1,3,5,7,9]
	let arr2=[2,4,6,8,10]
	let arr3=[...arr1,...arr2]
	console.log(...arr3);

控制台会分开输出1 3 5 7 9 2 4 6 8 10  相当于把arr1和arr2合并在一起



```
let person={name:'tom',age:18}
let person2={...person}
console.log(person2);
```

**注意** ...不能直接展开对象，但可以用{...}来复制对象

**但是** babel加上react 就可以用...来展开一个对象

所以 

```
ReactDOM.render(<Person {...p}/>,document.getElementById('test'))
```

内的 {...p} 并不是复制对象  {}内的是JS代码  也就是展开对象 不过不能随意使用，只能用于标签的使用。

```
let person2={...person,name:'jack',addres:'地球'}
```

后面的 name:'jack',addres:'地球' 可以用来修改或者添加属性





## 22.对props进行限制

**注意** 前置需要引入 prop-types.js文件

	Person.propTypes={
				name:PropTypes.string.isRequired, //限制name为必传，且为字符串
				sex:PropTypes.string,//限制sex为字符串
				age:PropTypes.number,//限制age为数字
			}

**注意** propTypes和PropTypes的差别， string和number需小写。

**注意**  如果需要限制为函数 则需要写成 PropTypes.func  而不是function 。

```
Person.defaultProps={
			sex:'未知',//sex默认值为'未知'
		}
```

 如果sex没写，那么页面会呈现出  ‘未知’。





## 23.props的简写方式

props是只读的不能通过

```
this.props.name='jack'
```

这种方式修改





通过static 可以给类自身添加属性 而不是给实例对象添加属性

所以可以用static 来把上面的限制写进类本身里面

	class Person extends React.Component{
			static propTypes={
				name:PropTypes.string.isRequired, //限制name为必传，且为字符串
				sex:PropTypes.string,//限制sex为字符串
				age:PropTypes.number,//限制age为数字
			}
			static defaultProps={
				sex:'未知'
			}
			render(){
				const{name,age,sex}=this.props
			 return (
				<ul>
					<li>姓名:{name}</li>
					<li>性别:{sex}</li>
					<li>年龄:{age}</li>
				</ul>
			)
		 }
		}





## 24.类式组件中的构造器与props

构造器是否接受props，是否传递给super，取决于：是否希望在构造器中通过this访问props

类中的构造器可以省略

**注意** 极少使用 能省略就省略





## 25.函数式组件使用props

	function Person(props){
		const {name,age,sex}=props
		return (
			<ul>
				<li>姓名:{name}</li>
				<li>性别:{sex}</li>
				<li>年龄:{age}</li>
			</ul>
		)
	}
	ReactDOM.render(<Person name='jerry' age={19} sex='男'/>,document.getElementById('test1'))

函数式组件能够通过接受参数的方式 使用props属性

但props的限制就不能使用static方式来写了 必须写在外侧。



## 26.总结props

1. 每个组件对象都会有props(properties的简写)属性

2. 组件标签的所有属性都保存在props中

   3.通过标签属性从组件外向组件内传递变化的数据

   4.注意: 组件内部不要修改props数据