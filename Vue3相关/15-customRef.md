### 作用：创建一个自定义的 ref ，并对其依赖项跟踪和更新触发进行显式控制。
> 实现防抖效果：
```js
<template>
  <input type="text" v-model="keyword">
  <h3>{{keyword}}</h3>
  </input>
</template>

<script>
  import {ref, customRef} from 'vue'
  export default {
	name:'test',
	setup(){
	  // Vue 内置的 ref
	  // let keyword = ref('hello')

	  // 自定义一个 myRef
	  function myRef(value, delay){
		let timer
		// 通过 customRef 实现，注意有两个 return 
		return customRef((track, trigger) => {
		  return {
			get(){
			  // 告诉 vue 这个 value 值是需要被 “追踪”的
			  track
			  return value
			},
			set(newValue){
			  // 先停掉之前的计时器，实现防抖（不然会开启多个计时器，显示效果会出错）
			  clearTimeout(timer)
			  tier = setTimeout(() => {
				value = newValue
				// 告诉 Vue 去更新界面
				trigger()
			  },delay)
			}
		  }
		})
	  }
	  let keyword = myRef('hello', 500)
	}
  }
</script>
```
