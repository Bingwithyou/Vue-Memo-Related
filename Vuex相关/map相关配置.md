## mapState方法

如果`actions`不需要相关逻辑，也可以直接跳过`dispatch`来直接调用`commit`，这个时候可能会经常调用`this.$store.state.xxx`



可以使用`mapState`来自动生成调用，先在 **组件(VC)** 中引入`mapState`：

```js
import {mapState} from 'vuex'

// 借助mapState生成计算属性，从state中读取数据（当函数名与数据名一致时，可以写成数组形式：...mapState['a', 'b', 'c']）。

computed: {
    ...mapState({name:'xxx', xuexiao:'school', xueke:'subje}),
}
```
#### '...' 作用是将对象脱掉({ })展开来存放。例：xuexiao: 'school'代表如下代码：
```js
xuexiao(){
    return this.$store.state.school
}
```

同理还有：`mapGetters`, `mapMutations`, `mapActions`

`mapGetters`相当于：
```js
// computed
xxx(){
    return this.$store.getters.xxx
}
```


`mapMutations`相当于：
```js
// methods
xxx(){
    // 注意大写
    this.$store.commit('???')
}
```
>要传值时，需要手动传入，例：`<button @click="xxx(value)"></button>`


`mapActions`传值时和`mapMutations`一样需要手动传入：

```js
// methods
xxx(){
    this.$store.dispatch('???')
}
```
