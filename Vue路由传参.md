## 为了复用路由组件，可以根据传递的参数来展示不同的页面数据

### 传递参数，to的字符串写法：
**父**路由组件通过在`<router-link>`中指定参数，以'?'开始，'&'分隔：
```js
<router-link to="/home/message/detail?id=123&title=Hola!"></router-link>
```
>如果需要传递组件内的数据，应该先把to绑定：`:to`，然后用模板语法`${}`：
>
>`:to="/home/message/detail?id=${m.id}&title=${m.title}"`

### to的对象写法：
```js
<router-link :to="{
  path:'/home/message/detail',
  query:{
    id:???,
    title:???
  }
}"></router-link>
```

### 接收参数：
经过上一步的传参，detail路由组件身上多了一个`query`存储数据`query: {id: "123", title: "Hola!"}`
在`Detail.vue`组件中调用：
```js
$route.query.id
$route.query.title
```
