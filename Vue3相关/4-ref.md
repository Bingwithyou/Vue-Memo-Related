### 1. 与 Vue2 中不同的是，ref 不再是给元素打标识用
#### Vue2 中的 ref 用法：
```js
// 定义在普通标签上，相当于 getElementById 用法
<div ref="deom"></div>

// 组件间传递数据
<div id="app">
	<mainPage ref="mainPage"></mainPage>
</div>
// 调用
new Vue({
    el:'#app',
    mounted:function(){
		console.log(this.$refs.mainPage)
    }
})
```
#### Vue3 中的用法：
>在 setup 中定义数据时，直接定义数据会丢失响应式，数据更改时不会被检测到，应该使用ref。
```js
// 需要引入 ref 
import {ref} from 'vue'
setup(){
	// 此时数据就会有 getter 和 setter
	let name = ref('Alto')
	let age = ref(22)
	
	return {
		name,
		age
	}
}
```
> 在模板中使用时 {{ name }} 不需要添加 ".value"，会自动读取值
### 2. 处理对象类型
当 ref 定义的是一个对象类型数据时，如何在方法中调用到对象里的值？
```js
setup(){
	let person = ref({
		name = 'Alot'
		age = 22
	})
	// 在 .value 后边选择对象里的值
	function changeInfo(){
		person.value.name = 'Ezio'
		person.value.age = 18
	}
}
```
> 利用 ref 读取对象内部数据用到了 Vue3 中的一个新函数 —— `reactive` 函数，将其变为 `proxy` 实例对象
