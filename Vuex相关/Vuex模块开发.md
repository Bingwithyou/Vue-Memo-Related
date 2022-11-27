 ### 在store/index.js中可以模块化定义相关函数，便于后期维护相关。

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

要在`store/index.js`中，在模块内添加：`namespaced: true`，不然报错

使用`map`相关方法时指定模块：
```js
...mapState('firstFcuntion', [ 'a','b','c' ])
```
`mapActions`和`mapMutations`写法：
```js
...mapActions('funName',{evet1,event2})

...mapMutations('funName',{evet1,event2})
```

#### 提交修改commit时需要注意，不再是简单的添加模块名，而是以斜线`/`分割：

```js
// methods
this.$store.commit('firstFunction/MUTATIONS_NAME', value)

// 其中dispatch的用法同上。
```
Map写法：
```js
...mapGetters('eventName',['handleName']),
...mapMutations('eventName1',{'aaa'})
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
