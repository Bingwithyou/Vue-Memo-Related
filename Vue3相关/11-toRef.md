### toRef

 - 作用：创建一个ref 对象，其 value 值指向另一个对象中的某个属性。
 - 语法：`const name = toRef(person,'name')`
 - 应用：要将响应式对象中的某个属性单独提供给外部使用时
 - 扩展：`toRefs`与`toRef`功能一致，但可以批量创建多个 ref 对象
 - 语法：`toRefs(person)`
### 使用
```js
// 需要引入 toRef
import {reactive, toRef, toRefs} from 'vue'
export default {
  setup(){
	let person = reactive({
	  name:'Alto',
	  age:22,
	  job:{
		j1:{
		  salary:20
		}
	  }
    })
  }
}
```
> 直接 return 对象身上的属性会丢失响应式
```js
// 错误
return {
  name: person.name,
  age: person.age,
  salary: person.job.j1.salary
}
```
> 使用 toRef
```js
// 可以直接在模板中使用 {{name}}, {{age}} 而不需要加上前缀：person.name 
return {
  name: toRef(perosn, 'name'),
  age: toRef(perosn, 'age'),
  salary: toRef(perosn.job.j1, 'salary'),
}
```
> 使用 toRefs 批量处理
```js
return {
  person,
  // 使用 ES6 语法 ... 展开参数，省略了 person 前缀
  // 但 salary 仍需要使用：job.j1.salary
  ...toRefs(person)
}
```
