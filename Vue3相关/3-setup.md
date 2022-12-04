### 1. setup为 Vue3.0 新的配置项，值为一个函数
setup函数的两种返回值：
 - 若返回一个对象，则对象中的属性、方法，在模板中均可以直接使用。
 - （了解）若返回一个渲染函数，则可以自定义渲染内容。
```js
import {h} from 'vue'
export default {
	name:'App',
	setup(){
		// 数据（注意此方法定义数据丢失了响应式，参考ref章节内容）
		let name = "test"
		// 方法（前缀必须要写 function 不然报错）
		function helloWorld(){
			// 模板字符串写法：`${}`
			console.log(`Hello World ${name}`)
		}
		// 需要配置返回值
		return {
			name,
			helloWorld,
		}
		// 返回渲染函数（需要引入 h 使用）
		return ()=> h('h1','Hello World')
		// 页面会显示 h1 格式的 ‘Hello World’，忽略其他元素
	}
}
```
### 2. 注意事项
 - 尽量不要与 Vue2 配置混用
 
 - Vue2 配置（data, methods, computed...）可以访问到 setup 中的属性、方法。

 - setup 中不能访问到 Vue2 配置（data, methods, computed...）

 - 如果有重名，以 setup 优先

 - setup 不能是一个 async 函数，因为返回值不再是 return 的对象，而是 promise， 模板看不到 return 对象中的属性。
