### readonly
> 数据设为只读，无法修改数据
```js
import {reactive, readonly, shallowReadonly} from 'vue'
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
  // 启动只读，当修改 person 里的对象数据时，会提示不能修改
  person = readonly(person)
  return {
	person
  }
}
```
### shallowReadonly
> 浅层只读，对象深层数据仍然可以更改
```js
// 更改 person 里的 salary 数据可以生效
person = shallowReadonly(person)
```
