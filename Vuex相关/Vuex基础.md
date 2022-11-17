### 每一个 Vuex 应用的核心就是 store（仓库）。

`store` 基本上就是一个容器，它包含着你的应用中大部分的状态 `state`。

#### Vuex 和单纯的全局对象有以下两点不同：

1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。



## 安装：

`npm i vuex`

>现在默认安装的Vuex版本为4，只能在Vue3中使用，如果要在Vue2中使用要安装vuex@3版本。

### 指定Vuex的文件夹：

两种方法：

1. 在src文件夹中新建store文件夹，在store中新建index.js（官方）

2. 在src中新建vuex文件夹，在vuex中新建store.js

#### 以第一张方法为例，在store/index.js文件中搭建核心：

```js
// 引入Vue
import Vue from 'Vue'

// 引入Vuex
import Vuex from 'Vuex'

//应用Vuex插件
Vue.use(Vuex)

// 准备actions -- 用于响应组件中的动作，请求
const actions = {}

// 准备mutations -- 用于操作数据
// state
const mutations = {}

// 准备state -- 用于存储数据，组件间可以方便共享
const state = {}

// 创建并暴露store
export default new Vuex.Store({
    actions,
    mutations,
    state,
})
```


之后再`main.js`中引入`store`（默认会读取目录下的`index.js`），并在Vue中应用:

```js
import store from './store'

new Vue({
    render: (h) => h(App),
    store,
}).$mount(#app);
```




### 使用：

1. 在组件中，可以通过dispatch方法使用：`this.$store.dispatch('funtionName', value)`可选value传值



2. 在`store/index.js`的`actions`中定义函数，`actions`函数接收两个参数：

```js
const actions = {
    functionName(context, value){
        ...
    },
    funtionName2(){},
    ....
}
```

其中`context`相当于迷你版的`store`，调用其身上的`commit`方法来到`mutations`进行下一步数据操作。

```js
context.commit("FUNCTIONNAME", value)
```

为了区分与`mutations`里的函数，函数名应该使用**大写**：

```js
const mutations = {
    FUNTIONNAME(state, value){
        ...
    }
}
```
>在`mutations`中可以直接操作数据，业务逻辑等应该写在`actions`里。


#### 当state中的数据需要经过加工后再使用时，可以使用getters加工（别忘记在 export default 中添加getters）：

```js
// store/index.js中定义:
const getters = {
    funtion(state){
        return state....
    }
}
```
>之后在组件中可以通过`this.$store.getters.state`获取值。



## mapState方法

如果`actions`不需要相关逻辑，也可以直接跳过`dispatch`来直接调用`commit`，这个时候可能会经常调用`this.$store.state.xxx`



可以使用`mapState`来自动生成调用，先在组件中引入`mapState`：

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
