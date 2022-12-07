 ### Vue2中的 watch 监听写法：
```js
export default {
  watch:{
    sum(newValue, oldValue){
      // 接收两个参数，新数据和原来的旧数据
      console.log(newValue, oldValue)
    }

    // 第二种对象写法，功能更多
    sum:{
      // 立即执行一次
      immediate: true,
      // 深度监视
      deep: true,
      handler(newValue, oldValue){
		console.log(newValue, oldValue)
	  }
    }
  }
}
```
### Vue3中的 watch 监听写法：
```js
// 先引入 watch
import {ref, reactive, watch} from 'vue'
export default {
  setup(){
    let sum = ref(0)
    let msg = ref("Hello")
    let person = reactive({
	  name: 'Alto',
	  age: 18,
	  job:{
        j1:{
		  salary: 20
		}
      }
	})

    return {
      sum,
      msg
	}
  }
```
>情况一：监视一个响应式数据，可以在第三个参数位置配置 `immediate `
```js
watch(sum, (newValue, oldValue) => {
  console.log('sum Changed', newValue, oldValue)
}, {immediate: true})
```
>情况二：监视多个响应式数据
```js
watch([sum, msg], (newValue, oldValue) => {
      console.log('sum or msg changed:', newValue, oldValue)
}, {immediate: true})
// 查看控制台会发现，多个数据会出现在一个数组里：
// sum or msg changed: [1,"Hello"] → [0, "Hello"]
// 即左边数组代表新数据，右边为旧数据
```
>情况三：监视一个响应式对象身上 全部 数据
```js
watch(person, (newValue, oldValue) => {
  console.log('person changed,' newValue, oldValue)
},{deep:true})
// 测试后发现 watch 无法正确获取到 reactive 的 oldValue 值
// 无法手动关闭 reactive 的深度监视
```
>情况四：监视一个响应式对象身上 某一个 数据
```js
// 直接 person.name 无法正常运行，需要通过一个匿名函数返回要监视的值
watch(() => person.name, (newValue, oldValue) => {
  console.log("person's name changed,"newValue, oldValue)
})
// 无法监视到 oldValue 值变化
```
>情况五：监视一个响应式对象身上 多个 数据
```js
// 与情况四类似，通过 数组+匿名函数 形式返回要监视的值
watch([() => person.name, () => person.age], (newValue, oldValue) => {
  console.log("person's name and age changed,", newValue, oldValue)
})
// 无法监视到 oldValue 值变化
```
>特殊情况：监视一个响应式对象身上的 对象 里的数据
```js
// 因为 job 是对象里的 对象形式 数据，需要声明开启 deep:true 才能监测到数据变动
watch(() => person.job, (newValue, oldValue) => {
  console.log("person's job changed,", newValue, oldValue)
}, {deep:true})
```
### 总结
当 watch 的是一个 reactive 响应式 对象 数据时：
 - 无法正确获取到 oldValue 值
 - 强制开启了深度监视（deep 配置无效）
 - 特殊情况里，因为监视的是 reative 响应式里的 "对象" 属性，此时 deep 配置有效。
 - ❗❗不同于 person.name, 此时的 name 属于字符串型数据，可以获取到 oldValue 值。
