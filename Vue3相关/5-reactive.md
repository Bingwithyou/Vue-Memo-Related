### 1. 作用：
>定义一个 对象类型 的响应式数据（基本类型不能用reactive而是ref）

#### 语法：
```js
setup(){
	// 使用 reactive 包裹对象，返回一个代理对象（Proxy 的实例对象）
	let person = reactive({
		name = "Alto"
		age = 22
		hobby:{
			hb1:"typing code"
		}
	})
	return person
}
// 调用时，可以直接 对象名.值 获取数据，省略了 .value
function changeInfo(){
	person.name = "Conna"
	person.age = 18
	// 可以自动监测深层数据变动
	person.hobby.hb1 = "gaming"
}
```
>内部基于 ES6的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。
