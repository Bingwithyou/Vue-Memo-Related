## mapState方法
如果`actions`不需要相关逻辑，也可以直接跳过`dispatch`来直接调用`commit`，这个时候可能会经常调用`this.$store.state.xxx`
```js
// 举例，繁琐的写法
sum(){
  return this.$store.state.sum
},
school(){
  return this.$store.state.school
},
```
这时可以使用`mapState`来自动生成调用，首先要在 **组件(VC)** 中引入`mapState`：

```js
import {mapState} from 'vuex'

// 借助mapState生成计算属性，从state中读取数据，当函数名与数据名一致时，可以写成数组形式：...mapState(['a', 'b', 'c'])

computed: {
    // 等效上边的举例
    ...mapState({sum, school}),
}
```
'...' 作用是将对象脱掉({ })展开来存放。例：xuexiao: 'school'代表如下代码：
```js
xuexiao(){
    return this.$store.state.school
}
```
## mapGetters方法
使用方法基本与 state 相似
```js
computer: {
  // 举例
  getSum(){
    return this.$store.getters.getSum
  }
  // 等效于
  ...mapGetters(["getSum"])
}
```
## mapActions，mapMutations方法与上边基本相同
```js
methods:{
  ...mapActions({}),
  ...mapMutations({})
}
```
## mapActions 与 mapMutations 使用时，若需要传递参数：在模板中绑定事件时传递好参数，否则参数是事件对象，因为默认生成的模板为：
```js
eventName1(value){
  this.$store.dispatch('stateHandle-1',value)
}
eventName2(value){
  this.$store.commit('stateHandle-2',value)
}
```
