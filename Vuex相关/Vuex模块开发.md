 ## 在store/index.js中可以模块化定义相关函数，便于后期维护相关。

```js
// 将相关功能和配置定义在一个模块里
const firstFunction = {
    
    actions: {...},

    mutations: {...},

    state: {...},

    getters: {...},
}

const secondFunction = {

    actions: {...},

    mutations: {...},

    state: {...},

    getters: {...},

}
```
### 在export暴露时需要相应修改：
```js
export default new Vuex.Store({
    modules: {
        firstFunction,
        secondFunction,
    }
})
```


### 用到map相关方法时：

1. 在`store/index.js`中，在模块内添加：`namespaced: true`



2. 使用`map`相关方法时，指定模块

3. 以`mapState`为例：`...mapState('firstFcuntion', [ 'a','b','c' ])`


#### 提交修改commit时需要注意，不再是简单的添加模块名，而是以斜线`/`分割：

```js
// methods
this.$store.commit('firstFunction/MUTATIONS_NAME', value)

// 其中dispatch的用法同上。
```

#### 使用getters时注意：
```js
// computed
return this.$store.getters['firstFunction/gettersName']
```
`firstFunction`与`secondFunction`可以进一步模块化：

在store文件夹下新建xxx.js文件并将对应代码转移（不要忘记export）。

之后在`index.js`中进行引入操作：
```js
import firstFunction from './firstFunction'
modules: {
    firstFunction,
}
```
