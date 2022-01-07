# 个人 尚硅谷React全家桶学习笔记 （四）

## 4.虚拟DOM与真实DOM

####   关于虚拟DOM

> 1. 虚拟DOM本质是Object数据类型对象（一般对象）。
> 2. 虚拟DOM属性相比真实DOM少很多,因为虚拟DOM是React内部在用，无需真实DOM那么多属性。
> 3. 虚拟DOM最终会被React转化为真实DOM，呈现在页面上 