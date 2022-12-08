### shallowReactive

 - 只处理对象最外层属性的响应式（浅响应式）。
 - 如果有一个对象数据，结构比较深，但只是外出属性变化，可以使用此属性
```js
import {shallowReactive} from 'vue'
export default {
  setup(){
	let person = shallowreactive({
	  name:'Alto',
	  age:22,
	  job:{
		j1:{
		  salary:20
		}
	  }
    })
  }
  // 网页中只能监测到 name, age 数据变动，salary数据变动无法监测到
  return {
	person
  }
}
```
### shallowRef
 - 只处理基本数据类型的响应式，不进行对象的响应式处理。
 - 如果一个对象数据，后续功能不会修改对象中的属性，而是生成新的对象来替换，可以使用这个方法。
```js
import {shallowRef} from 'vue'
export default {
  setup(){
    // x 是响应式的，但无法监测到 y 数据变动
	let x = shallowRef({
      y:0
	})
  }
}
```
> ref 处理对象类型数据时，是通过 reactive 处理的，shallowRef 不再用 Proxy 处理而是原始的 Object
